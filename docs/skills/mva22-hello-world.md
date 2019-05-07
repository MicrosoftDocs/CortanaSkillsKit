---
title: Create your first Cortana Skill
description: Describes how to create your first Cortana Skill.

ms.date: 05/07/2019
ms.topic: article

keywords: cortana
---

# Create your first Cortana skill

Once you have set up your environment, you can dive in and build your first Cortana skill. As you learned in the previous module, you can develop a Cortana skill on either a Mac or a PC running Windows 10 Anniversary Update (build 1607) or later, using your choice of development tools. For more information on setting up your development environment, see [Set up your development environment](./mva21-setup.md).

This module shows the basics of creating a Cortana skill using the Azure Portal and Azure Bot Service. First, you'll create a bot, and then register it and connect it to the Cortana channel to make it a Cortana skill.

For more information on creating your first skill, see [Create your first skill](./get-started.md).

## Step 1 - Create a bot using the Azure Bot Service

To create a bot using the Azure Bot Service, first open the [Microsoft Azure Portal](https://ms.portal.azure.com) and log in with your Microsoft account.

1. Click on `Create a resource`.

1. In the Azure Marketplace pane, click `AI + Machine Learning`.
1. Click on `Web App Bot` in the `Featured` column.

![Azure Marketplace](../media/images/mva22_azure_marketplace.png)

Enter a name for your bot. The bot service uses the bot name as the default name for the resource group name and app name.

Specify your subscription plan, location, app name, and the bot template you want to use, and then click `Create`. To create a simple single-dialog bot that echoes back the user input, use the `Basic` template.

![Create Pane](../media/images/mva22_create.png)

It may take a few minutes to provision and initialize your bot. When the process is complete, you can test your bot. Click `Test in Web Chat` to open the **Test** pane.

![Open Test](../media/images/mva22_open_test.png)

Try typing something into the `Type your message` prompt. The bot repeats what you typed, preceded by "You said " and a count of how many messages you've typed. You can reset the count by typing `reset`.

![Test Bot](../media/images/mva22_test.png)

## Step 2 - Explore the code

The mva-hello-world bot uses .NET C# code that is part of the Basic bot template. To view the code behind the bot, click `Build` and then `Open online code editor` to open the **App Service Editor**.

![Open Code Editor](../media/images/mva22_open_code_editor.png)

The code that handles the bot's response to the message you type can be found in the `MessagesController.cs` and `EchoDialog.cs` modules. Expand the **Controllers** and **Dialogs** trees under WWWROOT in the **App Service Editor** to view the code.

![Code Modules](../media/images/mva22_modules.png)

The Post method in `MessagesController.cs` invokes an instance of the `EchoDialog` class when a user types a message:

``` C#
    public virtual async Task<HttpResponseMessage> Post([FromBody] Activity activity)
    {
         // check if activity is of type message
        if (activity != null && activity.GetActivityType() == ActivityTypes.Message)
        {
            await Conversation.SendAsync(activity, () => new EchoDialog());
        }
        else
        {
            HandleSystemMessage(activity);
        }
        return new HttpResponseMessage(System.Net.HttpStatusCode.Accepted);
    }
```

The `EchoDialog` class contains the code that creates the response:

``` C#
    public class EchoDialog : IDialog<object>
    {
        protected int count = 1;

        public async Task StartAsync(IDialogContext context)
        {
            context.Wait(MessageReceivedAsync);
        }

        public async Task MessageReceivedAsync(IDialogContext context, IAwaitable<IMessageActivity> argument)
        {
            var message = await argument;

            if (message.Text == "reset")
            {
                PromptDialog.Confirm(
                    context,
                    AfterResetAsync,
                    "Are you sure you want to reset the count?",
                    "Didn't get that!",
                    promptStyle: PromptStyle.Auto);
            }
            else
            {
                await context.PostAsync($"{this.count++}: You said {message.Text}");
                context.Wait(MessageReceivedAsync);
            }
        }

        public async Task AfterResetAsync(IDialogContext context, IAwaitable<bool> argument)
        {
            var confirm = await argument;
            if (confirm)
            {
                this.count = 1;
                await context.PostAsync("Reset count.");
            }
            else
            {
                await context.PostAsync("Did not reset count.");
            }
            context.Wait(MessageReceivedAsync);
        }
    }
```

You can revise the code to customize the response. For example, you could revise the `EchoDialog` class to display how many characters are in the message:

``` C#
    public class EchoDialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            context.Wait(MessageReceivedAsync);
        }

        public async Task MessageReceivedAsync(IDialogContext context, IAwaitable<IMessageActivity> argument)
        {
            var message = await argument;
            int msgLength = (message.Text ?? string.Empty).Length;

            await context.PostAsync("'" + message.Text + "'" + " has " + msgLength + " characters.");
            context.Wait(MessageReceivedAsync);
        }
    }
```

For the changes to take effect, you need to redeploy the bot. In the **App Service Editor**, click the `Open Console` icon to open the **Console** window, and then enter `build.cmd`.

![Console Window](../media/images/mva22_console_window.png)

Once the redeployment is complete, you can return to the **Test** pane to test your bot.

![Revised Bot](../media/images/mva22_revised_bot.png)

## Step 3 - Connect your Azure Bot to the Cortana Channel

Once you have created a bot, connect it to the Cortana channel to make it a Cortana skill.

In the Azure Portal, click the Channels tab to view the available channels, and then click the Cortana channel.

On the Configure Cortana page, scroll down to the **Discovery and Management** section and click `Manage`. Click the `Publish` menu tab and then `Publish to self` to open the channel configuration settings, where you can specify an optional icon for the skill, a display name, and the invocation name. Cortana uses the invocation name you specify to invoke the skill.

<!-- new -->  
![Configure Cortana Skill](../media/images/cortana-configure-settings.png)  
<!-- new -->  

On the Channels tab of the Azure Portal, you can now see Cortana listed as an `mva-hello-world` bot service channel.

![Bot Channel](../media/images/mva22_helloworld_channel.png)

To return to the **Configure Cortana** page, where you can update the skill's configuration settings, click `Edit`. To test your new skill, direct Cortana to invoke the skill using the invocation name you specified; for example, "Tell Hello World 'hi there'."

![Hello World Cortana](../media/images/mva22_helloworld_cortana.png)
