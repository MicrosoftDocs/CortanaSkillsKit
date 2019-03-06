---
title: Monitoring your skill
description: How to monitor skills after they're deployed

ms.date: 03/06/2019
ms.topic: article
ms.prod: cortana
ms.author: v-daturc

keywords: cortana enterprise
---  

# Monitoring your skill after deployment

If your IT Admin has given you permission, you may monitor the health of your skills.  From the channel configuration, click on `All App Service Settings`, or click on the **Monitor** blade under services. Select your skill to see `Insights`. This will show server health and metrics pinned to the summary dashboard, including:

- HTTP 5xx errors,
- Data In
- Data Out
- HTTP Requests, and
- Average Response Time.

You can drill into any metric by clicking on it, or you can add your own!

To add your own metrics, select `Monitor` and then your skill’s Application Insights. Click the **Metrics** blade to start exploring data that's available out of the box.

Use Smart Detection to set up alerts or notifications based on rules or performance thresholds.

For more details, visit [Azure Monitor](https://azure.microsoft.com/en-us/services/monitor/)