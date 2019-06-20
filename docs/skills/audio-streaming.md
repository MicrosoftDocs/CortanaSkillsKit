---
title: Add audio streaming to your skill
description: Learn how to add audio streaming to your bot-based skill.
label: Conceptual
ms.assetid: A7CD987E-5DD1-42EA-A436-49D4E8327365
ms.date: 01/23/2019
ms.topic: article

keywords: cortana
---

# Add audio streaming to your skill

> [!NOTE]
> This documentation provides details around streaming audio in Cortana skills built using the Microsoft Bot Framework.
> 


Skills can play rich, long running audio media. You can play a single track or multiple tracks (playlist). Cortana supports the following audio media formats:

|Media|Extension
|-|-
|Audio MP3|mp3
|Audio MP4|m4a
|Audio MP4|aac
|Audio WAV|wav


To play a single track, include a single Audio Card attachment in the message you send Cortana. For playlists, include multiple Audio Card attachments in the message. Each Audio Card should specify a single URL. If you include multiple URLs in one Audio Card, Cortana plays only the first URL. Cortana plays playlists in the order received. 

To specify the audio to play, use the Audio Card's `Media` property. The audio that you want to play must be Internet accessible, and it must use the HTTPS protocol. You should also set the card's `Title` property to the name of the track. Cortana ignores all other Audio Card properties.

Please refer to the [Azure Bot Service documentation](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0) on Media attachments for more details.

The following example shows how to add a single track for Cortana to play and stop the conversation.


```csharp
    // Cards are sent as Attachments in the Bot Framework.
    // So we need to create a list of attachments for the reply activity.
    var attachments = new List<Attachment>();

    // Reply to the activity we received with an activity.
    var reply = MessageFactory.Attachment(attachments);
    
    // Add a single media URL for Cortana to play
    MediaUrl murl = new MediaUrl("https://{yourstreamurl}");
    MediaUrl[] medias = new MediaUrl[] {murl};

    // Create a new AudioCard and attach your media URL
    AudioCard audioCard = new AudioCard()
    {
        Media = medias,
    };

    // Add the attachment and send the reply
    reply.Attachments.Add( audioCard.ToAttachment() );

    // Send the Audio Card
    await turnContext.SendActivityAsync(reply, cancellationToken);
    
    // EndConversation
    var message = turnContext.Activity.CreateReply().AsEndOfConversationActivity();
    await turnContext.SendActivityAsync( message, cancellationToken);
    await _conversationState.ClearStateAsync(turnContext, cancellationToken); // if you have state
```
```javascript
    // create an AudioCard using CardFactory
    let audioCard = CardFactory.audioCard( 'Title', [ "https://{yourstreamurl}" ] );
    
    // set the reply Activity with the card
    await turnContext.sendActivity( { attachments: [ audioCard ] } );
    
    // EndConversation
    await turnContext.sendActivity( { type: ActivityTypes.EndOfCOnversation, code: EndOfConversationCodes.CompletedSuccessfully } );
    // and clear conversation state if any
```


> ![NOTE]
> Cortana does not notify the skill when the audio stream or playlist completes.

If the message includes speech, Cortana reduces the volume of the audio stream (plays it in the background) until she finishes speaking.

To play audio on Windows, Android, and iOS, Cortana must remain open. Closing her canvas ends the audio streaming and skill.


On Windows, Cortana sends user utterances to your skill until you end the conversation. After you end the conversation, Cortana handles the user's utterances. However, on speaker-only devices, Cortana handles all user utterances while an audio stream is playing. For your skill to receive user utterances while the audio is playing, the user must invoke your skill (for example, "Ask My Radio to...").

<!--
// Commented out because these features do not work with third party skills.
// Also, current OTG/UWP only play one audio card.

## Skill audio commands

Skills may send the following audio commands to Cortana while she's streaming your files.

|Command|Description
|-|-
|Stop|Cortana stops playing the audio stream. 


The following example shows how to send a Stop event. The message type must be `ActivityTypes.Event`, and the event's name must be `media/stop`.


```csharp
Activity reply = activity.CreateReply();
                    reply.Type = ActivityTypes.Event;
                    reply.Name = "media/stop";
                    reply.InputHint = InputHints.ExpectingInput;

                    await connector.Conversations.ReplyToActivityAsync(reply);
```


For speaker-only devices, you should not send this event unless your skill is the one playing the audio; Cortana stops streaming whatever is playing whether it was initiated by you or another skill.


## User audio commands

Users may use the following Cortana commands to control streaming on speaker-only devices:

|Command|Description
|-|-
|Stop|Stops the audio streaming. 
|Pause|Pauses the audio streaming.
|Resume|Resumes the audio streaming.
|Next|Play the next track in a playlist.
|Previous|Play the previous track in a playlist.

To use the commands, user's must prefix the command with, "Hey Cortana". For example, “Hey Cortana, Pause.” Cortana uses these commands to control the audio; these commands are not passed to the skill. 

If the device includes a controller, you can also use it control the audio play. 

The commands are not supported on Windows, iOS, or Android devices.



## Getting the playback state

If your skill is playing audio, any message that Cortana sends your skill includes a `CurrentAudioInfo` object in the message's `channelData` property. For example, if the user says, "Hey Cortana, ask My Tuner what's playing," you can access the channel data's `currentAudioInfo` property to get details about the audio that's playing. 

The following are the `CurrentAudioInfo` properties.

| Name | Type | Description 
|-|-|-
| Url | string | The URL of the audio stream that's playing. 

<!- - | Value | String | A user-defined value that's stored with the audio stream. - ->

Cortana includes the `CurrentAudioInfo` object in the channel data on speaker-only devices only.

The following example shows how to get the audio information from the message's channel data.

```csharp
    JObject valueObj = JsonConvert.DeserializeObject<JObject>(activity.ChannelData.ToString());
    string url = "";
    JObject currentAudioObject = JsonConvert.DeserializeObject<JObject>(valueObj["currentAudioInfo"]?.ToString() ?? "");
    if(currentAudioObject!=null)
    {
        url = currentAudioObject["url"]?.ToString() ?? "";
    }
```

## Known issues

The following are known issues.

|Platform|Expected behavior|Issue
|-|-|-
|Windows, iOS, Android|If your message includes speech along with the audio attachment, Cortana reduces the volume of the audio stream (plays it in the background) until she finishes speaking.|The audio volume does not reset to normal levels.
|Windows, iOS, Android|Users may use the Cortana commands to control streaming, such as pause, resume, next, and previous.|Not supported.

-->
