---
title: Add speech
description: Learn how to add speech to your bot-based skill.
label: Conceptual

ms.date: 07/02/2019
ms.topic: article

keywords: cortana, speech
---

# Add speech to your Cortana skill

The Cortana channel will speak the message or response sent from the skill to the channel if the `speak` property is set on the message, and the conversation turn was triggered by voice input.

By default, Bot Service bots don't speak, so you need to make minor modifications to get your Cortana skill to speak.

## Add Speech to Bot Service (V4) bots

On a `turn` you have two forms of `sendActivityAsync`: the first method takes an activity (message), and the second takes optional named arguments `speak` and `inputHint`.

### First method

# [C#](#tab/cs2)

```csharp
   await turnContext.SendActivityAsync( "This is displayed", speak: "This is spoken", inputHint: "expectingInput" );
```

# [JavaScript](#tab/js2)

```javascript
await turnContext.sendActivity( 'This is displayed', 'This is spoken', 'expectingInput' );
```

---

### Second method

# [C#](#tab/cs1)

```csharp
   var message = turnContext.Activity.CreateReply();
   message.Text = "This is displayed";
   message.Speak = "This is spoken";
   message.InputHint = "expectingInput";
   await turnContext.SendActivityAsync(message);
```

# [JavaScript](#tab/js1)

```javascript
   let message = { text: 'This is displayed', speak: 'This is spoken', inputHint: 'expectingInput' };
   // or
   // let message = {};
   // message.speak = "speker";
   // message.text = "texter";
   // message.inputHint = "acceptingInput";
   //
   await turnContext.SendActivity(message);
```

---

The Bot Service V4 reference documentation is here: [C#](/dotnet/api/microsoft.bot.builder.iturncontext.sendactivityasync)
or [JavaScript](/JavaScript/api/botbuilder-core/turncontext#sendactivity).

## Input Hints

Cortana requires a hint as to whether or not to open the microphone to have a conversation. The resulting behavior depends on the type of device. A device with a screen (like a Windows 10 device) behaves differently from a headless device (like an Invoke speaker).

| Hint | With Display | No Display |
| --- | --- | --- |
| `acceptingInput` (default)| Passively waits for input on the conversation by Search Box or mic button click. | Closes the conversation. |
| `expectingInput` | Opens the mic and actively waits for input. Timeout closes mic and Cortana passively waits for input. | Reprompts once before closing the conversation |
| `ignoringInput`| Proceeds to the next turn (until reaching a turn specifies expecting or accepting input). | Proceeds to the next turn. |

Use `deviceInfo` to modify your skill's behavior based on device type, documented in the [Determine Cortana's device type](./cortana-device-type.md) section.

You can find how-to documentation on specifying input hints in the [Add input hints to messages](/azure/bot-service/dotnet/bot-builder-dotnet-add-input-hints?view=azure-bot-service-4.0) page.