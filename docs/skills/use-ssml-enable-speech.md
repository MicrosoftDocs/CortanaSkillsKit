---
redirect_url: /cortana/skills/speech-synthesis-markup-language
---



<!-- This needs to go away - need to point to framework content -->

<!--
# Use Speech Synthesis Markup Language (SSML) to enable your skill to speak

With the latest BotBuilder SDK, new features were added to support speech based channels such as Cortana. If you have an existing bot, update the BotBuilder library to this latest version. For examples of using speech with cards, take a look at the [Card Design Best Practices](../../design-guides/card-design-best-practices.md)

>[!Note]
> Currently Cortana does not support proactive notifications. As such your bot can’t initiate the conversation, only the user can by invoking your skill using an invocation phrase such as "Ask &lt;invocation name&gt; to do something…".

## Input Hints

One of the new additions to the BotBuilder SDK is the `InputHints` enumeration which is used to specify whether a bot is accepting, expecting, or ignoring input. The `InputHints` enumeration provides the following values.

| Name           | String Value | Description  |
|--------------------|------------------|------------------|
| **AcceptingInput** | acceptingInput   | Your bot is passively ready for input but is not waiting on a response.  |
| **ExpectingInput** | expectingInput   | Your bot is actively expecting a response from the user. |
| **IgnoringInput**  | ignoringInput    | Your bot is ignoring input. Bots may send this hint if they are actively processing a request and will ignore input from users until the request is complete. |

If you do not specify input hints in your bot, it will automatically select the one depending on the response. Prompts for instance will be expecting input, while a standard text response may be set to accept input.

>[!Tip]
> Cortana uses a turn-based model. You can send multiple replies as a response to a single user invocation, as long as the first N-1 replies has an input hint of **IgnoringInput**. The last reply must have an input hint of **ExpectingInput** (which automatically turns the microphone on), or **AcceptingInput** (which doesn’t).

## Add Speech in the BotBuilder Node.js SDK

The `session` class in version 3.8 and above of the Node.js BotBuilder SDK (`npm install –save botbuilder@next`) has a new `session.say()` method which allows you to specify the speech output. Here is the format of this method:

> `session.say(displayText: string, speechText: string, options?: object)`

The following information can be passed into the `session.say()` method.

| Property    | Type | Description  |
|-----------------|----------|------------------|
| **displayText** | string   | The text that is displayed at the top of Cortana’s canvas.|
| **speechText**  | string   | The text or [SSML](../../reference/ssml.md) that Cortana will read out to the user.|
| **options**     | object   | An object containing an attachment or input hint. Input hints indicate whether the bot is accepting, expecting, or ignoring input. Card attachments are displayed in Cortana’s canvas below the displayText information. Currently Cortana supports the following Bot Framework cards: Hero Card, Thumbnail Card, Receipt Card, Sign-In Card. |

In addition to using the new `session.say()` method you can also pass in text or SSML into built-in prompts using two new `speak` & `retrySpeak` options.

```javascript
builder.Prompts.text(session, 'text based prompt', {
    speak: 'This is the text that will be spoken by Cortana.'
});
```

>[!Tip]
> If you use waterfalls and the built-in prompts, input hints are taken care of for you automatically. 

Here are some examples of how to use the new `session.say()` method.

**Have plain text read by Cortana**

```javascript
session.say('Hello World', 'This is the text that will be spoken by Cortana.');
```

**Have SSML read by Cortana**

```javascript
session.say('Hello World', '<speak version="1.0" xmlns="http://www.w3.org/2001/10/synthesis" xml:lang="en-US">This is the text that will be spoken by Cortana.</speak>');
```

**Add an InputHint to let Cortana know to expect user input**

```javascript
session.say('Hi there', 'Hi, what’s your name?', {
    inputHint: builder.InputHint.expectingInput
});
```

### Prompts

In addition to the `session.say()` method, you can also add speech to your bot by using the new `speak` and `retrySpeak` options in built-in prompts. Both options support plain text as well as SSML. Input hints are also supported. For example:

```javascript
builder.Prompts.text(session, 'text based prompt', {                                    
    speak: 'Cortana reads this out initially',                                               
    retrySpeak: 'This message is repeated by Cortana after waiting a while for user input',  
    inputHint: builder.InputHint.expectingInput                                              
});
```

>[!Tip]
> There are several useful SSML libraries available through [npm](https://www.npmjs.com/search?q=ssml) which make it easy to create well formatted SSML.

## Add Speech in the BotBuilder .NET SDK

The latest version of the .NET BotBuilder SDK ([Version 3.5.8 or above](https://www.nuget.org/packages/Microsoft.Bot.Builder)) adds support for speech responses in the `IMessageActivity`. The `IMessageActivity` class has had two new properties added to it; `Speak` and `InputHint`.

| Property  | Type | Description                                                       |
|---------------|----------|-----------------------------------------------------------------------|
| **InputHint** | string   | Indicates whether the bot is accepting, expecting, or ignoring input. |
| **Speak**     | string   | The text or [SSML](../../reference/ssml.md) that Cortana will read out to the user. |

Here are some examples of how to add a speech response for Cortana to read.

**Have plain text read by Cortana**

```csharp
Activity reply = activity.CreateReply("Cortana will display this in her canvas."); 
reply.Speak = "This is the text that will be spoken by Cortana.";
```

**Have SSML read by Cortana**

```csharp
Activity reply = activity.CreateReply("Cortana will display this in her canvas.");
reply.Speak = "<speak version=\"1.0\" xmlns=\"http://www.w3.org/2001/10/synthesis\" xml:lang=\"en-US\">This is the text that will be spoken by Cortana.</speak>";
```

**Add an InputHint to let Cortana know to expect user input**

```csharp
Activity reply = activity.CreateReply("Hi there"); 
reply.Speak = "Hi, what’s your name?.";             
reply.InputHint = InputHints.ExpectingInput;
```

>[!Tip]
> To help ensure that your SSML is correctly formatted, use an XML library.

## Context.SayAsync

In addition to adding speach using the `Speak` property of an activity, you can also use the `SayAsync` method of the context. Here is the format of this method:

> `context.SayAsync(string text, string speak, MessageOptions options, string locale, CancellationToken cancellationToken)`

The following information can be passed into the `session.say()` method.

| Property    | Type | Description |
|-------------|------|-------------|
| **text**    | string | The text that is displayed at the top of Cortana’s canvas. |
| **speak**    | string | The text or [SSML](../../reference/ssml.md) that Cortana will read out to the user. |
| **options**    | MessageOptions | The options for the message. |
| **locale**    | string | The locale of the text. |
| **cancellationToken**    | CancellationToken | A cancellation token.  |

Here is an example using the SayAsync method to display the text "This is displayed" and to have Cortana speak "This is spoken".

```csharp
await context.SayAsync($"This is displayed", $"This is spoken");
context.Wait(MessageReceivedAsync);
```

### Prompts

Prompts also support speech options as well. Prompts also support specifying a `retrySpeak` property which is what Cortana will say when the user hasn't responded with a valid response to the prompt.

```csharp
var promptOptions = new PromptOptionsWithSynonyms<string>("Pick a number between 1 and 4",
    retry: "Didn't get that!",
    choices: new Dictionary<string, IReadOnlyList<string>>()
    {
        { "1", new List<string> { "one", "1" } },
        { "2", new List<string> { "two", "to", "too", "2" } },
        { "3", new List<string> { "three", "tree", "3" } },
        { "4", new List<string> { "four", "for", "fore", "4" } }
    },
    speak: "Pick a number between 1 and 4",
    retrySpeak: "Didn't get that!");

PromptDialog.Choice(context, this.NumberChoiceReceivedAsync, choices, "Pick a number between 1 and 4", );
```

Here is how this is prompt looks in Cortana's canvas.

![Card Prompt](../../images/design-guides/cards/cards-prompt.png)

## Ending a Conversation

When the user has reached the end of the work flow in your skill, or if the user asks to exit the skill, you can gracefully end the conversation. In the Node.js BotBuilder SDK the `session` object has a simple method called `endConversation` which will end the conversation and set the response code to *completedSuccessfully*. Here is how you can use this method.

```json
session.endConversation();
```

With the .NET BotBuilder SDK create a `EndOfConversationActivity` and marking the response code as *CompletedSuccessfully*. This activity is then sent to the back to Cortana and `Done` method of themcontext is called to close the session.

```csharp
var exitReply = activity.CreateReply();
exitReply.Type = ActivityTypes.EndOfConversation;
exitReply.Code = EndOfConversationCodes.CompletedSuccessfully;
exitReply.AsEndOfConversationActivity();
await context.PostAsync(exitReply);

context.Done<object>(null);
```

## Next Up

[Actions, ChannelData and Entity Information](bot-entity-channel-data.md)

-->