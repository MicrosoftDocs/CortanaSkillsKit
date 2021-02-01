---
title: Add audio streaming to your skill
description: Learn how to add audio streaming to your bot-based skill.
label: Conceptual
ms.assetid: A7CD987E-5DD1-42EA-A436-49D4E8327365
ms.date: 07/08/2019
ms.topic: article

keywords: cortana
---

# Add audio streaming to your skill

> [!NOTE]
> This documentation provides details about streaming audio in Cortana skills built using the Microsoft Bot Framework.
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

Please refer to the [Azure Bot Service documentation](/azure/bot-service/bot-builder-howto-add-media-attachments?preserve-view=true&view=azure-bot-service-4.0) on Media attachments for more details.

The following example shows how to add a single track for Cortana to play and stop the conversation.

# [C#](#tab/cs)

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

# [JavaScript](#tab/js)

```javascript
    // create an AudioCard using CardFactory
    let audioCard = CardFactory.audioCard( 'Title', [ "https://{yourstreamurl}" ] );
    
    // set the reply Activity with the card
    await turnContext.sendActivity( { attachments: [ audioCard ] } );
    
    // EndConversation
    await turnContext.sendActivity( { type: ActivityTypes.EndOfConversation, code: EndOfConversationCodes.CompletedSuccessfully } );
    // and clear conversation state if any
```

---

Be sure to use `ExpectingInput` as the input hint in your message. You should not use `IgnoringInput` as the input hint. If you set the hint to `IgnoringInput` without sending a follow-up `ExpectingInput` hint, the conversation will eventually error out because the system is expecting your skill to send another message.

> [!NOTE]
> Cortana does not notify the skill when the audio stream or playlist completes.

If the message includes speech, Cortana reduces the volume of the audio stream (plays it in the background) until she finishes speaking.

To play audio on Windows, Android, and iOS, Cortana must remain open. Closing her canvas ends the audio streaming and skill.

On Windows, Cortana sends user utterances to your skill until you end the conversation. After you end the conversation, Cortana handles the user's utterances. However, on speaker-only devices, Cortana handles all user utterances while an audio stream is playing. For your skill to receive user utterances while the audio is playing, the user must invoke your skill (for example, "Ask My Radio to...").