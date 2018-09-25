---
title: Using client code with Cortana skills
description: Describes how to use client code with a Cortana skill.

ms.date: 09/25/2018
ms.topic: article

keywords: cortana
---

# Using client code with Cortana skills

|   |   |
| - | - |
| ![](../images/video-icon.png) | [Watch a video](https://mva.microsoft.com/en-US/training-courses/getting-started-with-cortana-skills-18241?l=03ED05boE_4411787171) about using client code with Cortana skills. |


In addition to developing audio and video interfaces to enhance your Cortana skill, you can create interfaces that launch native code on a user's active device. In [Adding audio to Cortana skills](./mva41-streaming-audio.md) and [Adding visual elements to Cortana skills](./mva42-visual-ux.md), you learned how to use audio and visual elements in your skill. In this module you'll see how to extend the **Mixtape** skill to use client code.

If you are creating a Cortana skill for a Windows, Android, or iOS device, your skill can launch apps or web sites to help users get things done. For example, your skill may involve completing a complex task or require a larger visual canvas than a visual interface card can provide. You can specify a protocol or application, and the skill launches a *deep link* using that protocol or application. 

Deep linking is useful when Cortana and your app service act as a gateway to your full-featured app (instead of requiring the user to launch the app through the Start menu), or for providing access to richer detail and functionality within your app that is not possible through Cortana. 

In this module you'll learn how to extend the **Mixtape** skill developed in [Building conversations](./mva32-building-conversations.md) to enable a user to save a song by sending it via email when the **SaveSong** intent is invoked.

## Step 1 - Revise your skill to launch email 

You can use Cortana's **ChannelData** object to launch the default client email using the [mailto URI protocol](https://msdn.microsoft.com/en-us/library/jj710215(v=vs.85).aspx). Revise the **SaveSongIntent** method in the **BasicLuisDialog.cs** module of your **Mixtape** skill as follows:

    public async Task SaveSongIntent(IDialogContext context, LuisResult result)
    {
        var response = context.MakeMessage();
        response.Text = "Sign in to save the song to a mixtape.";
        response.Speak = response.Text;

        response.ChannelData = JObject.FromObject(new
        {
            action = new { type = "LaunchUri", uri = "mailto://" }
        });

        await context.PostAsync(response);
        context.Wait(MessageReceived);
    }

For more information on working with the **ChannelData** object, see [Get Cortana's channel data](./cortana-channel-data.md).

You can also use the **ChannelData** object to launch a variety of apps or websites from a Cortana skill. For more information, see [Launching apps or websites from a Cortana skill](./launch-apps-from-skills#launching-and-deep-linking-an-app.md).

## Step 2 - Vary the skill's response depending on the type of device

The Mixtape skill can save a song by sending it in email if a user invokes the skill on a device with a screen and email client, but that approach will not work correctly for a headless device such as the Invoke speaker. To make sure the skill works correctly for the current device, you can check the device's **supportsDisplay** property and then take appropriate action. Revise the **SaveSongIntent** method as follows:

    public async Task SaveSongIntent(IDialogContext context, LuisResult result)
    {
        var response = context.MakeMessage();

        var userInfo = ((Activity)context.Activity).Entities.FirstOrDefault(e => e.Type.Equals("DeviceInfo"));
        var hasDisplay = userInfo.Properties["supportsDisplay"].ToString();

        if (hasDisplay =="true")
        {
            response.ChannelData = JObject.FromObject(new
            {
                action = new { type = "LaunchUri", uri = "mailto://" }
            });
        }
        else
        {
            response.Text = "Sorry, I cannot save this song on this device. Check back soon.";
            response.Speak = response.Text;
        }

        await context.PostAsync(response);
        context.Wait(MessageReceived);
    }

The skill now launches the device's default mail program if the device's **supportsDisplay** property is **true**. Otherwise, the skill responds with a message that Cortana cannot save the song on the device.

## Step 3 - Add a subject line to the email message

You can further enhance the Mixtape skill by passing data from the service to the mail application. You can add query parameters to the **mail to** deep link to pass a variety of information to the application. For example, revise the **SaveSongIntent** method as follows to add a subject line to the message sent by Cortana:

    public async Task SaveSongIntent(IDialogContext context, LuisResult result)
    {
        var response = context.MakeMessage();

        var userInfo = ((Activity)context.Activity).Entities.FirstOrDefault(e => e.Type.Equals("DeviceInfo"));
        var hasDisplay = userInfo.Properties["supportsDisplay"].ToString();

        if (hasDisplay =="true")
        {
            response.ChannelData = JObject.FromObject(new
            {
                action = new { type = "LaunchUri", uri = "mailto://?subject=Save%20this%20song" }
            });
        }
        else
        {
            response.Text = "Sorry, I cannot save this song on this device. Check back soon.";
            response.Speak = response.Text;
        }

        await context.PostAsync(response);
        context.Wait(MessageReceived);
    }

In addition to the subject line, you can add a variety of items as parameters to the **mail to** deep link. For more information on **mail to** protocol query parameters, see [mailto Protocol](https://msdn.microsoft.com/en-us/library/aa767737(v=vs.85).aspx).

## Step 4 - Test the revised skill

Before you can test the revised skill, you must republish it. If you are working with the Microsoft Azure App Service Editor or in Visual Studio, follow the redeployment steps in [Create your first Cortana skill](./mva22-hello-world.md) or [Building conversations](./mva32-building-conversations.md).

To test your revised skill, direct Cortana to invoke the Mixtape skill using an invocation phrase related to the **SaveSong** intent. For example:

*Ask Mixtape to save a song.*

If you invoked the skill on a device that supports visual display, Cortana responds by launching the device's default mail application with the subject line you specified.

![Save CSongard](../images/mva43-save-song.png)