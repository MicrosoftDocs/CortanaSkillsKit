---
title: Adding audio to Cortana Skills
description: Describes how to develop a Cortana Skill that uses SSML and streaming audio.

ms.date: 10/08/2018
ms.topic: article

keywords: cortana
--- 

# Adding audio to Cortana skills

Whether you are developing a Cortana skill for a device without a screen such as the Invoke speaker (a *headless device*), or a device with a screen such as a PC or mobile device, you can use a variety of audio features to enhance a user's experience. 

In addition to Cortana's built-in text-to-speech technology, you can:

* Use Speech Synthesis Markup Language (SSML) to customize speech and embed short audio clips. 
* Use an audio card to stream audio.

In [Create your first Cortana skill](./mva22-hello-world.md) and [Building conversations](./mva32-building-conversations.md) you learned how to use the basic functionality of Cortana's text-to-speech technology. In this module you'll see how to extend the **Mixtape** skill developed in [Building conversations](./mva32-building-conversations.md) to include additional audio elements.

## Step 1 - Customize how Cortana speaks

You can use SSML to customize and enhance the **Mixtape** skill created in [Building conversations](./mva32-building-conversations.md). You can adjust a variety of speech attributes, including the speed at which Cortana speaks.

To increase the speed at which Cortana speaks, revise the **MixtapeIntent** method in the **BasicLuisDialog.cs** module of your **Mixtape** skill as follows:

        public async Task MixtapeIntent(IDialogContext context, LuisResult result)
        {
            var response = context.MakeMessage();
            response.Text = "Welcome to Mixtape! Let's find a song to play.";

            var ssml = @"<speak version=""1.0"" xmlns = ""https://www.w3.org/2001/10/synthesis"" xml:lang = ""en-US""> 
                <prosody rate=""fast"">
                Welcome to Mixtape! Let's find a song to play. 
                </prosody>
            </speak>";

            response.Speak = ssml;

            response.InputHint = InputHints.ExpectingInput;
            await context.PostAsync(response);
            context.Wait(MessageReceived);
        }

SSML enables you to control a variety of speech attributes. You can use the *prosody* element to control pitch, speaking rate, and volume of speech output. For more information about SSML, see [Speech Synthesis Markup Language (SSML) reference](./speech-synthesis-markup-language.md).

## Step 2 - Play an audio clip when a skill starts

You can also use SSML to embed an audio clip in Cortana's response. For example, revise the **MixtapeIntent** method code as follows to play an audio file when the Mixtape skill starts.

        public async Task MixtapeIntent(IDialogContext context, LuisResult result)
        {
            var response = context.MakeMessage();
            response.Text = "Welcome to Mixtape! Let's find a song to play.";

            var ssml = @"<speak version=""1.0"" xmlns = ""https://www.w3.org/2001/10/synthesis"" xml:lang = ""en-US""> 
                <prosody rate=""fast"">
                Welcome to Mixtape! 
                <audio src=""https://myaudio/tada.mp3>""/>
                Let's find a song to play. 
                </prosody>
            </speak>";

            response.Speak = ssml;

            response.InputHint = InputHints.ExpectingInput;
            await context.PostAsync(response);
            context.Wait(MessageReceived);
        }

Use the *audio* element to play an audio file. In this case, the skill plays a short MP3 file, *tada.mp3*.

## Step 3 - Test the revised skill

Before you can test the revised skill, you must republish it. If you are working in the Microsoft Azure App Service Editor or in Visual Studio, follow the redeployment steps in [Create your first Cortana skill](./mva22-hello-world.md) or [Building conversations](./mva32-building-conversations.md).

To test your revised skill, direct Cortana to invoke the skill using the invocation name you specified. Cortana responds with the text you specified and plays the *tada.mp3* audio file.

![Play Audio](../media/images/mva41_tada.png)

## Step 4 - Play an audio track in response to a request

In addition to playing an audio clip when the skill starts, your Mixtape skill can play one or more audio files in response to a request to play a song. As you saw in [Building conversations](./mva32-building-conversations.md), you can create a variety of *intents* in the skill's underlying LUIS application. For example, you could add a **PlaySong** intent with utterances such as:

* What music do you have?
* Play me a song.
* I want to listen to music.

Over time, the skill uses language understanding to learn to trigger the intent when a user makes a similar request.

You can then add code to the Mixtape skill to play an audio track, or multiple audio tracks, when a user triggers the intent. To add streaming audio in your skill, use an *Audio card*. For example, revise the Mixtape skill's **PlaySongIntent** method as follows:

    public async Task PlaySongIntent(IDialogContext context, LuisResult result)
    {
        var response = context.MakeMessage();
        response.Text = "Here's a song for you.";

        AudioCard card = new AudioCard
        { 
              Media = new MediaUrl[] { new MediaUrl("https://myaudio.azurewebsites.net/song.mp3") }
        };

        response.Attachments.Add(card.ToAttachment());

        response.InputHint = InputHints.ExpectingInput;
        await context.PostAsync(response);
        context.Wait(MessageReceived);
    }

The code creates an Audio card that plays the audio file *song.mp3*. To stream additional audio files, create an Audio card for each file, and then add the Audio cards as attachments to the Cortana response.

For more information on adding audio streaming to your skill, see [Add audio streaming to your skill](./audio-streaming.md).

## Step 5 - Test the revised skill

As you did earlier in Step 3, you must redeploy the skill to test it. Then direct Cortana to invoke the skill using an invocation such as, "Ask Mixtape to play me a song." Cortana responds with the text you specified in the **PlaySongIntent** method and streams the *song.mp3* audio file.
