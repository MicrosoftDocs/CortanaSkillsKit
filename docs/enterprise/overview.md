---  
title: Overview of Cortana Skills Kit for Enterprise | Cortana Skills Kit for Enterprise
description: Extend your Cortana capabilities to help your employees be more productive. 

ms.date: 04/25/2019
ms.topic: article
ms.prod: cortana
ms.author: v-daturc

keywords: cortana
---  

# Cortana Skills Kit for Enterprise  

>[!NOTE]
> Cortana Skills Kit for Enterprise is currently available through Microsoft's Technology Adoption Program. <!-- Please fill out the [interest form](http://aka.ms/CortanaForEnterprise) and we will keep you informed about the program.-->

>[IMPORTANT]
> Here is our [latest blog update](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Ftechcommunity.microsoft.com%2Ft5%2FCortana-Skills-Kit-Blog%2FCortana-Skills-Kit-for-Enterprise-BUILD-2019-Update%2Fba-p%2F533738&data=01%7C01%7Cv-daturc%40microsoft.com%7C859d1277447e434bf9cc08d6d1fc6a15%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=LPWiJ5C9ipIR7XDi0wIYe5V5pQVUo61PaiwWhYXMIsQ%3D&reserved=0) on Cortana Skills Kit for Enterprise.

Cortana is a digital assistant that keeps users informed and productive, helping them get things done throughout the day. With Cortana Skills Kit for Enterprise, businesses can now extend Cortana’s capability by building their own custom skills for domains ranging from HR, IT, Helpdesk, Sales to areas like Smart Building:  

:::row:::
    :::column:::
        ![globe](../media/images/blue-globe-20x20.png)  To make information retrieval an easy task  
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        ![screwdriver and wrench](../media/images/blue-screwdriver_and_wrench-20x20.png)  To complete company specific tasks and different workflows more easily with voice  
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        ![clock](../media/images/blue-clock-20x20.png)  Help employees save more time and focus on things that matter most  
    :::column-end:::
:::row-end:::

>[!TIP]
>In Azure Active Directory (Azure AD), a tenant is representative of an organization. It is a dedicated instance of the Azure AD service that an organization receives and owns when it signs up for a Microsoft cloud service such as Azure.

Cortana Skills Kit for Enterprise is built on top of Azure Bot Service and leverages Azure Active Directory to manage building, testing and deployment of the custom skills within the tenant.  
* [Azure Bot Service](https://azure.microsoft.com/services/bot-service)  
    A skill is a speech bot. Use the Bot Framework to build your speech bot, register it, and define your Cortana channel. The framework provides a .NET SDK and Node.js SDK that you use to build your bot. The Bot Framework SDKs provide features such as dialogs and built-in prompts that make interacting with users much simpler.  

* [Azure Active Directory](https://azure.microsoft.com/services/active-directory)  
    Azure Active Directory (Azure AD) helps enterprises manage user identities and create intelligence-driven access policies to secure your resources. The Skills Kit leverages the same technology to deploy custom skills to a group of Azure AD users for testing and to manage deployment to the entire tenant.  

* [IT Admin Portal for managing skill deployment to tenant](https://it-admin-portal-prod.azurewebsites.net/)
    Dedicated portal for IT Administrators and delegated reviewers to review the skills submitted by enterprise developers for deployment to tenant. Reviewers should ensure that custom skills follow company’s guidelines on privacy, security and other practices before approving a skill for tenant deployment. 

<!-- 04/25/2019 commented out because there really is no next step for this version of enterprise --dt
## Next steps

Read the [Before you start](/before-you-start.md) page for an overview of the development process. -->