---
title: Using profile data in your Cortana Skill
description: Describes how to use profile data in your Cortana Skill.

ms.date: 10/08/2018
ms.topic: article

keywords: cortana
---

# Using profile data in your Cortana skill

As you learned in [Understanding Cortana's user profile data](./mva51-profile-data.md), Cortana's user profile contains a variety of information that you can view and use in your Cortana skill with the user's consent. In this module, you'll learn how to customize the **Mixtape** skill developed in previous modules to include profile data.

For more information about user profile and contextual information, see [Get the user's profile and contextual information](./get-user-profile-context.md). 

For reference information on the user profile entities you can use in code when you are developing your Cortana skill, see [Cortana user profile and contextual information reference](./user-profile-contextual-info.md).

## Step 1 - Configure your skill to request user profile data

As you learned in [Create your first Cortana skill](./mva22-hello-world.md) and [Building conversations](./mva32-building-conversations.md), you register a Cortana skill by connecting your bot to the Cortana channel.

To make user profile data available to your Cortana skill, update the skill's channel configuration settings.

<!--
![Knowledge Store Publish](../media/images/mva52_ks_publish.png)
-->

Select **Publish to self**. In the **User data** box, specify the user profile data that you want to make available. For example, to make the user's name available, select **User.Info.Name**.

<!--
![User Data](../media/images/mva52_info_name.png)
-->

## Step 2 - Revise your skill to use profile data

Now that you configured your Cortana skill to request user profile data, you can use that data to customize the skill. For example, you can personalize the greeting in the Mixtape skill to include the user's name by revising the skill's **MixtapeIntent** method as follows:

        public async Task MixtapeIntent(IDialogContext context, LuisResult result)
        {
            var userInfo = ((Activity)context.Activity).Entities.FirstOrDefault(e => e.Type.Equals("UserInfo"));
            string userName;
            if (userInfo != null)
                userName = userInfo.Properties["userName"]["GivenName"].ToString();
            else
                userName = "Stranger";
            
            var response = context.MakeMessage();
            response.Text = "Welcome to Mixtape, " + userName + "! Let's find a song to play.";

            var ssml = @"<speak version=""1.0"" xmlns = ""https://www.w3.org/2001/10/synthesis"" xml:lang = ""en-US""> 
                <prosody rate=""fast"">
                Welcome to Mixtape" + userName + @"! 
                <audio src=""https://myaudio/tada.mp3>""/>
                Let's find a song to play. 
                </prosody>
            </speak>";

            response.InputHint = InputHints.ExpectingInput;
            await context.PostAsync(response);
            context.Wait(MessageReceived);
        }

The code adds the user's name from the **UserInfo** profile data to the Mixtape greeting.

## Step 3 - Test the revised skill

Before you can test the revised skill, you must republish it. If you are working with the Microsoft Azure App Service Editor or in Visual Studio, follow the redeployment steps in [Create your first Cortana skill](./mva22-hello-world.md) or [Building conversations](./mva32-building-conversations.md).

To test your revised skill, direct Cortana to invoke the Mixtape skill using an invocation phrase related to the **Mixtape** intent. For example:

*Ask Mixtape to make me a new playlist.*

Since you have configured Cortana to request user profile data, Cortana asks your consent before launching the skill. Cortana will not use information from the user profile without explicit consent.

![Ask Consent](../media/images/mva52_ask_consent.png)

If you give your consent, Cortana responds by launching the Mixtape skill with a personalized greeting, using the name specified in the user profile.
