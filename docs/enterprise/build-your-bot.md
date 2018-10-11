---
title: Build Your Bot | Cortana Skills Kit for Enterprise
description: Build your bot. 

ms.date: 10/10/2018
ms.topic: article
ms.prod: cortana

keywords: cortana
---

# Build Your Bot  

1.  Go to the [Bot Framework Developer](https://dev.botframework.com) portal.  
    1.  Click on the **sign in** button in the top right and sign in with your Active Directory (AD) account.  
    2.  Click on the **My bots** link.  
        
        >[!NOTE]
        > A list of your bots is displayed.  
    
    3.  Click on the **create a bot** link.  
    4.  Click on the **Create** button to confirm bot creation using Azure Bot Service.  
2.  On the Azure portal, click on the **Web App Bot** link.  
    
    >[!NOTE]
    > To create a bot directly through the Azure portal.
    > 1.  Click on the **Create Resource** link.  
    > 2.  Click on the **AI + Machine Learning** link.  
    > 3.  Click on the **Web App Bot** link.  
    
    1.  Complete the fields.  
        *   `Bot Name` | required  
        *   `Subscription` | required  
            *   For more information about subscriptions, visit the [Enterprise Cloud Adoption: Resource access management in Azure](https://docs.microsoft.com/azure/architecture/cloud-adoption/getting-started/azure-resource-access) page.  
        *   `Resource group` | required  
            *   For more information about resource groups, visit the [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) page.  
        *   `Location` | required  
            *   Location of your resources.  
                Select location near you.  
        *   `Pricing` | required  
            *   `F0 Free` or `S1 Premium`  
                 For more information about pricing, visit the [Azure Bot Service pricing](https://azure.microsoft.com/pricing/details/bot-service) page.  
        *   `App Name` | required  
            *   A unique name for your service.   
                
                >[!NOTE]
                > Use any combination of your corporation or organization names to differentiate your bots.  
                
        *   `Bot template` | required 
            *   See below.  
        *   `LUIS App location` | required  
            *   Language Understanding Intelligent Service.
                For more information about LUIS, visit the[Language Understanding (LUIS)](https://www.luis.ai) page.  
                Select location near you.  
        *   `Azure Storage` | required  
            *   Create a new or use an existing Azure storage container.  
        *   `Application Insights` | optional  
            *   Enables analytics using Azure Application Insights.  
        *   `Application Insights Location` | required  
            *   Location to gather and store metrics.  
                Select location near you.  
        *   `Microsoft App Id and Microsoft App Password` | required  
            *   Auto-create or select from a previously registered Azure app.  
                `client ID` or `app ID`  
                `secret key` or `app password`  

    2.  Click on the **Create** button.  

    3.  Wait for deployment  
        
        >[!Note]
        > After your bot is deployed, you are prompted to pin the bot to your Azure dashboard for easy access.  
    
## Next Steps  
