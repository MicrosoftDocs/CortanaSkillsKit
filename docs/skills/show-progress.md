---
title: Show the user you're working on their request 
description: For long running request, show the user that you're still working on their request.

ms.assetid: 23802F09-921E-4475-AD34-3A71C9078290
ms.date: 01/31/2019
ms.topic: article

keywords: cortana
---

# Show the user progress

It's important to keep the user informed while you're working on their request. If it takes longer than three seconds to fulfill the request, you should send a message letting them know that you're still working on it.

## C# example
This example uses the `ExecuteWithTimeoutHandler` method to notify the user if the request exceeds three seconds. The `ExecuteWithTimeoutHandler` method executes the default message handler for the specified number of milliseconds. If the method exceeds the limit, it executes the timeout handler, which sends a message to the user (for example, "Working on it...").

```csharp
        /// <summary>
        /// Executes the message handler for <var>millisecondsTimeout</var>. If the messageHandler exceeds this time, it executes the <var>timeoutHandler</var>
        /// </summary>
        /// <param name="millisecondsTimeout">Number of milliseconds before the timeoutHandler executes.</param>
        /// <param name="messageHandler">The default message handler</param>
        /// <param name="timeoutHandler">The timeout handler</param>
        /// <returns>Returns true if the <var>messageHandler</var> executed in time</returns>
        public static async Task<bool> ExecuteWithTimeoutHandler(int millisecondsTimeout, Action messageHandler, Action timeoutHandler)
        {
            var timeSpan = TimeSpan.FromMilliseconds(millisecondsTimeout);
            try
            {
                Task task = Task.Factory.StartNew(() => messageHandler());
                task.Wait(timeSpan);
                if (!task.IsCompleted)
                {
                    await Task.Factory.StartNew(timeoutHandler);
                    task.Wait();
                    return false;
                }
                return true;
            }
            catch (AggregateException ae)
            {
                throw ae.InnerExceptions[0];
            }
        }

        private async Task MessageReceivedAsync(IDialogContext context, IAwaitable<object> result)
        {
            var activity = await result as Activity;

            await ExecuteWithTimeoutHandler(3000, async () => {
                Task.Delay(3100).Wait(); //fake task taking more than 3 seconds
                Activity reply = activity.CreateReply($"This is the original reply");
                reply.Speak = $"This is the original reply";
                reply.InputHint = InputHints.ExpectingInput;
                await context.PostAsync(reply);
            }, async () => {
                Activity reply = activity.CreateReply($"Working on it...Please hold on");
                reply.Speak = $"Working on it...Please hold on";
                reply.InputHint = InputHints.IgnoringInput;
                await context.PostAsync(reply);
            });
        }
```  

## Node.js example
This example is a bot that starts a task timer and displays an out-of-band wait message until the
task is complete.
```javascript
var restify = require('restify');
var builder = require('botbuilder');

// Setup Restify Server
var server = restify.createServer();
server.listen(process.env.port || process.env.PORT || 3978, function () {
    console.log('%s listening to %s', server.name, server.url);
});

// Create chat connector for communicating with the Bot Framework Service
var connector = new builder.ChatConnector({
    appId: process.env.MicrosoftAppId,
    appPassword: process.env.MicrosoftAppPassword,
    openIdMetadata: process.env.BotOpenIdMetadata
});

// Listen for messages from users
server.post('/api/messages', connector.listen());

// Create your bot with a function to receive messages from the user
var bot = new builder.UniversalBot(connector);
bot.set('storage', new builder.MemoryBotStorage());

const kWelcomeText = 'Hi! Say \'start\' to create a timer and a polling loop.';
const kMisunderstood = 'Sorry, I didn\'t get that.';
const kStarting = 'Starting 30 second timer. Please wait.';
const kWaiting = 'Please wait.';
const kDone = 'My task is done.';

bot.dialog('/', function (session) {
    var txt = session.message.text;
    if (!txt) {
        var msg = new builder.Message(session)
            .text(kWelcomeText)
            .speak(kWelcomeText)
            .inputHint("acceptingInput");
        session.send(msg);
        return;
    }
    if (txt === 'start') {
        console.log('entering pollerDialog');
        session.conversationData.counter = 0;
        session.conversationData.done = false;
        session.beginDialog('pollerDialog');
        return;
    }
    else {
        var msg = new builder.Message(session)
            .text(kMisunderstood)
            .speak(kMisunderstood)
            .inputHint("acceptingInput");
        session.send(msg);
        return;
    }
});

function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms)
)
    ;
}

bot.dialog('pollerDialog', function (session) {
    console.log('entering pollerDialog');
    var iter = session.conversationData.counter || 0;
    session.conversationData.counter = iter + 1;
    if (session.conversationData.done) {
        console.log('done');
        var msg = new builder.Message(session)
            .text(kDone)
            .speak(kDone)
            .inputHint("acceptingInput");
        session.endDialog(msg); // exits the dialog back to main conversation
        return;
    }
    console.log(`iteration is ${iter}`);
    if (iter === 0) {
        console.log('setting timeout');
        setTimeout(function () {
            console.log('timeout done');
            session.conversationData.done = true;
        }, 30000); // 30 seconds - Cortana by default will stop after 10s

        var msg = new builder.Message(session)
            .text(kStarting)
            .speak(kStarting)
            .inputHint("ignoringInput"); // forces Cortana to come back for a turn
        session.sendTyping(); // ignored by Cortana
        session.send(msg);

        console.log('sent kStarting');
        setTimeout(function () {
            console.log('replacing kStarting');
            session.replaceDialog('pollerDialog');
        }, 5000); // after 5s, resend a message to keep the conversation alive
        sleep(5000); // might was well go for a soda
        return;
    } else {
        var msg = new builder.Message(session)
            .text(kWaiting)
            .speak(kWaiting)
            .inputHint("ignoringInput");
        session.sendTyping(); // ignored by Cortana
        session.send(msg);
        console.log('sent kWaiting');
        setTimeout(function () {
            console.log('replacing kWaiting');
            session.replaceDialog('pollerDialog');
        }, 5000);
        sleep(5000);
        return;
    }

});
```