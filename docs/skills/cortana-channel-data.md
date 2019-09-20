---
title: Get Cortana's channel data
description: Shows how to get the Cortana's channel data when your skill runs.
ms.assetid: 2C558B30-1B9B-445D-B190-56E1197E16E1
ms.date: 07/18/2019
ms.topic: article
keywords: cortana
---

# Get Cortana's channel data

Cortana and skills use the message's `channelData` property to pass Cortana-specific data. The `channelData` property is an object that contains the following properties: 

<!-- Verify whether all messages include skillId or just the first -->

| Name | Type | Description |
|-|-|-|
| skillId | string  | An ID that uniquely identifies the skill. This is regenerated for each deployment. For example, the ID may be 123 when the skill is deployed to self, and 656 when it's deployed to group. |
| skillProductId | string  | An ID that uniquely identifies the skill.  |
| isDebug | Boolean  | Specifies whether Cortana is in debug mode. If **true**, debugging is enabled and messages are written to her canvas. For more information, see [Enable debugging in Cortana](test-debug.md#enable-debugging-in-cortana). |
<!-- | currentAudioInfo | CurrentAudioInfo | A `CurrentAudioInfo` object that contains information about the audio stream that's playing. The channel data includes this property only if your skill is playing audio on a speaker-only device. For more information, see [Getting the playback state](audio-streaming.md#getting-the-playback-state).
 NOTE: This information was removed from the target document. 06/26/2019 -->

Here's an example of the `channelData` object that Cortana sends.

```json
{
  "skillId": "3253-fsafa-32522-afa3a",
  "skillProductId": "A7CDE-5DD1-42EA-A436-49D7365",
  "isDebug": true
}
```

In addition to using `channelData` to receive Cortana-specific information, you can include it in your skill's outgoing message to have Cortana launch an app or a website. For information, see [Launching apps or websites from a Cortana skill](launch-apps-from-skills.md).

## Next steps

These are some additional types of data that Cortana can send to your skill.

|Entity | Purpose | Refer to |
|-|-|-|
| `DeviceInfo` | Determine the type of device that Cortana is running on. | [Determine Cortana's device type](cortana-device-type.md) |
| `AuthorizationToken` | Get the access token for secured skills. | [Adding Authentication to Your Cortana Skill](authentication.md) |

Cortana messages can also include user profile information. For information, see [Get the user's profile and contextual information](get-user-profile-context.md).
