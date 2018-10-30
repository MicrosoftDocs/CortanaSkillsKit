---
title: Using Adaptive Cards in your skill
description: Learn how to use Adaptive Cards in your bot-based skill.
label: Conceptual

ms.assetid: A7CD987E-5DD1-42EA-A436-49D4E8327365
ms.date: 10/08/2018
ms.topic: article

keywords: cortana
---

# Use Adaptive Cards in Your Cortana Skill

Cards are interface elements that you may use to enhance the user experience in your Cortana skill.  
The most versatile card is an Adaptive Card. An Adaptive Card is a customizable card that includes any combination of text, speech, images, buttons, and input fields.  

## Adaptive Cards  

Adaptive Cards provide the following options.  

*   **Input controls** : Add input controls for text, date, number, time, toggle switch, and choice set.  
*   **Richer text** : Text in your card is not limited to title, subtitle, and text fixed formats. Use a variety of font sizes, formats, and colors.  
*   **A single open card exchange format** : Use your existing cards in a common and consistent way and extend your cards with rich controls using a common schema.  

Adaptive Cards use an open card exchange format. The open card exchange format enables you to specify user interface content in your skill in a common and consistent way. You describe the content as a simple JSON object. The JSON content is natively displayed by the skill and automatically adapts to the look and feel of your skill.  

Adaptive Cards include elements, containers, actions, and inputs.  
A basic Adaptive Card includes the following items.   
*   The Adaptive Card root object.  
*   The Adaptive Card body, which includes the elements of your card.  
*   Any actions for your Adaptive Card, which are typically displayed in an action bar at the bottom of your card.  

## Adaptive Cards Designer  

The Adaptive Cards Designer provides an interactive card builder where you can see the resulting card JSON.

*   [adaptivecards.io/designer](https://adaptivecards.io/designer)
*   [adaptivecards.io/visualizer](https://adaptivecards.io/visualizer)

>[!TIP]
> # The speak object of an Adaptive Card needs to be copied to the Message for Cortana to speak the text.
> # The speak object > text needs to be wrapped in SSML `speak` tags._


 The following text block provides the title text for the sample card in the Adaptive Cards Visualizer.
 
 ```json
 "type": "TextBlock",
 "text": "Publish Adaptive Card schema",
 "weight": "bolder",
 "size": "medium"
 ```
 
 ![Sample Card](./media/images/ac_visualizer1.png)  
 
 Change the titles text using the following text to updated the text block.  
 
 ```json
 "type": "TextBlock",
 "text": "This is a test",
 "weight": "bolder",
 "size": "medium"
 ```  

 ![Revised Card](./media/images/ac_visualizer2.png)  

## Create an Adaptive Card using .NET

1.  Install the `AdaptiveCards` NuGet package.
2.  Specify the elements of your card in code.
3.  Add the card to your Cortana skill as an attachment.

>[!TIP]
> The following code adds an Adaptive Card to a Cortana skill response.
>
> ```csharp
> var response = context.MakeMessage();
>
> AdaptiveCard card = new AdaptiveCard();
>
> card.Body.Add(new AdaptiveTextBlock()
>     {
>         Text = "This is a test",
>         Weight = TextWeight.Bolder
>         Size = TextSize.Medium,
>     }
> );
>
> response.Attachments.Add(card.ToAttachment());
>
> await context.PostAsync(response);
> context.Wait(MessageReceived);
> ```  

## More Information  

*   For more information about Adaptive Cards, visit the Adaptive Cards page located at  [adaptivecards.io](https://adaptivecards.io).  
*   For more information about Bot Framework cards using .Net, visit the Add rich card attachments to messages for .NET page located at [docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0).
*   For more information about Bot Framework cards using Node.js, visit the Add rich card attachments to messages for Node.js page located at [docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards](https://docs.microsoft.com/azure/bot-service/nodejs/bot-builder-nodejs-send-rich-cards?view=azure-bot-service-3.0).
*   For an example of creating an Adaptive Card using .NET, visit the Add an Adaptive card to a message section located at [docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#adaptive-card](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0#adaptive-card).  
