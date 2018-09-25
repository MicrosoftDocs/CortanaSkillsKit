---
title: Cortana Skills Kit FAQ
description: Tips on Testing & Debugging Cortana Skills.

ms.assetid: 3f37e309-3170-4896-8434-33bdce3c1889
ms.date: 09/25/2018
ms.topic: article

keywords: cortana
---

# Cortana Skills Kit FAQ

<!-- Need to go through comments on docs.ms.com and see if we should add any of them -->

<!-- Need to confirm that these answers are still accurate. -->

**Can Cortana provide the users IP Address?**

Currently the Cortana skills kit does not provide access to the user's IP Address.

**Can Cortana Skills access insights about the user such as their location?**

Cortana Skills Kit provides access to user profile and context information such as cuisine preferences and user location. For more information, see [Get user profile and contextual information](get-user-profile-context.md).

**Can a custom skill be invoked without the invocation name if there are no competing skills available?**

No. You must use the skill's invocation name to invoke them.

**Can I define the voice used when users talk to my skill?**

No. You may use SSML to change her speech patterns but not her voice. For more information, see [Speech Synthesis Markup Language (SSML) reference](speech-synthesis-markup-language.md).

**Can I re-use custom intents or entities across my Cortana skills?**

Yes, you may use a single language model across your bots. 

**Does my skill have to run on Azure?**

No. Any internet accessible endpoint is an option. 

**How does Cortana Skills Kit, Cortana Devices SDK and Cortana Intelligence Suite play together?**

Microsoft is deeply committed to its AI vision, and sees key roles for agents, apps, services and infrastructure. Cortana is an agent, a personal digital assistant, designed to help users achieve more. Many of the intelligent services that Cortana uses are available to enterprises to build their own intelligent experiences. 

* **Cortana Intelligence Suite** allows enterprises and developers to build their own intelligent experiences using enterprise-grade APIs from Microsoft. Find out more [here](https://www.microsoft.com/en-us/cloud-platform/cortana-intelligence-suite).
* **Cortana Devices SDK** allows OEMs/ODMs to bring the Cortana personal assistant to their devices where she can run on top of different underlying OSes - including variants of Linux, Android, and Windows IoT. [Interested? Contact us for more info](https://aka.ms/cortanadevicepreview).
* **Cortana Skills Kit** allows developers to integrate their experiences (bots, web services, apps, and websites) with Cortana so she can intelligently drive engagement of these experiences when the user needs them.

Cortana Skills Kit is designed to:

* **Allow developers to reuse their existing investment** in Bot Framework bots.
* **Offer multi-platform reach** by being able to run skills wherever Cortana is available.
* **Access the user's contextual information, with their permission** to provide them a personalized experience. Users control their information stored in Cortana's Notebook.
* **Use a flexible language to invoke your skill**, so users don't need to memorize specific phrases.
* **Allow you access to a large install base** with over 145 million monthly, active users and growing.

**How do you add re-prompts using Bot Framework?**

Currently Bot Framework does not support re-prompts.
<!-- Is this true? I thought they had the retry field? -->


**How long can Cortana's speech response be?**

Your response may contain a maximum of 90 seconds of speech.

**How many intents and entities can a skill have?**

<!-- This doesn't sound right. Doesn't the language model/service they choose to use decide the limits? Shouldn't this read: That's up to the language understanding service you use. If you use [LUIS](https://luis.ai) (recommended), it supports 80 intents, 30 custom entities and 10 built-in entities in a single language model. -->

Cortana uses Luis.ai to build a custom language model for your skill. Luis.ai supports 80 intents, 30 custom entities and 10 built-in entities in a single language model. 

**How many users can access my skill?**

Cortana has 145 million monthly, active users. Your skills are available on any device running Cortana. 

**How will you prevent Cortana saying sexual, racist, or otherwise inappropriate things through a third-party skill?**

Cortana Skills are governed by developer terms of use (TOU) that prohibits inappropriate content. This is similar to the terms that govern applications on Microsoft Store. In addition to a certification process, any skills that are reported to violate the TOU (for content or otherwise) will be audited and removed from the platform. 

**Is two-factor authentication supported?**

Cortana Skills currently do not support two-factor authentication. However, it is possible to use a Connected Account and a Bot Framework Sign-in card in the same skill and thus require two methods of authentication.

**I've already built a VCD, will that just work with Skills Kit?**

Your voice command definition (VCD) will continue to work. 

**I've built a bot for Facebook, what do I do next?**

You can convert your Facebook bot to a Cortana skill in the following ways:
* If you leveraged Microsoft Bot Framework to create your Facebook bot, then you can make it into a Cortana Skill with a minimal set of modifications. <!-- Would be nice to mention what changes. Are there design changes or just add speech? -->
* If you leveraged Facebook's API directly, then you need to expose a separate endpoint using Microsoft Bot Framework.

**Will my skill work with voice and text?**

<!-- Is this asking about typing into "Type here to search" or "Ask me anything" instead of using the microphone? -->
<!-- Has it been added? Still plans? How far out? -->

Beginning with the Windows 10 Fall Creators Update (or the latest version of Cortana for iOS or Android), users can use voice or text to interact with your skill. Previously, users could interact with your skill only using voice.

**What is the difference between the language support capabilities in VCD versus what is offered with Cortana Skills Kit?**

Cortana Skills Kit provides true natural language support instead of the more limited, rules-based triggering supported in voice command definitions (VCD). Natural language models are extensible and developers can train their skills with sample utterances. 

Another limitation of VCDs is that you must install them on the Windows device whereas skills are cloud-based and cross-platform.

Currently, Cortana Skills Kit enables skills in the US only whereas VCDs are supported in all 14 Cortana languages.

<!-- //TODO update regions -->

**When I convert my bot into a Cortana Skill, will Cortana speak the bot's response in Cortana's voice?**
<!-- This seems like a duplicate -->

Yes. Cortana does not support using a custom voice.

**What markets are supported and what is the timeline?**

Currently, Cortana Skills supports only the en-US market. LUIS supports a wider range of locales, and the Cortana skills team is certainly planning to add support for more locales in the near future. For a list of languages that LUIS supports, see [LUIS Supported Languages](https://docs.microsoft.com/azure/cognitive-services/LUIS/Home#supported-languages).

<!-- //TODO update regions -->

**Why is Cortana Skills Kit only available in limited markets?**

We want to ensure the Cortana Skills Kit is available at high quality, with natural language support. We are working on making the Cortana Skills Kit available in more markets over time, and will announce additional markets as they become available. 


## Next steps

See also [Bot Framework FAQ](https://aka.ms/s5qwzg).
