---
title: Show the user you're working on their request 
description: For long running request, show the user that you're still working on their request.

ms.assetid: 23802F09-921E-4475-AD34-3A71C9078290
ms.date: 10/12/2018
ms.topic: article

keywords: cortana
---

# Show the user you're working on their request

If it takes longer than three seconds to fulfill the request, you should send a message to the user letting them know that you're still working on their request.

The following shows an example that uses the `ExecuteWithTimeoutHandler` method to notify the user if the request exceeds three minutes. The `ExecuteWithTimeoutHandler` method executes the default message handler for the specified number of milliseconds. If the method exceeds the limit, it executes the timeout handler, which sends a message to the user (for example, "Working on it...").

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

<!--
For an equivalent example in Node.js, see the [ProgressDialog](https://github.com/Microsoft/BotBuilder-Samples/tree/master/Node/core-ProgressDialog) sample.
-->
