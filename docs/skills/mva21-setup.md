---
title: Set up your development environment
description: Describes how to set up the Cortana development environment.
author: v-stsau
manager: mujtabak
label: Conceptual

ms.author: v-stwohl
ms.date: 5/03/2018
ms.topic: article
ms.prod: cortana
keywords: cortana
--- 

# Set up your development environment

|   |   |
| - | - |
| ![](../images/video-icon.png) | [Watch a video](https://mva.microsoft.com/en-US/training-courses/getting-started-with-cortana-skills-18241?l=EkOyiMfnE_7911787171) about how to set up your development environment. |


Before you can build your first skill, you need to set up your development environment. Here are a few things you may need to do:

* Set up cloud resources such as a Microsoft account, the Cortana developer center, Bot Framework, LUIS (Language Understanding Intelligent Service), and a cloud hosting account on Microsoft Azure or another hosting service.
* Make sure your PC or Mac has the necessary development tools and operating system version. 
* Set up your Android or iOS mobile device, or Harman Kardon Invoke speaker, to work with Cortana.
* Set up Cortana.

## Step 1 - Set up cloud resources

Developing a Cortana skill requires a variety of cloud resources. For example, you need a Microsoft account in order to register your skill and connect it to Cortana. If you don't already have a Microsoft account, go to the [Microsoft Account](https://account.microsoft.com/account) web site to sign up for one.

> [!NOTE]
> To develop a Cortana skill, you must use a [Microsoft account](https://account.microsoft.com/account) rather than an Azure Active Directory (Azure AD) organizational account, such as an account associated with Office 365.

![Microsoft account site](../images/microsoft-account.png)

Other resources include:

* **Bot Framework**. To create a Cortana skill, you must first create a bot. Then log in to the [Bot Framework Developer Portal](https://dev.botframework.com/) using your Microsoft account, register the bot, and connect it to the Cortana channel to make it a Cortana skill. For information on creating your first Cortana skill, see [Create your first Cortana skill](https://docs.microsoft.com/en-us/cortana/skills/mva22-hello-world).

![Bot Framework developer portal](../images/Bot-Framework-dev-portal.png)

* **Cortana Developer Center**. Log in to the [Cortana Developer Center](https://developer.microsoft.com/cortana) using your Microsoft account to open your Cortana Skills Dashboard. The developer center provides a variety of resources for developing a Cortana skill.

![Cortana Dev Center](../images/Cortana-dev-center.png)

* **LUIS (Language Understanding Intelligent Service)**. Log in to [LUIS.ai](https://www.luis.ai) using your Microsoft account to create and manage LUIS applications that let you use language understanding technology in your Cortana skill. 

![LUIS Site](../images/mva32-LUIS-account.png)

* **A cloud hosting service**. Optionally, you can use a cloud hosting service such as [Microsoft Azure](https://azure.microsoft.com). This is required if you want to want the skill to be available to Cortana using a web address.

![Azure Site](../images/Azure-site.png)

## Step 2 - Set up your PC, Mac, or Cortana device

You can develop a Cortana skill on either a Mac or a PC running Windows 10 Anniversary Update, using your choice of development tools. The only requirement is that you have installed the [Microsoft Bot Builder SDK](https://github.com/Microsoft/BotBuilder).

Although you can use any development environment, Microsoft Visual Studio offers a variety of useful tools and features, including Bot Application, Bot Controller, and Bot Dialog templates. For information about installing Visual Studio, see [Install Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio). 

> [!NOTE]
> The Bot Builder SDK for .NET currently supports C#. Visual Studio for Mac is not supported.

For either a Mac or PC environment, install the [Bot Framework Emulator](https://docs.microsoft.com/en-us/bot-framework/debug-bots-emulator) to be able to view and test your bot in action before registering it and connecting it to the Cortana channel.

If you are developing your skill on a Mac, or developing for an iOS, Android, or Harman Kardon Invoke device, you also need to set up the device where Cortana invokes the skill. Since Cortana is not available in a Mac environment, skills developed in a Mac environment must be invoked on a mobile device or in a virtual machine environment running Windows.

## Step 3 - Set up your Cortana device

To set up your iOS or Android device to invoke a Cortana skill, download the Cortana app from the device's app store, and then log in to Cortana using the same Microsoft account that you used to register the skill. Since Cortana is built-in to the Harman Kardon Invoke device, you only need to log in to Cortana using the Microsoft account used to register the skill.

## Step 4 - Set up Cortana

Finally, make sure Cortana is set up to work with your skill:

* Make sure you are logged in to Cortana on your computer or device with your Microsoft account.
* Make sure the microphone on your computer or device is set up and working so that you can speak to Cortana.
* Optionally, set debug mode in the [Cortana Developer Center](https://developer.microsoft.com/cortana). When you invoke a Cortana skill in debug mode, Cortana gives you additional information that you can use fine-tune how the skill works.



