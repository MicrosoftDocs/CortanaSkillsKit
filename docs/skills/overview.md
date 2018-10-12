---
title: Overview of Cortana Skills - Cortana skills design and development
description: Provides an overview of Cortana Skills Kit and how you can use it to extend Cortana so your users can use Cortana to interact with your service.

ms.assetid: 6dad0848-3886-4729-90fa-0bcd424b3561
ms.date: 10/08/2018
ms.topic: article

keywords: cortana
---

# Cortana Skills Kit

>[!NOTE]
> Cortana Skills Kit is currently in public preview.  

Cortana is a digital assistant that keeps users informed and productive, helping them get things done across devices and platforSkills define the tasks that Cortana can accomplish. Cortana invokes the skills based on spoken input from the user. You can extend Cortana by adding your own skills that let your users use Cortana to interact with your service.

To extend Cortana, use the Cortana Skills Kit. The kit is a suite of tools that help you build skills that connect users to your custom services and solutions. 

The following components make up the skills kit.

- [Bot Framework](https://docs.microsoft.com/bot-framework/)  
  A skill is a speech bot. Use the Bot Framework to build your speech bot, register it, and define your Cortana channel. The framework provides a .NET SDK and Node.js SDK that you use to build your bot. The Bot Framework SDKs provide features such as dialogs and built-in prompts that make interacting with users much simpler. The Bot Builder SDK is provided as open source on GitHub (see [BotBuilder](https://github.com/Microsoft/BotBuilder)). For an overview of how the framework works, see [How the Bot Framework works](https://docs.microsoft.com/bot-framework/overview-how-bot-framework-works).
  
- [Cortana Skills Dashboard](https://developer.microsoft.com/en-us/cortana/dashboard#!/home)  
  The dashboard lists the skills that you have configured a Cortana channel for. Use the dashboard to deploy your skill to yourself (default), a group of users, or the world. Publishing your bot in Bot Framework does not make it available to users. To make your skill available to users, you must use the dashboard. You also use the dashboard to turn on debugging so you can see the message exchange between your bot and Cortana.

Because Cortana is available on many different devices, some may have a screen while others may be a standalone speaker. You should ensure that your bot is capable of handling both scenarios. The bot framework provides device information as an entity of the activity. 

The following image shows how users interact with Cortana and your skill.

![Cortana Skills workflow](./media/images/workflow.png)

## How do users invoke skills?

Users invoke skills simply by speaking to Cortana. Users don't install or activate skills.

<!-- I'm confused by "don't install or activate" because there's this site where they can discover new skills: https://www.microsoft.com/en-us/windows/cortana/cortana-skills/. And in Cortana Notebook there's Skills, which they use to "manage and control what skills you've connected to."-->

Users invoke skills by speaking or typing to Cortana, optionally by providing an **invocation phrase**. The invocation phrase includes an **invocation name**, which uniquely identifies the skill to invoke. For example, if a skill's invocation name is "Northwind Photo", the user might say "Ask Northwind Photo to..." or "Tell Northwind Photo that...". You specify the name when you configure the Cortana channel for your skill. For a list of invocation phrases, see [Invocation Name Guidelines](./cortana-invocation-guidelines.md). 

If an invocation name is not provided, Cortana will try to suggest a skill to the user in order to fulfill their request.

Users can invoke skills on any platform that includes Cortana. For a list of platforms, see (#Platform-requirements).

For a list of locales where users can invoke skills, [Supported locales](./supported-locales.md).

>[!NOTE]
> Cortana supports skills in the en-US locale only.

## How do users interact with skills?

When a user invokes your skill, Cortana sends a structured request to the service that powers your skill and waits for a response. There are two ways that Cortana listens for requests. The first is when the user presses the microphone button in the Cortana app or in the "Ask me anything" search box in Windows. The second is when the user enables Cortana to respond to "Hey Cortana". The following are examples of how users might interact with Cortana.

If a user asks Cortana about the weather, Cortana triggers the built-in weather skill. For example:

```
User: "What is the weather like?"
Cortana: "It is currently 58 degrees and mostly cloudy..."
```

If the user is using Cortana on a device that has a screen, she also displays a card with additional information on her canvas.

![Weather Card](./media/images/weather-card.png)

If a user wants to invoke a custom skill, they speak an invocation phrase using the skill's invocation name. For example, if a user wants to use the "Northwind Photo" skill to check the status of an order and make a change, the conversation might go something like this:

```
User: "Ask Northwind Photo what the status of my order of cat photos is."
Cortana: "Your order of cat photos will be ready in an hour. Can I help you with anything else?"
User: "What did I order?"
Cortana: "3 copies of prints on glossy paper. Would you like to make a change?"
User: "Make it matte paper."
Cortana: "You would like to change the paper to matte. Is this correct?"
User: "Yes"
Cortana: "Your order has been updated."
```

Take a look at the following design guides to create engaging user experiences:

* [Skill design principles](./design-principles.md)
* [Invocation name guidelines](./cortana-invocation-guidelines.md)
* [Performance guidelines](./performance-guidelines.md)
* [Publishing review guidelines](./skill-review-guidelines.md)
* [Maintaining Cortana's persona](./cortanas-persona.md)


## Personalize the user's experiences using user insights

With permission, Cortana can send your skill the user's profile and contextual information, which you can use to personalize the user's experience. User profile information is data that Cortana knows about the user, such as their name and email address. Contextual information is data that may change more frequently, such as their current location and cuisine preference. For information about how Cortana passes the user's data to your skill when she invokes it, see [Get user profile and contextual information](./get-user-profile-context.md).

## Add intelligence to your skill using Microsoft Cognitive Services

Microsoft Cognitive Services lets you tap into a growing collection of powerful AI algorithms developed by experts in the fields of computer vision, speech, natural language processing, knowledge extraction, and web search. The services simplify a variety of AI-based tasks, giving you a quick way to add state-of-the-art intelligence technologies to your bots with just a few lines of code.

Intelligent skills respond as if they can see the world as people see it. They discover information and extract knowledge from different sources to provide useful answers, and, best of all, they learn as they acquire more experience to continuously improve their capabilities.

For the full list of services that you can integrate into your skill, see [Add intelligence to bots with Cognitive Services](https://docs.microsoft.com/bot-framework/cognitive-services-bot-intelligence-overview).

## Natural language understanding

Interactions between users and skills is mostly free-form, so skills need to understand language naturally and contextually. Skills determine what a user wants to do by identifying their intent from spoken or textual input, or utterances. The intent maps utterances to actions that the skill takes, such as invoking a dialog. A skill may also need to extract entities, which are important words in utterances.

You could use a simple method such as using regular expressions to inspect the content of a message and determine intent, but you're encouraged to use [Language Understanding Intelligent Service (LUIS)](https://luis.ai). LUIS is a powerful tool that processes natural language using pre-built or custom-trained language models. LUIS uses the models to determine what users want, identifies concepts and entities in a given sentence, and ultimately allows your skill to respond with the appropriate action.

Depending on the Bot Framework SDK that you use, for information about recognizing intents and entities with LUIS, see [Using LUIS with the Node.js SDK](https://docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-recognize-intent-luis) or [Using LUIS with the .NET SDK](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-luis-dialogs).

For information about modeling intents and entities in LUIS, see [intents](https://www.microsoft.com/cognitive-services/en-us/LUIS-api/documentation/Add-intents) and [entities](https://www.microsoft.com/cognitive-services/en-us/LUIS-api/documentation/Add-entities).

## Platform requirements

Cortana can run skills on any platform that Cortana runs on. Cortana is available on Windows, Android, and iOS platforms.

|Platform|Requirements
|-|-
|Windows|Windows 10 or later.
|iOS|iPhone, iPad, or iPod Touch running iOS 9.0 or later.<br /><br />The Cortana for iOS client must be version 1.9.15 or later.
|Android|An Android phone running Android 4.4 or later.<br /><br />The Cortana for Android client must be version 2.1.6.1547 or later.

## Next steps

Ready to create a skill? For details about creating your first skill, see [Get started](./get-started.md).

For answers to commonly asked questions, see [FAQ](./faq.md).
