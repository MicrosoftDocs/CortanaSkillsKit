---
title: Cortana voice commands - Cortana UWP design and development
description: Extend the basic functionality of Cortana with voice commands that launch and execute a single action in an external application.
author: kbridge
label: Conceptual
ms.assetid: 18e45699-6f2f-431a-a4e7-7706171d1d8b
ms.author: wdg-dev-content
ms.date: 02/08/2017
ms.topic: article
ms.prod: cortana
keywords: cortana
---

# Cortana voice commands

Extend the basic functionality of **Cortana** with voice commands that launch and execute a single action in an external application.

**Other speech components**: See [Speech interactions](https://msdn.microsoft.com/windows/uwp/input-and-devices/speech-interactions) if integrating speech recognition and text-to-speech (also known as TTS, or speech synthesis) directly into your app.

> [!NOTE] 
> A voice command is a single utterance with a specific intent, defined in a Voice Command Definition (VCD) file, directed at an installed app through **Cortana**.

> A VCD file defines one or more voice commands, each with a unique intent.

> Voice command definitions can vary in complexity. They can support anything from a single, constrained utterance to a collection of more flexible, natural language utterances, all denoting the same intent.

The target app can be launched in the foreground (the app takes focus and **Cortana** is dismissed) or activated in the background (**Cortana** retains focus but provides results from the app), depending on the complexity of the interaction. For example, voice commands that require additional context or user input are best handled in a foreground app, while basic commands can be handled in **Cortana** through a background app. 

By integrating the basic functionality of your app, and providing a central entry point for the user to accomplish most of the tasks without opening your app directly, **Cortana** becomes a liaison between your app and the user. Providing this shortcut to app functionality and reducing the need to switch apps can save the user significant time and effort.

| Article | Description |
|--- | --- |
| [Voice command design guidelines](voicecommand-design-guidelines.md) | These guidelines and recommendations describe how your app can best use **Cortana** voice commands to interact with the user, help them accomplish a task, and communicate clearly how it's all happening. |
| [Activate a foreground app with voice commands](launch-a-foreground-app-with-voice-commands-in-cortana.md) | In addition to using voice commands within **Cortana** to access system features, you can also use voice commands through **Cortana** to launch a foreground app and specify an action or command to execute within the app. |
| [Dynamically modify VCD phrase lists](dynamically-modify-voice-command-definition-vcd-phrase-lists.md) | Learn how to access and update the list of supported phrases (**PhraseList** elements) in a VCD file using the speech recognition result at run time. |
| [Activate a background app with voice commands](launch-a-background-app-with-voice-commands-in-cortana.md) | In addition to using voice commands within **Cortana** to access system features, you can also extend **Cortana** with features and functionality from a background app using voice commands that specify an action or command to execute within the app. |
| [Interact with a background app](interact-with-a-background-app-in-cortana.md) | Learn how a user can interact with a background app through the **Cortana** voice and canvas during the execution of a voice command. |
| [Deep link to a background app](deep-link-into-your-app-from-cortana.md) | Provide deep links from the background app service in **Cortana** to launch the app to the foreground in a specific state or context. |
| [Support natural language voice commands](support-natural-language-voice-commands-in-cortana.md) | Learn how to extend **Cortana** with more flexible and natural voice commands, so a user can say your app's name anywhere in the command. |
<br />
## <span id="related_topics"></span>Related articles


* [VCD elements and attributes v1.2](https://msdn.microsoft.com/library/windows/apps/dn706593)

**Designers**
* [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121)
* [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233)

**Samples**
* [Cortana voice command sample](https://go.microsoft.com/fwlink/p/?LinkID=619899)
 

 




