---
title: Automatically Deploying Group Policy
description: Automating policy update pushes.

ms.date: 03/06/2019
ms.topic: article
ms.prod: cortana
ms.author: v-daturc

keywords: cortana enterprise
---  

# Automatically deploying group policy

You can automate the process of pushing policy updates by using Windows Update for Business (WUFP). For more information , see [Walkthrough: use Group Policy to configure Windows Update for Business](https://docs.microsoft.com/en-us/windows/deployment/update/waas-wufb-group-policy).

To immediately push the change to all computers:

1. Launch the Group Policy Management tool.
1. Right click on the `CortanaOU`.
1. Click `Group Policy Update…`, and follow the instructions.

For this to work, the Network policy for Windows Firewall `Allow remote administration exception` property needs to be enabled. RPC (port 135) needs to be running and accessible on the managed computer.