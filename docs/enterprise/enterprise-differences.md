---
title: Differences between Cortana Skills Kit for Enterprise versus Consumer
description: Describes differences between two types of skills

ms.date: 03/06/2019
ms.topic: article
ms.prod: cortana
ms.author: v-daturc

keywords: cortana enterprise
---  

# Differences between Cortana Skills Kit for enterprise versus consumer

Most of the steps you will take to develop your enterprise skills are the same as those used to develop consumer skills. There are some key differences, though.

- **Cortana endpoints:** Enterprise skills can only be used from Cortana in Windows 10. They do not work with the Android or iOS clients.
- **Account to use:** The consumer skills documentation mentions the use of Microsoft Accounts (MSA), which are usually personal accounts. Use your tenant AAD account instead for building and testing enterprise skills.
- **Consumer skill features not available to enterprise skills:** There are consumer features that are not available to enterprise skills. Please ignore the following documentation when building enterprise skills:
    - [Get the user's profile and contextual information](https://docs.microsoft.com/en-us/cortana/skills/get-user-profile-context): Personalize your skill by getting user profile information and context via AAD permissions that are explicitly extracted by your skill. <!-- Reference in enterprise docs? -->
    - [Publishing Cortana skills](https://docs.microsoft.com/en-us/cortana/skills/publish-skill): There is a separate publishing flow for enterprise skills, which is documented in Configure Tenant Publish. <!-- add link file when created -->
- **Microsoft does not certify enterprise skills:** Your enterprise is responsible for all skills that they develop and use.
