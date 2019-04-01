---
title: Differences between enterprise skills development and the Cortana Skills Kit
description: Describes differences between two types of skills

ms.date: 04/01/2019
ms.topic: article
ms.prod: cortana
ms.author: v-daturc

keywords: cortana enterprise
---  

# Differences between enterprise skills development and the Cortana Skills Kit

The Cortana Skills Kit targets consumer skills only. While most of the steps you will take to develop your enterprise skills are the same as those used to develop consumer skills, there are some key differences.

- **Cortana endpoints:** Enterprise skills can only be used from Cortana in Windows 10. They do not work with the Android or iOS clients.

- **Account to use:** The consumer skills documentation mentions the use of Microsoft Accounts (MSA), which are usually personal accounts. Instead of using an MSA, you must use your Azure Active Directory (AAD) account on your enterprise tenant for building and testing enterprise skills.

- **Consumer skill features not available to enterprise skills:** There are consumer features that are not available to enterprise skills. Please ignore the following documentation when building enterprise skills:
    - To personalize your skill, get user profile information and context via AAD permissions that are explicitly extracted by your skill. Ignore [Get the user's profile and contextual information](https://docs.microsoft.com/en-us/cortana/skills/get-user-profile-context).<!-- Reference in enterprise docs? -->
    - [Publishing Cortana skills](https://docs.microsoft.com/en-us/cortana/skills/publish-skill): There is a separate publishing flow for enterprise skills, which is documented in Configure Tenant Publish. <!-- add link file when created -->
- **Microsoft does not certify enterprise skills:** Your enterprise is responsible for all skills that they develop and use.
