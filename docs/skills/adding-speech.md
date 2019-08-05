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
The Cortana channel will speak the message or response sent from the skill to the channel if the `speak` property is set on the message (and the conversation turn was triggered by voice input).
Bot Service bots do not speak by default, so you need to make minor modifications to get Cortana to speak.

## Add Speech to Bot Service (V4) bots

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
or [JavaScript](https://docs.microsoft.com/JavaScript/api/botbuilder-core/turncontext#sendactivity).

## Add Speech to Bot Framework (V3) bots

```csharp
   Activity message = activity.CreateReply("This is displayed");
   message.Speak = "This is spoken";
   message.InputHint = InputHints.ExpectingInput;
   await context.PostAsync(message); // or connector.Conversations.ReplyToActivityAsync(message);
```
OR
```csharp
   await context.SayAsync( "This is displayed", "This is spoken" );
```
> [!NOTE]
> `SayAsync` has been deprecated in V4 of Bot Service: use the optional named arguments for `SendActivityAsync`.
> 

Find the Botframework V3 reference documentation here: [C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.sendtoconversationasync?view=botbuilder-dotnet-3.0)
or [JavaScript](https://docs.botframework.com/node/builder/chat-reference/modules/_botbuilder_d_.html).
You can find how-to documentation on adding speech in the [Add speech to messages](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-text-to-speech?view=azure-bot-service-3.0) page.

## Input Hints

Cortana requires a hint as to whether or not to open the microphone to have a conversation. The resulting behavior depends on the type of device. A device with a screen (like a Windows 10 device) behaves differently from a headless device (like an Invoke speaker).

| Hint | Has Display | No Display |
| --- | --- | --- |
| `acceptingInput` (default)| Passively waits for input on the conversation by Search Box or mic button click. | Closes the conversation. |
| `expectingInput` | Opens the mic and actively waits for input. Timeout closes mic and Cortana passively waits for input. | Reprompts once before closing the conversation |
| `ignoringInput`| Proceeds to the next turn (until reaching a turn specifies expecting or accepting input). | Proceeds to the next turn. |

Use `deviceInfo` to modify your skill's behavior based on device type, documented in the [Determine Cortana's device type](https://docs.microsoft.com/cortana/skills/cortana-device-type) section.

You can find how-to documentation on specifying input hints in the [Add input hints to messages](https://docs.microsoft.com/azure/bot-service/dotnet/bot-builder-dotnet-add-input-hints?view=azure-bot-service-3.0) page.

## More control over Cortana's speaking voice

If Cortana's standard speaking voice doesn't meet your needs, you can specify exactly how she reads your text. Cortana supports Speech Synthesis Markup Language (SSML), an XML-based markup language used to specify how she speaks text. Using SSML improves the quality of synthesized content over sending Cortana plain text. See [Speech Synthesis Markup Language (SSML) reference](../skills/speech-synthesis-markup-language.md) for more details.