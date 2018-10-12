---
title: Overview of Cortana Skills - Cortana skills design and development
description: Provides an overview of Cortana Skills Kit and how you can use it to extend Cortana so your users can use Cortana to interact with your service.

ms.assetid: 6dad0848-3886-4729-90fa-0bcd424b3561
ms.date: 10/12/2018
ms.topic: article

keywords: cortana
---

# Cortana Skills Kit

>[!NOTE]
> Cortana Skills Kit is currently in public preview.  

Cortana is a digital assistant that keeps users informed and productive, helping them get things done across devices and platforSkills define the tasks that Cortana can accomplish. Cortana invokes the skills based on spoken input from the user. You can extend Cortana by adding your own skills that let your users use Cortana to interact with your service.

To extend Cortana, use the Cortana Skills Kit. The kit is a suite of tools that help you build skills that connect users to your custom services and solutions. 

The following components make up the skills kit.  

*   [Bot Framework](https://docs.microsoft.com/bot-framework/)  
    A skill is a speech bot. Use the Bot Framework to build your speech bot, register it, and define your Cortana channel. The framework provides a .NET SDK and Node.js SDK that you use to build your bot. The Bot Framework SDKs provide features such as dialogs and built-in prompts that make interacting with users much simpler.  
    For more information about the Bot Builder SDK is provided as open source on GitHub, visit the [BotBuilder](https://github.com/Microsoft/BotBuilder) page.  
    
    >[!TIP]
    >For an overview of how the framework works, vist the [How the Bot Framework works](https://docs.microsoft.com/azure/bot-service/bot-service-overview-readme?view=azure-bot-service-3.0) page.  
    
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
> For more information about invocation phrases, visit the [Invocation Name Guidelines](./cortana-invocation-guidelines.md) page. 

If an invocation name is not provided, then Cortana suggests a skill to the user in order to fulfill the user request.

Users invoke skills on any platform that includes Cortana. 

>[!TIP]
> For a list of platforms, visit the [Platform Requirements](#Platform-requirements) section.

>[!TIP]
> For more information about the locales for invoking, visit the[Supported locales](./supported-locales.md) page.  

>[!IMPORTANT]
> Cortana supports skills in the en-US locale only.  

## How do users interact with skills?  

When a user invokes your Cortana Skill, Cortana sends a structured request to the service that powers your Cortana Skill and waits for a response. There are two ways that Cortana listens for requests. The first is when the user presses the microphone button in the Cortana app or in the `Ask me anything` search box in Windows. The second is when the user enables Cortana to respond to `Hey Cortana`. The following are examples of how users might interact with Cortana.  

>[!NOTE]
> If a user asks Cortana about the weather, then Cortana triggers the built-in weather skill.  
>
>```
>User: "What is the weather like?"
>Cortana: "It is currently 58 degrees and mostly cloudy..."
>```  

>[!NOTE]
> If the user invokes a Cortana Skill on a device with a screen, then a card with additional information on the Cortana Canvas.  
>
> ![Weather Card](./media/images/weather-card.png)  

>[!NOTE]
> If a user is trying to invoke your Cortana Skill, then the user speaks an invocation phrase using the invocation name.  

>[!NOTE]
> If a user invokes the Cortana Skill named `Contoso Photo` to check the status of an order and make a change, then the following conversation may happen.  
>
> ```
> User: "Ask Contoso Photo what the status of my order of cat photos is."
> Cortana: "Your order of cat photos will be ready in an hour."  
> Cortana: "Can I help you with anything else?"
> User: "What did I order?"
> Cortana: "3 copies of prints on glossy paper. Would you like to make a change?"
> User: "Make it matte paper."
> Cortana: "You would like to change the paper to matte. Is this correct?"
> User: "Yes"
> Cortana: "Your order has been updated."
> ```  

Take a look at the following design guides to create engaging user experiences.  

* [Skill design principles](./design-principles.md)  
* [Invocation name guidelines](./cortana-invocation-guidelines.md)  
* [Performance guidelines](./performance-guidelines.md)  
* [Publishing review guidelines](./skill-review-guidelines.md)  
* [Maintaining Your Cortana persona](./cortanas-persona.md) 

## Personalize the user experiences using user insights  

With permission, Cortana provides the user profile and contextual information, which you use to personalize the user experience. User profile information is data that Cortana knows about the user, such as name and email address. Contextual information is data that may change more frequently, such as current location and cuisine preference of the user.  

>[!TIP]
> For more information about how Cortana passes the user data, visit the [Get user profile and contextual information](./get-user-profile-context.md) page.  

## Add intelligence to your skill using Microsoft Cognitive Services  

Microsoft Cognitive Services taps into a growing collection of powerful AI algorithms developed by experts in the fields of computer vision, speech, natural language processing, knowledge extraction, and web search. The services simplify a variety of AI-based tasks, providing you a quick way to add state-of-the-art intelligence technologies to your bot with just a few lines of code.  

An intelligently-designed Cortana Skill responds like a person who sees the world as people see it. Your Cortana Skill discovers information and extracts knowledge from different sources to provide useful answers. Best of all, Your Cortana Skill learns by acquiring more experience and continuously improves the capabilities.  

>[!TIP]
> For the full list of services that you may integrate, visit the [Add intelligence to bots with Cognitive Services](https://docs.microsoft.com/azure/bot-service/bot-service-concept-intelligence?view=azure-bot-service-3.0) page.  

## Natural Language Understanding  

Interactions between a user and your Cortana Skill is mostly free-form, so Cortana must understand language naturally and contextually. You Cortana Skill determines what a user wants to do by identifying the user intent from spoken or textual input or utterances. The intent maps utterances to actions that your Cortana Skill takes, such as invoking a dialog. Your Cortan Skill may extract entities, which are important words in utterances.  

You could use a simple method such as using regular expressions to inspect the content of a message and determine intent, but you are encouraged to use [Language Understanding Intelligent Service (LUIS)](https://luis.ai). LUIS is a powerful tool that processes natural language using pre-built or custom-trained language models. LUIS uses the models to determine what users want, identifies concepts and entities in a given sentence, and ultimately allows your Cortana Skill to respond with the appropriate action.  

Depending on the Bot Framework SDK that you use.  

>[!TIP]
> For information about recognizing intents and entities with LUIS, visit the  [Using LUIS with the Node.js SDK](https://docs.microsoft.com/azure/bot-service/nodejs/bot-builder-nodejs-recognize-intent-luis?view=azure-bot-service-3.0) or [Using LUIS with the .NET SDK](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-luis-dialogs?view=azure-bot-service-3.0) page.  

>[!TIP]
> For information about modeling intents and entities in LUIS, visit the  [Manage intents](https://docs.microsoft.com/azure/cognitive-services/luis/luis-how-to-add-intents) and [Manage entities](https://docs.microsoft.com/azure/cognitive-services/luis/luis-how-to-add-entities) pages.  

## Platform requirements  

Run Cortana Skills on any platform that supports Cortana. Cortana is available on Windows, Android, and iOS platforms.  

>[!IMPORTANT]
> The Cortana for iOS client must be version 1.9.15 or newer.  
> The Cortana for Android client must be version 2.1.6.1547 or newer.  

| Platform | Requirements |  
|:--- |:--- |  
| Windows | Windows 10 or newer. |  
| iOS | iPhone, iPad, or iPod Touch running iOS 9.0 or newer. |  
|Android | Android phone running Android 4.4 or newer. |  

## Next steps  

Get ready to create you Cortana Skill.  

>[!TIP]
> For details about creating your first skill, visit the [Create Your First Skill](./get-started.md) page.  

>[!TIP]
> For answers to commonly asked questions, visit the [Cortana Skills Kit FAQ](./faq.md) page.  
