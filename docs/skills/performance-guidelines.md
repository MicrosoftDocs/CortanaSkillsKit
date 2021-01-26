---
title: Cortana Skills performance guidelines
description: Tips and guidelines for crating performant Cortana skills.
ms.assetid: 182bda3b-5466-4337-8399-72598116cd9f
ms.date: 07/12/2019
ms.topic: article
keywords: cortana
---

# Skills performance guidelines

## General performance tips

**Load resources at start up**

If you need to retrieve data that the user may request (for example, a list of songs, or images, or locations), load it at startup, not after the user requests the information.
  
**Avoid large images**

Use images that are 720 pixels wide or less. Also consider compressing images to reduce their file size.  
  
**Avoid long texts**

Keep speech text short. As you would expect, it takes longer to process long strings. It's better to split long messages into several shorter ones if possible. Also, the amount of time it takes to process speech depends on whether you use text strings, SSML, MP3 playback, etc. You may want to experiment with different methods.
  
**Avoid long running processes**

Identify the parts of your skill that require the most processing time, and investigate how you can make these parts faster. 

* If your skill repeatedly loads the same data to perform lookups, consider caching the data. Is there any other data that you can also cache in memory?
  
* If your skill calls an external service, determine whether there's a latency issue. Can you accomplish the same task using local code in your skill? Can your skill work without this service?

## Azure performance guidelines

**Same region deployment**

Deploy all your services in the same Azure region. This includes your bot, LUIS, and any external services that your bot uses.

**LUIS deployment**

If you are using LUIS for language understanding, create a key in the same Azure region that your bot runs in. If you created your LUIS service in a different region, you should move it to the same region as your bot.

<!-- confirm: create a key in the same Azure region that your bot runs in. -->
<!-- I went to that page but didn't see how to pick a new region for my existing LUIS service. Seems like we need more details, or a link to an Azure page that offers more details. 

The previous comment refers to this link: see [LUIS Cognitive Service Create](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesLUIS) 

I took it out because it's useless. It just takes you to the Create page.-->

**Avoid cold starts in Azure**

If an Azure function or Web app is not used for a period of time (typically about 20 minutes), Azure recycles it. Recycled functions and apps can take up to 10 seconds to restart. This is known as a cold start. You can prevent cold starts by enabling the [Always On](/azure/azure-functions/functions-scale#always-on) option in the application settings of your Azure [Function](/azure/azure-functions/functions-how-to-use-azure-function-app-settings) or [Web app](/azure/app-service-web/web-sites-configure).

Azure functions and Web apps that are on *Free* or *Shared App* service plans do not have the option to always be on.

**Disable ARR affinity cache**

If you are not using Azure's automatic scaling feature, you should disable application request routing (ARR). For more information, see [Disabling ARR’s Instance Affinity in Windows Azure Web Sites](https://azure.microsoft.com/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites)

## Additional performance resources

- [Bot Framework - Troubleshooting general problems](/azure/bot-service/bot-service-troubleshoot-general-problems?view=azure-bot-service-4.0)
- [Troubleshoot performance issues in Azure Web Apps](/azure/app-service-web/app-service-web-troubleshoot-performance-degradation)
- [Optimize the performance and reliability of Azure Functions](/azure/azure-functions/functions-best-practices)