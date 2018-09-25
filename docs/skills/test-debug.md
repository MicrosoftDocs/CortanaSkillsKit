---
title: Testing and debugging Cortana Skills
description: Tips on testing and debugging Cortana Skills.
label: Conceptual

ms.assetid: 3f37e309-3170-4896-8434-33bdce3c1889
ms.date: 09/25/2018
ms.topic: article

keywords: cortana
---

# Testing and debugging Cortana Skills

The following are the options available to test and debug your skill.

- Use Bot Framework's emulator to test and debug your skill while you're developing it. The emulator lets you interact with your bot and see the messages that are exchanged. For details about using the emulator, see [Debug with the emulator](https://docs.microsoft.com/bot-framework/debug-bots-emulator). Currently, the emulator does not support passing user profile and contextual information to the skill. 
  
- Use the debugger in Visual Studio Code to walk through your code as it executes in the console window. For details, see [Debug a Bot Service bot](https://docs.microsoft.com/bot-framework/bot-service-debug-bot).
  
- Use the Chat window in the Bot Framework portal. Typically, you do this after you configure your Cortana channel and deploy the service to confirm that it's running.  
  
-  Enable debug in Cortana so you can see the message exchange between Cortana and your skill. For information about enabling debugging, see [Enable debugging in Cortana](#Enable-debugging-in-Cortana).


For details about debugging your skill in Azure's [continuous publishing](https://docs.microsoft.com/bot-framework/azure-bot-service-continuous-deployment#set-up-continuous-deployment) environment, see [Debug an Azure Bot Service bot](https://docs.microsoft.com/bot-framework/azure-bot-service-debug-bot).


But before you start debugging your skill, check out [Troubleshooting tips](#Troubleshooting-tips) and [Known Issues](known-issues.md).

> [!NOTE]
> If you found an error in someone else's Cortana skill, use the feedback button in Cortana to report it.


<a name="Enabling-Debugging-of-Cortana-Skills"></a>
## Enable debugging in Cortana

If Cortana reports an error when running your skill, follow these steps to turn on Cortana's debugging. When enabled, Cortana displays all errors and message exchanges on her canvas.

 1. Log in to the old [skills dashboard](https://developer.microsoft.com/en-US/cortana/dashboard#!/home) using the Microsoft account (MSA) that you used to configure your Cortana channel. 
 2. Click **Debug** in the left pane.
 3. Check **Debug mode for Cortana** to enable debugging. 
 4. Start Cortana on the system that you want to test your skill on. 
 5. Make sure you're signed in using the same MSA you used to sign into the dashboard with. For details, see [Get started](get-started.md).
 6. Click the **Home** icon on Cortana's menu bar to ensure that your computer is refreshed with the updated skills information from the dashboard.
 7. Click Cortana's microphone icon and invoke your skill. For information about invoking skills, see [Invocation name guidelines](cortana-invocation-guidelines.md).
 8. The canvas includes a debug button that you click to see the message exchange details. 

![Debugging Information](../images/testing/debugging-info.png)



## Troubleshooting tips

The following provides suggestions for solving common problems.

|Issue|Tip
|-|-
|I can't invoke my skill|Check the following:<ul><li>If you just saved your skill, press the **Home** icon on Cortana's menu bar. This updates Cortana's list of known skills on the computer with changes from Cortana's dashboard.</li><li>Make sure that you enabled debugging (see [Enable debugging in Cortana](#Enable-debugging-in-Cortana)).</li><li>Make sure that you signed into Cortana using the same MSA that you used to sign in to Cortana's dashboard.</li><li>Ensure that you are properly invoking your skill.</li><li>Verify that Cortana uses the correct name when she invokes your skill (she types the name in the **Type here to search** box as you speak).</li><li>Ensure that your device is set to one of the locales listed in [Supported Cortana locales](supported-locales.md).</li><li>Ensure that your microphone is configured. For details, see [Get started](get-started.md).</li></ul>
|Cortana isn't spelling my invocation name correctly when I say it|Check the following:<ul><li>If you just saved your skill for the first time, it can take up to 10 minutes for the Cortana to recognize it as a skill invocation name.</li><li>If you just saved your skill, try pressing the **Home** icon in Cortana's menu bar to refresh her list of known skills.</li><li>Your invocation name may not be well designed, which makes it difficult for Cortana to recognize it. Take a look at the [Invocation Guidelines](cortana-invocation-guidelines.md) for tips on creating a well-designed invocation name.</li></ul>
|I can't create more than 20 skills|You may associate a maximum of 20 skills to a Microsoft accounts (MSA). If you create more than 20 skills, simply use an additional MSA. <!-- confirm this limit still exists -->
|<a name="DownstreamDependencyFailed"></a>I get a `DownstreamDependencyFailed` error|You get this error when the service endpoint you created, failed to respond. For example:<ul><li>If your service takes too long to respond, Cortana will time-out the request.</li><li>If the response message is not formatted correctly based on the Bot Framework schema.</li><li>If your service returns a status code other than 200.</li></ul>
|I can invoke my skill, but no one else can|Ensure that you deployed your skill. If you want to make your skill available to a group of people, such as your family and friends, use the [Publish to Group](publish-skill.md#publish-to-group) option. If you want everyone to have access to your skill, use the [Publish to World](publish-skill.md#publish-to-world) option.<br /><br />**NOTE:** If your skill includes code that checks the skill ID in the request, the ID is different between the deployed to self, group, and world versions of your skill (your skill has a unique ID for each deployment).
|I've logged into the Cortana dashboard but don't see my skills|Ensure that you signed in to the dashboard with the same MSA that you used to configure the Cortana channel with in the Bot Framework portal.
|SSML reads XML characters aloud|If Cortana reads out the XML characters of your, the XML is likely invalid. Be sure that all opening tags have closing tags and vice-versa. Consider using an XML library to ensure that your XML is properly formatted.
|Cortana returns Forbidden error|Cortana tried to connect to your service but received a 403 Forbidden error. Ensure that your service endpoint is configured to accept POST requests, not GET requests.


## Additional resources

### Stack Overflow forums

- [Bot Framework](https://stackoverflow.com/questions/tagged/botframework)
- [Cortana Skills Kit](https://stackoverflow.com/questions/tagged/cortana-skills-kit)
- [LUIS](https://stackoverflow.com/questions/tagged/luis)
- [Cognitive Services](https://stackoverflow.com/questions/tagged/microsoft-cognitive)


### Azure debugging resources

**Azure Web Apps**

* [Remote debugging Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#a-nameremotedebugaremote-debugging-web-apps)  
  - After enabling remote debugging, simply invoke your skill in Cortana and it will hit your breakpoint you can walk through your code. Note that Cortana will likely timeout on your request, but you can still step through your code and look for issues. 
* [Best practices and troubleshooting guide for node applications on Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-nodejs-best-practices-and-troubleshoot-guide)
* [Troubleshoot slow web app performance issues in Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-troubleshoot-performance-degradation)
* [Best Practices for Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-best-practices)

**Azure Functions**

* [How to code and test Azure functions locally](https://docs.microsoft.com/azure/azure-functions/functions-run-local)
* [Running Azure Functions Locally with the CLI and VS Code](https://blogs.msdn.microsoft.com/appserviceteam/2016/12/01/running-azure-functions-locally-with-the-cli/)
* [Tips for improving the performance and reliability of Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-best-practices)


### Bot Framework troubleshooting guides

* [Bot Framework troubleshooting guide](https://aka.ms/hsjcm9)
* [Troubleshooting Bot Framework authentication](https://aka.ms/aei8qy)



<!--
![Debugging using Bot Framework Channel Emulator](../images/testing/bot-emulator-debugging.png)

**Not all Bot Framework Cards are supported in Cortana**

Currently Cortana supports the following Bot Framework cards: Hero Card, Thumbnail Card, Receipt Card.
-->

<!-- //TODO: AIT
## Custom Skills imported from Alexa

*Third-party trademarks used herein are the property of their respective owners.  Use of such marks does not imply any affiliation, sponsorship, or endorsement.*

If you are importing a skill from Alexa, it should be safe to assume that your skill was working on Alexa. The following are some tips on testing and debugging issues with Alexa import skills.

**I can trigger my Alexa imported skill but it is not working**

* Make sure to either disable the Alexa application ID verification in the Alexa code as Cortana will pass a different application ID (skill ID) or update your service to accept the skill id of your Cortana skill. If your code is a Node.js function, check to see if there is an **APP_ID** property in it. If it is present, add an if statement to check that the request contains either your Alexa skill application ID or your Cortana skill ID.

**Which image URL is Cortana using?**

Cortana will use the small image URL if it is available. If it isn't, it will then fall back to the large image URL if it is available and will scale the image as needed. The Cortana card scales images to 100% of the width of Cortana's canvas and then scales the height such that it maintains the original image aspect ratio.
-->