---
title: Testing and debugging Cortana skills
description: Tips on testing and debugging Cortana skills.

ms.assetid: 3f37e309-3170-4896-8434-33bdce3c1889
ms.date: 07/09/2019
ms.topic: article

keywords: cortana
---

# Testing and debugging Cortana skills

   >[!TIP]
   >Before you start debugging your Cortana skill, visit the [Troubleshooting tips](#troubleshooting-tips) section and the [Known Issues](./known-issues.md) page.  

The following options are available to test and debug your Cortana skill.

- Use the Bot Framework emulator to test and debug your skill while you are developing it. The emulator interacts with your bot, and displays the messages exchanged.  

    Currently, the emulator does not support passing user profile and contextual information to your Cortana skill. For more information about using the emulator, visit the [Debug with the emulator](https://docs.microsoft.com/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0) page.  

- Use the debugger in Visual Studio Code to walk through your code as it runs in the console window.  

   For more information, visit the [Debug a bot](https://docs.microsoft.com/azure/bot-service/bot-service-debug-bot?view=azure-bot-service-4.0) page.  

- Use the Chat window in the Bot Framework portal. In order to confirm that your bot is running, you typically test after configuring your Cortana channel and deploying your service.

- Enable debug in Cortana to see the message exchange between Cortana and your Cortana skill.

   For information about enabling debugging, visit the [Enable debugging in Cortana](#enable-debugging-in-cortana) section.

<!-- 07/09/2019: Commented this out because it points to the same debugger as above, and I am unable to find a  page referencing
    debugging in the Azure environment. --dt
   For details about debugging your Cortana skill in the Azure environment, visit the [Debug an Azure Bot Service bot](https://docs.microsoft.com/azure/bot-service/bot-service-debug-bot?view=azure-bot-service-4.0) page. -->

   If you're working in a continuous publishing environment, see the [Set up continuous deployment](https://docs.microsoft.com/azure/bot-service/bot-service-continuous-deployment?view=azure-bot-service-4.0) page.

## Enable debugging in Cortana

If Cortana reports an error when running your skill, then follow the steps below to turn on debugging for Cortana. After you enable debugging, the Cortana Canvas displays all errors and message exchanges.  

1. Go to the Configure Cortana page for your Cortana skill. Under the *Enable Cortana debug mode across all devices* section, click `Run Cortana in debug mode`  to enable.

1. Invoke Cortana to test your Cortana skill. Make sure you're signed in using the same Microsoft Account (MSA) that you used for the Bot Framework.

    For more information, visit the [Getting started with Cortana skills](get-started.md) page.

    a.  On the top-left menu, click on the `Home` icon. (This will update the Cortana skills information.)

    b.  On the bottom-right corner, click on the microphone icon.

    c.  Invoke your Cortana skill by speaking. 

    d. The canvas displays a `debug` button.

    e.  Click to see the message exchange details.  

    ![Debugging Information](../media/images/debugging-info.png)

## Troubleshooting tips

Suggestions for solving common problems.

| Issue  |  
|:---    |  
| [I am not able to invoke my Cortana skill](#i-am-not-able-to-invoke-my-cortana-skill) |  
| [Cortana is spelling my invocation name incorrectly when I say it](#cortana-is-spelling-my-invocation-name-incorrectly-when-i-say-it) |  
| [I get a `DownstreamDependencyFailed` error](#i-get-a-downstreamdependencyfailed-error) | 
| [I signed into Bot Framework but do not see my Cortana skills](#i-signed-into-bot-framework-but-do-not-see-my-cortana-skills) |  
| [SSML reads XML characters aloud](#ssml-reads-xml-characters-aloud) |  
| [Cortana returns a `403 Forbidden` error](#cortana-returns-a-403-forbidden-error) |  
| [I am able to invoke my Cortana skill but no one else can](#i-am-able-to-invoke-my-cortana-skill-but-no-one-else-can) |  

### I am not able to invoke my Cortana skill  

- If you just made changes and saved your skill, you may need to refresh the Cortana skills information. Click on the `Home` icon on the top-left menu.
- Verify that debugging is enabled. For more information, visit the [Enable debugging in Cortana](#enable-debugging-in-cortana) section.
- Verify that you signed into Cortana using the same MSA that you used to sign into Bot Framework.  
- Ensure that you are properly invoking your skill.
- Verify that Cortana uses the correct name when invoked. The Cortana Canvas types the name in the `Type here to search box` as you speak.
- Check that your device is set to one of the allowed locales. The [Supported Cortana locales](./supported-locales.md) page has more information.
- Make sure that your microphone is configured. Visit the [Getting started with Cortana skills](./get-started.md) page for more information.

### Cortana is spelling my invocation name incorrectly when I say it

- If you just saved for the first time, your updates to Cortana may be delayed up to 10 minutes before recognizing the invocation name of your Cortana skill.  
- If you just made changes and saved your skill, you may need to refresh the Cortana skills information. Click on the `Home` icon on the top-left menu.
- Your invocation name may be difficult for Cortana to recognize. For more information about designing invocation names, see the [Invocation Name Guidelines](./cortana-invocation-guidelines.md) page.  

### I get a `DownstreamDependencyFailed` error  

You will get this error when the service endpoint you created fails to respond. Some common reasons:

- If your service takes too long to respond, Cortana cancels the request with a time-out.  
- If the response message is not formatted correctly based on the Bot Framework schema.  
- If your service returns an http status code other than 200.  

### I signed into Bot Framework but do not see my Cortana skills  

Ensure that you signed into Bot Framework with the same MSA that you used to configure the Cortana channel within the Azure portal.  

### SSML reads XML characters aloud

If Cortana reads out the XML characters of your invocation, then the XML is likely not valid. Verify that all opening tags have closing tags and vice-versa. Consider using an XML library to verify that your XML is properly formatted.  

### Cortana returns a `403 Forbidden` error  

Cortana tried to connect to your service, but received an https status code of `403 Forbidden`. Verify that your service endpoint is configured to accept `POST` requests, not `GET` requests.

### I am able to invoke my Cortana skill, but no one else can  

Ensure that you have successfully deployed your skill.

- If you want to make your skill available to a group of people, such as your family and friends, use the [Test Group settings](./pub-test-settings.md) option.  
- If you want everyone to have access to your skill, use the [World settings](./publish-skill.md#world-settings) option. Your skill will be reviewed by Microsoft if you choose this option.

    See [Publishing Cortana skills](./publish-skill.md) for details on the publishing process.

    >[!IMPORTANT]
    > If your skill includes code that checks the skill ID in the request, then you have to remember to change the ID as you move between steps. The ID value will be different for each of the versions (default, test group, and world) of your Cortana skill.  

## Additional resources

### Stack Overflow forums

- [Bot Framework](https://stackoverflow.com/questions/tagged/botframework)  
- [Cortana Skills Kit](https://stackoverflow.com/questions/tagged/cortana-skills-kit)  
- [LUIS](https://stackoverflow.com/questions/tagged/luis)  
- [Cognitive Services](https://stackoverflow.com/questions/tagged/microsoft-cognitive)  

### Azure debugging resources

#### Azure Web Apps

- [Best Practices for Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-best-practices)  

- [Remote debugging Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#a-nameremotedebugaremote-debugging-web-apps): After enabling remote debugging, simply invoke your Cortana skill and Cortana stops at your breakpoint as you walk through your code. Cortana is likely to time out on your request, but you are still able to step through your code and look for issues.  
- [Best practices and troubleshooting guide for node applications on Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-nodejs-best-practices-and-troubleshoot-guide)  
- [Troubleshoot slow app performance issues in Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-troubleshoot-performance-degradation) 

#### Azure Functions  

- [Optimize the performance and reliability of Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-best-practices)  
- [How to code and test Azure functions locally](https://docs.microsoft.com/azure/azure-functions/functions-run-local)  
- [Code and test Azure Functions locally](https://docs.microsoft.com/en-us/azure/azure-functions/functions-develop-local)  

### Bot Framework troubleshooting guides  

- [Bot Framework troubleshooting guide](https://aka.ms/hsjcm9)  
- [Troubleshooting Bot Framework authentication](https://aka.ms/aei8qy)  
