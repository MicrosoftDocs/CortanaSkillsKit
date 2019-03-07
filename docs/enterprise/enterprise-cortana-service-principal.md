---
title: Adding Cortana as a service principal
description: Adding Cortana as service principal so she can access security groups

ms.date: 03/06/2019
ms.topic: article
ms.prod: cortana
ms.author: v-daturc

keywords: cortana enterprise
---  

# Adding Cortana as a service principal

If you use the “deploy to security groups” feature of enterprise skills, you need to allow Cortana visibility to those groups. This is done by an IT administrator adding Cortana as a service principal.

>[!NOTE]
>For information about service principals in Azure, see [Application and service principal objects in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals).

- Open Powershell in administrator mode. <In the word doc, the word "Powershell" is linked to a script. Are they supposed to use that?>
- Unless it's already installed, you need to run `Install-Module AzureAD`.
- `Connect-AzureAD New-AzureADServicePrincipal -AppId "5bea582d-897e-4ace-a2f0-d9a883bbde3d" -DisplayName "Cortana Enterprise"` <Is that GUID always going to be the same?>