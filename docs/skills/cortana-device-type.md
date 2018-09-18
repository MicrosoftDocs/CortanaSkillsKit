---
title: Get Cortana's device type
description: Shows how to get the type of device that Cortana is running on.
author: richbrun
label: Tutorial

ms.assetid: BB5B2186-2EDF-4BBB-9C53-B5CE64B2E042
ms.author: wdg-dev-content
ms.date: 4/15/2017
ms.topic: article
ms.prod: cortana
keywords: cortana
---


# Determine Cortana's device type

Cortana sends the type of device that it's running on as part of the message that it sends your skill. The device information lets the developer tailor the conversation to the specific device’s capabilities. For example, if the user is on a standalone speaker device, and they need to sign into your app, your skill could ask them to sign in using the device's companion app. 

Each message contains an `entities` field, which is an array of objects. One of the objects is a `DeviceInfo` object with the following properties:

| Name | Type | Description 
|-|-|-
| supportsDisplay | Boolean  | Indicates whether the device has a screen. If **true**, the device has a screen; otherwise, **false**. If the user is using a headless device such as a standalone speaker, this value would be false. Otherwise it would be true. 
| type | string | The object's type, which is set to DeviceInfo. 

<!-- really should include the activity object in the example to give full context. -->

The following shows an example of the `DeviceInfo` object.

```json
{                          
    "type": "DeviceInfo",       
    "supportsDisplay": Boolean                              
}
```

