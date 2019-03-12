---
title: Cortana Skills Kit FAQ
description: Tips on Testing & Debugging Cortana Skills.

ms.assetid: 3f37e309-3170-4896-8434-33bdce3c1889
ms.date: 02/26/2019
ms.topic: article

keywords: cortana
---

# Cortana Skills Kit FAQ

<!-- Need to confirm that these answers are still accurate. **Can Cortana provide the user's IP Address?**-->

### What markets (locales) are supported?

Currently, Cortana Skills supports the U.S. market only (en-US locale). 

### Is there a timeline for adding more locales?

LUIS supports a wider range of locales, and the Cortana skills team is planning to add support for more locales as soon as possible.

### Why do I get redirected to Bing when I invoke my skill?

By default, when Cortana does not recognize an invocation name it will redirect to Bing search. There are a few reasons this might happen.
1. If the skill is in development, the account logged in with Cortana is not the same as the account that self-published the skill. You must be logged in on the account that published the skill. Check that the account logged in to Cortana (type "settings" into the address bar, or click on the `Settings` button, and then click on `Your account info`), is the same as the account that published the skill on the Azure portal.
1. The device's region is not U.S., or the language is not English. Check the device's region and language settings; they must be en-US.
1. Cortana is disabled by policy on the device in use.
1. You're logged in with an Azure Active Directory (AAD) account. Third party skills are not supported for enterprise accounts.
1. You've found a bug! If you think you've found one, write to the support team at skillsup@microsoft.com.

If these scenarios do not apply, please check the [Known Issues](./known-issues.md) page.

### Why does my skill time out on the first invocation?

If you use an Azure free tier service plan or the default standard tier plan for your App Service, the App Service will be _unloaded_ after a 20 minute idle period when not in use. This prevents unnecessary resource usage. It may take some time for the service to load when you invoke your skill after it's been unloaded, which results in a "Sorry, but [your skill] isn't responding right now" error. If you use a standard service plan, you can prevent this by changing the App Service state (under Application Settings / General Settings ) to `Always On`. This will keep your app loaded, but will also increase your resource usage.
If you use the free tier plan, you can't change this setting.

 Find more performance guidance in the [Azure FAQ](https://docs.microsoft.com/en-us/azure/app-service/faq-availability-performance-application-issues#how-do-i-decrease-the-response-time-for-the-first-request-after-idle-time).

### Can I get access to the raw voice data?

No. Voice data is processed by _the agent_ and is transient for privacy reasons.

### Can Cortana provide the user's IP Address?

Currently, the Cortana skills kit does not provide access to the user's IP Address.

### Can Cortana Skills access insights about the user such as their location?

Cortana Skills Kit provides access to user profile and context information, including user location. For more information, see [Get user profile and contextual information](get-user-profile-context.md).

### Can a custom skill be invoked without the invocation name if there are no competing skills available?

No. The user must use the skill's invocation name.

### Can I define the voice used when users talk to my skill?

No. You may use SSML to change Cortana's speech patterns, but not her voice. For more information, see [Speech Synthesis Markup Language (SSML) reference](speech-synthesis-markup-language.md).

### Can I re-use custom intents or entities across my Cortana skills?

Yes, you may use a single language model across your bots. 

### Does my skill have to run on Azure?

No. Any internet accessible endpoint is an option. Your service endpoint must be configured to accept `POST` requests, not `GET` requests.
<!-- Added the request type based on content in the Testing and debugging Cortana Skills page. More info would be better. -->

### How do the Cortana Skills Kit, Cortana Devices SDK, and Cortana Intelligence Suite work together?

Microsoft is deeply committed to its AI vision, and sees key roles for agents, apps, services, and infrastructure. Cortana is a personal digital assistant, an agent, designed to help users achieve more. Many of the intelligent services that Cortana uses are available to enterprises to build their own intelligent experiences. 

* **Cortana Skills Kit** allows developers to integrate their experiences (bots, web services, apps, and websites) with Cortana so she can intelligently drive engagement of these experiences when the user needs them.
* **Cortana Devices SDK** allows OEMs/ODMs to bring the Cortana personal assistant to their devices where she can run on top of different underlying OSes - including variants of Linux, Android, and Windows IoT. [Interested? Contact us for more info](https://aka.ms/cortanadevicepreview).
* **Cortana Intelligence Suite** allows enterprises and developers to build their own intelligent experiences using enterprise-grade APIs from Microsoft. Find out more [here](https://www.microsoft.com/en-us/cloud-platform/cortana-intelligence-suite).

Cortana Skills Kit is designed to:

* **Allow developers to reuse their existing investment** in Bot Framework bots.
* **Offer multi-platform reach** by being able to run skills wherever Cortana is available.
* **Access the user's contextual information, with their permission**, to provide users with a personalized experience. Users control their stored information via Cortana's Notebook.
* **Use flexible language to invoke your skill**, so users don't need to memorize specific phrases.
* **Allow you access to a large installed base** , currently over 145 million monthly, active users, and growing.

### How do you add re-prompts using Bot Framework?

Currently the Bot Framework does not support re-prompts.
<!-- Is this true? I thought they had the retry field? -->

### How long can Cortana's speech response be?

Your response may contain a maximum of 90 seconds of speech.

### How many intents and entities can a skill have?

That's up to the language understanding service you use. If you use [LUIS](https://luis.ai) (recommended), it currently supports 80 intents, 30 custom entities, and 10 built-in entities per single language model. 

### How many users can access my skill?

Cortana has 145 million monthly, active users. Your skills are available on any device running Cortana. 

### How will you prevent Cortana saying sexual, racist, or otherwise inappropriate things through a third-party skill?

Cortana Skills are governed by developer terms of use (TOU) that prohibit inappropriate content. This is similar to the terms that govern applications on Microsoft Store. In addition to a certification process, any skills that are reported to violate the TOU, for content or otherwise, will be audited and removed from the platform. 

### Is two-factor authentication supported?

Cortana Skills currently do not support two-factor authentication. However, it's possible to use a Connected Account and a Bot Framework Sign-in card in the same skill, thus requiring two methods of authentication.

### I've already built a voice command definition, will that just work with the Skills Kit?

Yes, your voice command definition (VCD) will continue to work.

### I've built a bot for Facebook. What do I do next?

You can convert your Facebook bot to a Cortana skill in the following ways:
* If you leveraged Microsoft Bot Framework to create your Facebook bot, then you can make it into a Cortana Skill with a minimal set of modifications. <!-- Would be nice to mention what changes. Are there design changes or just add speech? Quick search of docs for Facebook shows nothing.-->
* If you leveraged Facebook's API directly, then you need to expose a separate endpoint using Microsoft Bot Framework.

### Will my skill work with voice and text?

Beginning with the Windows 10 Fall Creators Update (September 2017, version 1709), or the latest version of Cortana for iOS or Android, users can use voice or text to interact with your skill.

### Does Cortana work differently on devices that don't have a display, like the Invoke speaker)?

Yes. By design, the microphone is closed on headless devices (devices without a display) after Cortana receives user input. This closes the conversation and loses any context. Because of this, you must use `ExpectingInput` in these devices, and not `AcceptingInput`.

### What is the difference between the language support capabilities in VCD versus what is offered with Cortana Skills Kit?

Cortana Skills Kit provides true natural language support instead of the more limited, rules-based triggering supported in voice command definitions (VCD). Natural language models are extensible and developers can train their skills with sample utterances. 

Another limitation of VCDs is that you must install them on the Windows device whereas skills are cloud-based and cross-platform.

Currently, Cortana Skills Kit enables skills in the U.S. only (en-US locale) whereas VCDs are supported in all 14 Cortana languages.

<!-- //TODO update regions -->

### When I convert my bot into a Cortana Skill, will Cortana speak the bot's responses in Cortana's voice?

Yes.  You may use SSML to change Cortana's speech patterns, but not her voice. For more information, see [Speech Synthesis Markup Language (SSML) reference](speech-synthesis-markup-language.md).

### Why is the Cortana Skills Kit only available in limited markets?

We want to ensure that the Cortana Skills Kit is available at high quality, and with natural language support. We are working on making the Cortana Skills Kit available in more markets over time, and will announce additional markets as they become available.
