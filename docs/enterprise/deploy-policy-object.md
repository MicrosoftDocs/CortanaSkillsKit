---
title: Deploy the policy object
description: Manually deploying your new Cortana policy object. 

ms.date: 04/01/2019
ms.topic: article
ms.prod: cortana
ms.author: v-daturc

keywords: cortana
---  

# Deploy the policy object

<!-- This is kinda short. Can we merge it into one (or both) of the other policy sections? Or is there a reason that I don't know about to keep it separate?-->

To quickly apply the new policy, the members of the CortanaUser group can log into their machine and open a command prompt from the search box. Type `gpupdate` and the computer will pull the new policy settings to enable Cortana.  *You must restart the computer after running gpupdate*.

<!--So group members have to pull the policy? There's no way to push it? Also, does this happen automagically when the machine reboots?-->