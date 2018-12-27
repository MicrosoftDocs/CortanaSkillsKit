The Cortana channel will speak the message or response sent from the skill to the channel if the _speak_ property is set on the message.
Bot Service bots do not speak by default, so you need to make minor modifications to get Cortana to speak!



## Add Speech to Bot Service (V4) bots ##

On a 'turn' you have two forms of 'sendActivityAsync': the first method takes an activity (message), and the second takes optional named
arguments 'speak' and 'inputHint'.

C# example

   var message = turnContext.Activity.CreateReply();
   message.Text = "This is displayed";
   message.Speak = "This is spoken";
   message.InputHint = "expectingInput";
   await turnContext.SendActivityAsync(message);

OR

   await turnContext.SendActivityAsync( "This is displayed", speak: "This is spoken", inputHint: "expectingInput" );

Find the reference documentation here: [C#](https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.builder.iturncontext.sendactivityasync).
or [javascript](https://docs.microsoft.com/en-us/javascript/api/botbuilder-core/turncontext#sendactivity).

## Add Speech to Bot Framework (V3) bots ##

   Activity message = activity.CreateReply("This is displayed");
   message.Speak = "This is spoken";
   message.InputHint = InputHints.ExpectingInput;
   await context.PostAsync(message);

OR

   await context.SayAsync(text: "This is displayed!", speak: "This is spoken");


Note: SayAsync has been deprecated in V4 of Bot Service.

