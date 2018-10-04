---
title: Cortana Skills performance guidelines
description: Tips and guidelines for crating performant Cortana skills.
ms.assetid: 182bda3b-5466-4337-8399-72598116cd9f
ms.date: 09/5/2017
ms.topic: article
keywords: cortana
---

# Skills performance guidelines


## General performance tips

**Load resources at start up**

If you need to retrieve data that the user may ask for (for example, a list of songs, images, locations), do that at starts up, not when the user requests the information.  
  
  
**Avoid large images**

Use images that are a 720 pixels wide or less. Also consider compressing images to reduce their file size.  
  
**Avoid long speak texts**

Keep speech text short because translating long strings takes longer than translating short string. It's better to split long messages into several shorter ones. The amount of time it takes to translate speech depends on whether you use text strings, SSML, MP3 playback, etc.   
  
**Avoid long running processes**

Identify the parts of your skill that require the most processing time and investigate how you can make these parts faster. 

* If your skill repeatedly loads the same data to perform look ups, consider caching the data. Determine whether there's any other data that you can cache in memory?  
  
* If your skill calls an external service, determine whether there's a latency issue with calling the service. Can you accomplish the same task using local code in your skill? Can your skill work without this service?

<!-- start up: what's the max time where they'd want to load at start up versus when requested? A. Ask Vivek.-->




## Azure performance guidelines

**Same region deployment**

Deploy all your services in the same Azure region. This includes your bot, LUIS, and any external services that your bot uses.


**LUIS deployment**

If you are using LUIS for language understanding, create a key in the same Azure region that your bot runs in. If you created your LUIS service in a different region, see [LUIS Cognitive Service Create](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesLUIS) to pick a new region.

<!-- confirm: create a key in the same Azure region that your bot runs in. -->
<!-- I went to that page but didn't see how to pick a new region for my existing LUIS service. Seems like we need more details, or a link to an Azure page that offers more details. -->

NOTE: It may take up to 10 minutes for the newly generated keys to take effect.

**Avoid cold starts in Azure**

If an Azure Function and Web app is not used for a period of time (typically about 20 minutes), Azure recycles it. Recycled functions and apps can take up to 10 seconds to start. This is known as a cold start. You can prevent cold starts by enabling the [Always On](https://docs.microsoft.com/azure/azure-functions/functions-scale#always-on) option in the application settings of your Azure [Function](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings) or [Web app](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

Azure Functions and Web apps that are on Free or Shared App Service plans do not have the option to be always on.

**Disable ARR affinity cache**

If you are not using Azure's automatic scaling feature, you should disable application request routing. For more information, see [Disabling ARR’s Instance Affinity in Windows Azure Web Sites](https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)

## Additional performance resources

- [Troubleshoot performance issues in Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-troubleshoot-performance-degradation)
- [Optimize the performance and reliability of Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-best-practices)
- [Bot Framework - Troubleshooting general problems](https://docs.microsoft.com/bot-framework/troubleshoot-general-problems)