---
title: Overview of Cortana Skills - Cortana skills design and development
description: Provides an overview of Cortana Skills Kit and how you can use it to extend Cortana so your users can use Cortana to interact with your service.

ms.assetid: 6dad0848-3886-4729-90fa-0bcd424b3561
ms.date: 10/12/2018
ms.topic: article

keywords: cortana
---

# Cortana Skills Kit

>[!IMPORTANT]
> Cortana Skills Kit is currently in public preview.  

Cortana is a personal digital assistant that keeps users informed and productive, helping them get things done across devices and platforms. Skills define the tasks that Cortana can accomplish. You can extend Cortana by adding your own skills that let your users interact with your service via Cortana. Cortana invokes the skills based on input from the user, either spoken or typed.

The Cortana Skills Kit enables you to develop skills for Cortana. The kit is a suite of tools that will help you build skills that connect users to your custom services and solutions. 

The following components make up the Skills Kit.  

*   [Bot Framework](https://docs.microsoft.com/bot-framework)  
    A skill is a speech bot. Use the Bot Builder to build your bot, register it, and define your Cortana channel. The framework provides a .NET SDK and Node.js SDK that you use to build your bot. The Bot Framework SDKs provide features such as dialogs and built-in prompts that make interacting with users much simpler.  
    
    For links to both the .NET and JavaScript SDKs, read The Bot Builder SDK is provided as an open source repository: [BotBuilder on GitHub](https://github.com/microsoft/botbuilder-v3)
    
    >[!TIP]
    > This is an overview of the bot framework: [How the Bot Framework works](https://docs.microsoft.com/azure/bot-service/bot-service-overview-readme?view=azure-bot-service-3.0)  
    
*   [My Bot List Configured for Cortana](https://dev.botframework.com/bots?c=cortana)  
    View the list of bots that you configured for Cortana. Create new bots.  

Because Cortana is available on many different devices, some may have a screen while others may be a standalone speaker. You should ensure that your bot is capable of handling both scenarios. The bot framework provides device information as an entity of the activity.  

The following image shows how users interact with Cortana and your skill.  

![Cortana Skills workflow](./media/images/workflow.png)  

## How do users invoke skills?  

Users invoke skills simply by speaking to Cortana. Users don't install or activate skills.  

<!-- I'm confused by "don't install or activate" because there's this site where they can discover new skills: https://www.microsoft.com/en-us/windows/cortana/cortana-skills/. And in Cortana Notebook there's Skills, which they use to "manage and control what skills you've connected to."-->

Users invoke skills by speaking or typing to Cortana, optionally by providing an **invocation phrase**. The invocation phrase includes an **invocation name**, which uniquely identifies the skill to invoke.  
For example, if an invocation name is `Contoso Photo`, the user might say `Ask Contoso Photo to...` or `Tell Contoso Photo that...`. You specify the name when you configure the Cortana channel for your skill.  

>[!TIP]
> For more information about invocation phrases, visit the [Invocation Name Guidelines](https://docs.microsoft.com/en-us/cortana/skills/cortana-invocation-guidelines) page.

If an invocation name is not provided, then Cortana suggests a skill to the user in order to fulfill the user request.

Users invoke skills on any platform that includes Cortana.

>[!TIP]
> For a list of platforms, visit the [Platform Requirements](#Platform-requirements) section.

>[!TIP]
> For more information about the locales for invoking, visit the[Supported locales](./supported-locales.md) page.  

>[!IMPORTANT]
> Cortana supports skills in the en-US locale only.  

## How do users interact with skills?  

When a user invokes your Cortana skill, Cortana sends a structured request to the service that powers your Cortana skill and waits for a response. There are two ways that Cortana listens for requests. The first is when the user presses the microphone button in the Cortana app or in the `Ask me anything` search box in Windows. The second is when the user enables Cortana to respond to `Hey Cortana`. The following are examples of how users might interact with Cortana.  

### EXAMPLE 1
> If a user asks Cortana about the weather, then Cortana triggers the built-in weather skill. 
> Here's a sample dialogue:
>```
>User: "What is the weather like?"
>Cortana: "It is currently 58 degrees and mostly cloudy."
>```  

### EXAMPLE 2
> If the user invokes a Cortana skill on a device with a screen, then a card with additional information will be displayed on the Cortana Canvas. For example, this card might be displayed when Cortana answers the previous weather question:
>
> ![Weather Card](./media/images/weather-card.png)  

### EXAMPLE 3
> If a user is trying to invoke your Cortana skill by voice input, they speak an invocation phrase using the invocation name. For example, if a user invokes the Cortana skill `Contoso Photo` to check on the status of an order and make a change, then the conversation that follows might go like this sample.  
>
> ```
> User: "Ask Contoso Photo what the status of my order of cat photos is."
> Cortana: "Your order of cat photos will be ready in an hour."  
> Cortana: "Can I help you with anything else?"
> User: "What did I order?"
> Cortana: "3 copies of prints on glossy paper. Would you like to make a change?"
> User: "Make it matte paper."
> Cortana: "You would like to change the paper to matte. Is this correct?"
> User: "Yes."
> Cortana: "Your order has been updated."
> ```  

There are design guides available to help you create engaging user experiences.  

* [Skill design principles](./design-principles.md)  
* [Invocation name guidelines](./cortana-invocation-guidelines.md)  
* [Performance guidelines](./performance-guidelines.md)  
* [Publishing review guidelines](./skill-review-guidelines.md)  
* [Maintaining Your Cortana persona](./cortanas-persona.md) 

## Personalize the user experiences using user insights  

If the user gives permission, Cortana will provide the user profile and contextual information when invoking your skill, which you can use to personalize their user experience. User profile information is data that Cortana knows about the user, such as their name or email address. Contextual information is data that may change more frequently, such as the user's current location.

>[!TIP]
> For more information about how Cortana passes the user data, visit the [Get user profile and contextual information](./get-user-profile-context.md) page.  

## Add intelligence to your skill using Microsoft Cognitive Services  

Microsoft Cognitive Services taps into a growing collection of powerful AI algorithms developed by experts in the fields of computer vision, speech, natural language processing, knowledge extraction, and web search. The services simplify a variety of AI-based tasks, providing you a quick way to add state-of-the-art intelligence technologies to your bot with just a few lines of code.  

A well-designed Cortana skill that uses these technologies will respond like a person who sees the world as people see it. Your Cortana skill will discover information and extract knowledge from different sources to provide useful answers. Best of all, your Cortana skill will learn by experience, and will continuously improve its capabilities.  

> For the full list of Microsoft Cognitive Services that you may integrate, visit the [Add intelligence to bots with Cognitive Services](https://docs.microsoft.com/azure/bot-service/bot-service-concept-intelligence?view=azure-bot-service-3.0) page.  

## Natural language understanding

Interactions between a user and your Cortana skill are mostly free-form, so Cortana must understand language naturally and in context. You Cortana skill determines what a user wants to do by identifying the user intent from spoken or textual input (an utterance). The intent maps utterances to actions that your Cortana skill can take, such as invoking a dialog. Your Cortana skill may also extract entities, which are important words in utterances.

You could use a simple method such as using regular expressions to inspect the content of a message and determine intent, but we encourage you to use [Language Understanding Intelligent Service (LUIS)](https://www.luis.ai). LUIS is a powerful natural language processing tool that  uses pre-built or custom-trained language models to evaluate user input. LUIS can determine what users want (intent) and identify concepts and entities in a given sentence. Ultimately, this allows your Cortana skill to respond with the appropriate action.

> For information about recognizing intents and entities with LUIS, visit the  [Using LUIS with the Node.js SDK](https://docs.microsoft.com/azure/bot-service/nodejs/bot-builder-nodejs-recognize-intent-luis?view=azure-bot-service-3.0) or [Using LUIS with the .NET SDK](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-luis-dialogs?view=azure-bot-service-3.0) page, depending on the Bot Framework SDK that you use.

>[!NOTE]
> For information about modeling intents and entities in LUIS, visit the  [Manage intents](https://docs.microsoft.com/azure/cognitive-services/luis/luis-how-to-add-intents) and [Manage entities](https://docs.microsoft.com/azure/cognitive-services/luis/luis-how-to-add-entities) pages.  

## Platform requirements  

Cortana skills run on any platform that supports Cortana (Windows, Android, and iOS).

| Platform | Requirements |  
|:--- |:--- |  
| Windows | Windows 10 or newer. |  
|Android | Android phone running Android 4.4 or newer, with app version 2.1.6.1547 or newer. |  
| iOS | iPhone, iPad, or iPod Touch running iOS 9.0 or newer, with app version 1.9.15 or newer. |  

## Next steps  

Get ready to create your Cortana skill! Visit the [Create Your First Cortana Skill](./get-started.md) page.  

## FAQ
For answers to commonly asked questions, visit the [Cortana Skills Kit FAQ](./faq.md) page.  
