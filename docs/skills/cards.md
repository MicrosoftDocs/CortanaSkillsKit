---
title: Using Bot Framework cards in a Cortana Skill
description: Identifies the different cards that you can use in your skill to display information to the user.
label: Conceptual

ms.date: 09/25/2018
ms.topic: article

keywords: cortana
--- 

# Using Bot Framework cards and adaptive cards


Although the goal is to design your skill for voice only, for some skills that's not practical. There are times when displaying visual elements to support the information that your skill speaks is required. For example, if the user asks for recipes, displaying pictures of the prepared food with links to the recipe can be a better experience than trying to describe each recipe with voice only. Visual elements should not be required to communicate the intent, they should only support the intent.

If you determine that your skill requires a user interface, Bot Framework supports the following types of cards with predefined formats.

| Card Type | Description | Supported layout 
|-|-|-
| Hero Card | A card with a single large image, title, text, and buttons. | Single or Carousel 
| Thumbnail Card | A card with a single small image, title, text, and buttons. | Single or Carousel 
| Receipt Card | A card that contains an invoice or receipt. | Single 
| SignIn Card | A card that lets the user sign-in to a service that the skill uses. | Single 


For information about adding these cards to your skill, see [Add cards to your skill using Node.js](https://docs.microsoft.com/azure/bot-service/nodejs/bot-builder-nodejs-send-rich-cards?view=azure-bot-service-3.0) or [Add cards to your skill using .NET](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0). 

In addition to cards, Node.js users can use a set of [built-in prompts](https://docs.microsoft.com/azure/bot-service/nodejs/bot-builder-nodejs-dialog-prompt?view=azure-bot-service-3.0) to simplify collecting inputs from a user. For example, you can use the `choice` prompt to present a list of choices that the user can pick from, or you can use the `confirm` prompt to confirm an action. For a list of prompts, see [Prompt types](https://docs.microsoft.com/azure/bot-service/nodejs/bot-builder-nodejs-dialog-prompt?view=azure-bot-service-3.0#prompt-types).

If these cards and prompts don't meet your needs, see [Adaptive Cards](https://docs.microsoft.com/en-us/adaptive-cards/). Adaptive cards are flexible, user-designed cards that contain only the UI elements that you want in the format you want. See the following adaptive card resources: 

- [Adaptive Cards for Bot developers](https://docs.microsoft.com/en-us/adaptive-cards/get-started/bots)&mdash;Provides information about using adaptive cards with bots. 
- [Platform SDKs](https://docs.microsoft.com/en-us/adaptive-cards/get-started/bots#platform-sdks)&mdash;Provides information about downloading the adaptive card SDKs for Node.js and .NET.
- [Adaptive card example using Node.js](https://docs.microsoft.com/azure/bot-service/nodejs/bot-builder-nodejs-send-rich-cards?view=azure-bot-service-3.0#send-an-adaptive-card)
- [Adaptive card example using .NET](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0#adaptive-card)
- [Schema explorer](https://adaptivecards.io/explorer/) and [Card schema](https://docs.microsoft.com/en-us/adaptive-cards/create/cardschema)&mdash;Provides details about the adaptive card schema.
- [Visualizer](https://adaptivecards.io/visualizer/)&mdash;Lets you see how your adaptive card renders as you're design it. 
- [AdaptiveCards.io](https://adaptivecards.io)&mdash;The adaptive card developer portal. 


## What happens if the user is using a speaker-only device

Some users use Cortana on speaker-only devices and can't see your cards. If the user needs to see a card, direct them to Cortana's companion app on their mobile device. However, try and do this sparingly. Ideally, a user should be able to use your skill on any supported device without having to use a secondary device. The exception being when the user has to sign-in to your skill or provide private information. Note that other than the sign-in card, cards are read-only on speaker devices.

If your skill incorporates or relies on UI elements, it may not be an appropriate skill to run on speaker-only devices. In this case, you should let the user know that your skill isn't supported on speak-only devices. To determine the type of device your skill is running on, see [Determine Cortana's device type](cortana-device-type.md).


## Next steps

For card design and usage considerations, see [Design your skill's visual elements](design-principles.md#design-your-skills-visual-elements).
