---
title: Add speech
description: Learn how to add speech to your bot-based skill.
label: Conceptual
ms.assetid: 
ms.date: 12/27/2018
ms.topic: article

keywords: cortana
---
# Add speech to your Cortana skill #
The Cortana channel will speak the message or response sent from the skill to the channel if the _speak_ property is set on the message.
Bot Service bots do not speak by default, so you need to make minor modifications to get Cortana to speak!



## Add Speech to Bot Service (V4) bots ##

On a `turn` you have two forms of `sendActivityAsync`: the first method takes an activity (message), and the second takes optional named
arguments `speak` and `inputHint`.

```csharp
   var message = turnContext.Activity.CreateReply();
   message.Text = "This is displayed";
   message.Speak = "This is spoken";
   message.InputHint = "expectingInput";
   await turnContext.SendActivityAsync(message);
```
OR
```csharp
   await turnContext.SendActivityAsync( "This is displayed", speak: "This is spoken", inputHint: "expectingInput" );
```

Find the Bot Service V4 reference documentation here: [C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.builder.iturncontext.sendactivityasync)
or [javascript](https://docs.microsoft.com/javascript/api/botbuilder-core/turncontext#sendactivity).

## Add Speech to Bot Framework (V3) bots ##

```csharp
   Activity message = activity.CreateReply("This is displayed");
   message.Speak = "This is spoken";
   message.InputHint = InputHints.ExpectingInput;
   await context.PostAsync(message); // or connector.Conversations.ReplyToActivityAsync(message);
```
OR
```csharp
   await context.SayAsync(text: "This is displayed", "This is spoken");
```
> [!NOTE]
> `SayAsync` has been deprecated in V4 of Bot Service: use the optional, named arguments for `SendActivityAsync`.
> 

Find the Botframework V3 reference documentation here: [C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.sendtoconversationasync?view=botbuilder-dotnet-3.0)
or [javascript](https://docs.botframework.com/node/builder/chat-reference/modules/_botbuilder_d_.html).
You can find how-to documentation [on adding speech here](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-text-to-speech?view=azure-bot-service-3.0).

## Input Hints ##
Cortana requires a hint as to whether or not to open the mic to have a conversation. The resulting behavior depends on the type of device (for example, a device with a screen like a Windows 10 device or a headless device like an Invoke speaker.)

| Hint | Has Display | No Display |
| --- | --- | --- |
| `acceptingInput` (default)| Passively waits for input on the conversation. | Closes the conversation. |
| `expectingDefault` | Opens the mic and actively waits for input. Timeout closes mic and Cortana passively waits for input. | Reprompts once before closing the conversation |
| `ignoringInput`| Proceeds to the next step (until a turn uses expecting or accepting input). | Closes the conversation. |

> [!NOTE]
> You can modify your skills behavior based on device type by looking at `deviceInfo` documented [here](https://docs.microsoft.com/cortana/skills/cortana-device-type).
> 

You can find how-to documentation [on specifying input hints here](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-add-input-hints?view=azure-bot-service-3.0).
