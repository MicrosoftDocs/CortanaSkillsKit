---
title: Known Issues
description: A list of known issues in the Cortana Skills Kit platform.
author: richbrun
label: Conceptual
ms.assetid: 3f37e309-3170-4896-8434-33bdce3c1889
ms.author: wdg-dev-content
ms.date: 03/30/2017
ms.topic: article
ms.prod: cortana
keywords: cortana
---

<!-- Need to confirm if these are still issue. -->

# Known Issues

Cortana Skills Kit is currently in preview. This document lists known issues, and if available, alternative solutions.

**Cortana Skills only works when language is set to English (United States)**

The public preview for Cortana is available for the en-US market only.

**Cortana stops talking after 15 seconds or displays the message, "Unfortunately this skill won't work on this version of Windows"**

Cortana in the Windows 10 Anniversary update (version 1607) limits speech to 15 seconds. This has been resolved in the Windows 10 Creators update (version 1703). A workaround is to break your speech text into multiple responses. You can send multiple replies to a single user invocation, as long as the input hint of the first N-1 replies is IgnoringInput. The last reply must set the input hint to ExpectingInput (which automatically turns the microphone on), or AcceptingInput (which doesn't).

**Long repetitive sentences without appropriate punctuation become garbled when spoken in the Windows 10 Creators Update**

If you have long text that is repetitive, the speech output from Cortana may be garbled. For example:

> This is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence this is a very long sentence 

<!-- By "next update of Windows," do you mean patch (Windows Update) or Release? -->
The next update of Windows resolves this issue. To work around this issue, ensure your SSML contains proper punctuations such as commas and periods.

**Privacy policy and terms of use links don't work in permission card when deployed to self or group**

When a skill is deployed to self or group, the privacy and terms of use links in the permission card don't work. The reason for this is that you are not required to specify these links until you publish your skill to world.

**Spoken utterances sometimes have punctuations appended**

<!-- Added "user's" to utterance. Confirm. -->

Cortana will sometimes append punctuation, such as a period, to the end of a user's utterance. The speech recognition engine is capable of understanding multiple sentences in a single speech request. The engine may add a period to an utterance depending on how the utterance is spoken. Make sure that your language model is designed to handle this.

**Unable to interrupt Cortana**
<!-- //TODO Test as this should be fixed soon -->

Currently Cortana does not support user's interrupting her when she is speaking. She also ignores clicking on her canvas while she is speaking.  

**User email address not available on iOS and Android**
<!-- Bug 737656 -->

Currently, the user's email address from the user's profile information is not available on iOS and Android.

**Windows Phone does not support login**
<!-- Bug 750050 -->

Currently, Cortana does not support logging into skills on Windows Phone. Log in using any other supported device first before using the skill on Windows Phone.

**"Coming soon" displayed on the Cortana dashboard**

This occurs when signed in with an organizational account that uses AAD. Sign-out and sign back in using a Microsoft account (MSA).



## Known Bot Framework issues affecting skills

See the [Bot Build SDK Issues tab on GitHub](https://github.com/Microsoft/BotBuilder/issues).

<!-- if this isn't getting fixed, this should be in a LUIS how-to topic. -->

**LuisDialog fails on skill launch**

When Cortana launches skill without an utterance (for example, "Open \<invocation name\>", "Ask \<invocation name\>"), the `activity.Text` value is null. Passing the null text to LuisDialog throws an error. To work around this issue, override the `MessageReceived` method and add a null check as shown in the following example:

```csharp
/// <summary>
/// Need to override the LuisDialog.MessageReceived method so it detects when the user invokes the skill without
/// specifying a phrase. For example, "Open Hotel Finder", or "Ask Hotel Finder". In these cases, the message receives an empty string.
/// </summary>
/// <param name="context"></param>
/// <param name="item"></param>
/// <returns></returns>
protected override async Task MessageReceived(IDialogContext context, IAwaitable<IMessageActivity> item)
{
    // Check for empty query
    var message = await item;
    if (string.isNullOrEmpty(message.Text))
    {
        // Return the Help/Welcome
        await Help(context, null);
    }
    else
    {
        await base.MessageReceived(context, item);
    }
}
```

<!-- //TODO: AIT
## Known Issues for Skills Imported from Alexa

*Third-party trademarks used herein are the property of their respective owners.  Use of such marks does not imply any affiliation, sponsorship, or endorsement.*

The following known issues are specific to skills that have been imported to Cortana from Alexa.

**Flash Briefing Skills**

Cortana does not currently does not provide a Flash Briefing Skill API.

**Implict Auth not supported**
<!-- Bug: 666796 -->
<!--
Implicit Auth is not currently supported, but is a planned feature.

**Smart Home Skills**

Cortana Skills currently does not provide a Smart Home Skill API. However, a custom Cortana skill can be created that connects to a home automation service. Here is an [example](https://www.codeproject.com/Articles/1117146/Creating-a-Smart-Home-Chat-Bot).

<a name="SSML-Alexa-Cortana-differences"></a>
**Not all SSML that works in Alexa works in Cortana**

The likely causes are as follows:

* Cortana supports [SSML v1.0](https://www.w3.org/TR/speech-synthesis/) while Alexa supports some [SSML v1.1](https://www.w3.org/TR/speech-synthesis11/) tags, primarily the [w](https://www.w3.org/TR/speech-synthesis11/#edef_word) tag.
* Alexa and Cortana support different phonetic alphabets for the phoneme tag:
  * Alexa: 
    * International Phonetic Alphabet (IPA)
    * Extended Speech Assessment Methods Phonetic Alphabet (X-SAMPA).
  * Cortana: 
    * International Phonetic Alphabet (IPA)
    * Speech API (SAPI) Phone Set
    * Universal Phone Set (UPS)
* Differences in support for the **interpret-as** property of the **say-as** tag. 
  * **unit**, **interjection** and **expletive** are not supported by Cortana.
  * **time** - both platforms support a *time* option however, Alexa interprets this for durations while Cortana interprets this as 12 or 24 hour times. 
  * **date** - both platforms support a *date* option however, Alexa allows dates to consist of simply a number (e.g. `<say-as interpret-as=”date”>121</say-as>`) while Cortana requires the date parameters to be seperated by a "-" or "." (e.g. `<say-as interpret-as=”date”>1.21</say-as>`) as this removes the potential ambiguity as `121` could mean "December 1st" or "January 21st".
* Alexa has a custom SSML tag `<amazon:effect name="whispered">` which is not supported by Cortana, however a similar effect can be achieved using the [prosody tag](../reference/ssml.md#prosody-Element).

**Not all built-in intents and entities supported by Alexa are available in Cortana**

See the [Built-in Intent and Entity Support](../tutorials/alexa-skill-import.md#Built-in-Intent-and-Entity-Support) section of the [Import your custom Alea skill to Cortana guide](../tutorial/alexa-skill-import.md) for details.

**Not all audio streaming features are supported**

Cortana does support audio streaming via the AudioPlayer and embedded MP3s in the SSML audio tag, however not all Alexa features are supported. See the [Audio Support](../tutorials/alexa-skill-import.md#audio-support) section of the Alexa import guide for more information.

**No SessionEndedRequest sent when user closes Cortana in Windows**
<!-- //TODO: should be fixed in RS3 Bug# 697923 -->
<!--
When a user closes Cortana in Windows while using your skill, a SessionEndedRequest is not sent to your skill. This will be addressed in a future Windows update.

**All built-in intents and entities used by all skills**

Currently, all built-in intents and entities are used by all skills, even if not defined in your skills interaction model. 
-->