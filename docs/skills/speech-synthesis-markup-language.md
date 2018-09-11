---
title: Speech Synthesis Markup Language (SSML) Reference
description: Overview of the SSML schema used by Cortana.
author: richbrun
label: Conceptual
ms.assetid: 3f37e309-3170-4896-8434-33bdce3c1889
ms.author: wdg-dev-content
ms.date: 04/4/2017
ms.topic: article
ms.prod: cortana
keywords: cortana
---


# Speech Synthesis Markup Language (SSML) reference

SSML is an XML-based markup language that skill developers use to specify the speech text that Cortana translates to speech. Using SSML improves the quality of synthesized content over sending Cortana plain text. SSML handles normal punctuation, such as pausing after a period, or speaking a sentence that ends with a question mark as a question. However, in some cases, you may want additional control over various characteristics of synthetic speech or text-to-speech (TTS)output, including pitch, rate, volume, pronunciation, and other characteristics. 

Cortana's implementation of SSML is based on World Wide Web Consortium's [Speech Synthesis Markup Language Version 1.0](http://www.w3.org/TR/speech-synthesis/). 

For information about using SMML in your skill, see Add speech to messages in [Node.js](https://docs.microsoft.com/en-us/bot-framework/nodejs/bot-builder-nodejs-text-to-speech) and [.NET](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-text-to-speech).

<!--In addition to this Cortana also supports a subset of the [Emotion Markup Language (EmotionML)  Version 1.0](http://www.w3.org/TR/emotionml/) and []().-->

<!--
## Using SSML in your Cortana Skill
-->
<!-- Both Bot Framework //TODO: AIT and Alexa imported--> 
<!-- Cortana skills support SSML as a way to customize the speech output of Cortana when conveying the response from your skill to the user.-->

<!-- //TODO: AIT
Custom skills imported from Alexa can use SSML in the `outputSpeech` property of the response and Reprompt objects when the `outputSpeech` type property is set to SSML. For example: 

```json
"outputSpeech": {
    "type": "SSML",
    "ssml": "<speak>Hello World on <say-as interpret-as=\"date\" format=\"mdy\"> 4/10/2017 </say-as></speak>"
}
```
-->

The following are the SSML elements that Cortana supports. The **speak** element is **Required.** All other elements are optional.

* [audio](#audio-Element) - Inserts recorded audio files.
* [break](#break-Element) - Inserts pauses between words.
* [p and s](#p-and-s-Elements) - Denotes the paragraph and sentence structure of the document.
* [phoneme](#phoneme-Element) - Indicates the phonetic pronunciation for the contained text. Overrides the pronunciations in the lexicon, if one is specified.
* [prosody](#prosody-Element) - Specifies the pitch, contour, range, rate, duration, and volume for speaking the element's text.
* [say-as](#say-as-Element) - Indicates the type of text contained in the element (such as acronym, number, and date).
* [speak](#speak-Element) - Required root element for the SSML document.
* [sub](#sub-Element) - Specifies a string of text to pronounce in place of the text contained in the element.

<!--* [**emphasis**](#emphasis-Element) - Indicates the level of stress (prominence) with which the contained text is spoken. 
<!--* [**lexicon**](#lexicon-Element) - Specifies a lexicon document that contains the pronunciations for the content of the document.
* [**mark**](#mark-Element) - Designates a specific reference point in the text sequence. This element can also be used to mark an output audio stream for asynchronous notification.-->

<!--
The following EmotionML tags are supported as children of the **speak** tag.

* emotion
* category

The Microsoft Text-To-Speech 

* audiosegment
* prompt
* setting
* soundeffect
* spectrum
* ttsmetadata-->

<a name="audio-Element"></a>
## **audio** element 

An optional element that you use to insert a recorded audio file.

**Syntax**

```XML
<audio src="string"/></audio>
```

**Attributes**

| Attribute | Description |
|-----------|-------------|
| src | **Required.** The URL for the audio file.  |


**Remarks**

Use this element to play an audio file. The body of the `audio` element may contain plain text or SSML markup that's spoken if the audio file is unavailable or unplayable. The body may also contain an `audio` element of another audio to play as a backup. 
 
The following are the requirements for audio:

* The MP3 must be hosted on an Internet-accessible HTTPS endpoint. HTTPS is required, and the domain hosting the MP3 file must present a valid, trusted SSL certificate. 
* The MP3 must be a valid MP3 file (MPEG v2).
* The bit rate must be 48 kbps. 
* The sample rate must be 16000 Hz.
* The combined total time for all text and audio files in a single response cannot exceed ninety (90) seconds.
* The MP3 must not contain any customer-specific or other sensitive information.
 
<!--
These settings are from Google Home. May add support for these in the future.
* Format: MP3 (MPEG v2)
  * 24K samples per second
  * 24K ~ 96K bits per second, fixed rate
* Format: Opus in Ogg
  * 24K samples per second (super-wideband)
  * 24K - 96K bits per second, fixed rate
* Format: WAV (RIFF)
  * PCM 16-bit signed, little endian
  * 24K samples per second
* For all formats:
  * Single channel is preferred, but stereo is acceptable.
  * No more than five audio files can be used in a single response.
  * The combined total time for all audio files in a single response cannot be more than ninety (90) seconds.
  * 5 megabyte file size limit.
  * Source URL must use HTTPS protocol.
  -->

**Usage**

The `audio` element may contain text and the following elements: `audio`, `break`, `p`, `phoneme`, `prosody`, `say-as`, `sub`, and `s`.

<!-- **emphasis**, **mark**, **voice**-->

**Example**
     
```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    <p>
        <audio src="https://example.com/opinionprompt.wav"/> 
        Thanks for offering your opinion. Please begin speaking after the beep. 

        <audio src="https://example.com/beep.wav"> 
        Could not play the beep, please voice your opinion now. </audio>
    </p>
</speak> 
```


<a name="break-Element"></a>
## **break** element  

An optional empty used to insert pauses between words.

**Syntax**

```XML
<break />
<break strength="string" />
<break time="string" />
```

**Attributes**

| Attribute | Description |
|-----------|-------------|
| strength | **Optional.** Specifies the relative duration of a pause using one of the following values:<ul><li>none</li><li>x-weak</li><li>weak</li><li>medium (default)</li><li>strong</li><li>x-strong</li></ul> |
| time | **Optional.** Specifies the absolute duration of a pause in seconds or milliseconds. Examples of valid values are 2s and 500ms. |

**Remarks**

Use this element to override the default behavior of text-to-speech (TTS) for a word or phrase if the synthesized speech for that word or phrase sounds unnatural. Set `strength` to *none* to prevent a prosodic break which the speech synthesis engine would otherwise insert. 

**Example**
     
```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    <sentence>
        The phone number is one eight hundred <break strength="weak" /> 
        five five five <break time="500ms" /> one two three four.
    </sentence>
</speak>
```

<!--
### emphasis Element  

An optional element that indicates the level of stress (prominence) with which the contained text is spoken. 

**Syntax**

```XML
<emphasis level="string"></emphasis>
```

**Attributes**

| Attribute | Description |
|-----------|-------------|
| **level** | Indicates the strength of emphasis to be applied, using one of the following enumeration values:<br/><br/> •	*strong*<br/> •	*moderate* (default)<br/> •	*none*<br/> •	*reduced* |

**Usage**

The **emphasis** element can only contain text to be rendered and the following elements: **audio**, **break**, **emphasis**, **mark**, **phoneme**, **prosody**, **say-as**, **sub**, and **voice**.



<!--
### lexicon Element  

An optional element that specifies a lexicon document that contains the pronunciations for the content of the document.

**Syntax**

```XML
<lexicon uri=lexiconUri type=mediaType />
```

**Attributes**

| Attribute | Description |
|-----------|_------------|
| **uri** | **Required.** Specifies the location of the pronunciation lexicon, which is a relative URI or an absolute URI. |
| **type** | **Optional.** Specifies the media type of the pronunciation lexicon document. System.Speech currently supports two values. The value *application/pls+xml* indicates that the lexicon conforms to the *Pronunciation Lexicon Specification (PLS) Version 1.0 specification*. This is the preferred format to use. The value *application/vdn.ms-sapi-lex* indicates the lexicon format is "Uncompressed Lexicon", which was created by Microsoft. This is a legacy format and we recommend that you use the PLS format. |

**Remarks**

A pronunciation lexicon is a collection of words or phrases together with their pronunciations, which consist of letters and characters from a supported phonetic alphabet. You can use lexicons to create custom pronunciations for specialized vocabulary in your application. Pronunciations specified in an external lexicon file take precedence over the pronunciations of the speech synthesizer's internal lexicon or dictionary. However, pronunciations specified inline in prompts using the **phoneme** element take precedence over pronunciations specified in any lexicon. Inline pronunciations apply only to a single occurrence of a word. 

The **lexicon** element is an immediate child of the **speak** element. Multiple **lexicon** elements can occur in an SSML document. If there are references to multiple lexicons, the order in which they are listed dictates their priority. Speech synthesis (TTS) engines use lexicons of higher priority first when determining which pronunciations to use.

The pronunciation information provided by a lexicon is specific to the single language declared in the **xml:lang** attribute of the **speak** element, and is used only for content defined within the enclosing SSML document.

**Note:** The **lexicon** element must occur before all other elements and text contained within the root **speak** element. There are no other ordering constraints on the elements in this specification.

**Example**

The following example specifies a lexicon that defines a pronunciation for an uncommon word: *whatchamacallit*. Typically, you would use the **phoneme** element to specify a pronunciation for a single occurrence of an uncommon word. However, this example demonstrates how to attach a lexicon to an SSML prompt and how the pronunciation defined in a lexicon may improve the speech synthesizer's pronunciation of an uncommon word. A custom lexicon overrides the pronunciations in the speech synthesizer's internal lexicon and applies to all occurrences of the words it defines.

```XML
<?xml version="1.0"?>
<speak version="1.0"
    xmlns="http://www.w3.org/2001/10/synthesis"
    xml:lang="en-US"> 
    <lexicon uri="https://Test/whatchamacallit.pls" type="application/pls+xml"/>  
    Gimme the whatchamacallit.
</speak>
```

The following are the contents of the SSML prompt file, **whatchamacallit.pls**.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<lexicon version="1.0" 
    xmlns="http://www.w3.org/2005/01/pronunciation-lexicon"
    alphabet="x-microsoft-ups" xml:lang="en-US">
    <lexeme>
        <grapheme>whatchamacallit</grapheme>
        <phoneme>W S1 AX T CH AX M AX K S2 AA L IH T</phoneme>
    </lexeme>
</lexicon>
```

### mark Element  

An optional element that designates a specific reference point in the text sequence. This element can also be used to mark an output audio stream for asynchronous notification.

**Syntax**

```XML
<mark name="string" />
```

**Attributes**

Attribute | Description 
--- | ---
    **name** | **Required.** Identifies the name of the **mark** element. The value is a *string*.


**Remarks**

Use the empty **mark** element to insert a marker into an output stream to trigger asynchronous notification.

When the application reaches the **mark** element, the text-to-speech engine raises an event that includes the value for the **name** attribute of the element. In **System.Speech**, the speech synthesizer raises a **BookmarkReached** event when it encounters a **mark** element. 

The **mark** element does not affect the speech output process.

**Example**

```XML
<speak>
    <s>We guarantee that your call will be answered in less than three minutes. <mark name="beginWait" /></s>
</speak>
```
-->



<a name="p-and-s-Element"></a>
## **p** and **s** elements  

Optional elements that denote the paragraph or sentence structure of the document.

**Syntax**

```XML
<p></p>
<s></s>
```

**Remarks**

The speech synthesis (TTS) engine automatically determines the structure of the document in the absence of these elements. A speech synthesis engine may produce changes in prosody when it encounters a `p` or `s` element. 
 
**Usage**

The `p` element may contain text and the following elements: `audio`, `break`, `phoneme`, `prosody`, `say-as`, `sub`, and `s`.

The `s` element may contain text and the following elements: `audio`, `break`, `phoneme`, `prosody`, `say-as`, and `sub`.

<!-- **emphasis**, **mark**, **voice**-->

**Example**

```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    <p>
        <s>Introducing the sentence element.</s>
        <s>Used to mark individual sentences.</s>
    </p>
    <p>
        Another simple paragraph.
        Sentence structure in this paragraph is not explicitly marked.
    </p>
</speak>
```



<a name="phoneme-Element"></a>
## **phoneme** Element  

An optional element that specifies the phonetic pronunciation for the specified text using phones from a supported phonetic alphabet.

**Syntax**

```XML
<phoneme alphabet="string" ph="string"></phoneme>
```

**Attributes**

| Attribute | Description |
|-----------|-------------|
| alphabet | **Optional.** Specifies the phonetic alphabet to use when synthesizing the pronunciation of the string in the `ph` attribute. The string specifying the alphabet must be specified in lowercase letters. The following are the possible alphabets that you may specify.<ul><li>ipa &ndash; International Phonetic Alphabet</li><li>sapi &ndash; Speech API Phone Set</li><li>ups &ndash; Universal Phone Set</li></ul>The alphabet applies only to the containing phoneme. For more information, see [Phonetic Alphabet Reference](https://msdn.microsoft.com/en-us/library/hh362879(v=office.14).aspx). |
| ph |  **Required.** A string containing phones that specify the pronunciation of the word in the `phoneme` element. If the specified string contains unrecognized phones, the text-to-speech (TTS) engine rejects the entire SSML document and produces none of the speech output specified in the document. |

**Remarks**

Phonetic alphabets are composed of phones, which consist of letters, numbers or characters, sometimes in combination. Each phone describes a unique sound of speech. This is in contrast to the Latin alphabet, where any letter may represent multiple spoken sounds. Consider the different pronunciations of the letter "c" in the words "candy" and "cease", or the different pronunciations of the letter combination "th" in the words "thing" and "those". 

**Usage**

The `phoneme` element may contain only text (no elements). You should always include human-readable text for this element that Cortana displays when she cannot play the SSML as audio.

<!-- what "text element" is it talking about? -->

**Example**

```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    <s>His name is Mike <phoneme alphabet="ups" ph="JH AU"> Zhou </phoneme></s>
</speak>
```



<a name="prosody-Element"></a>
## prosody element  

An optional element that specifies the pitch, contour, range, rate, duration, and volume for speaking the element's text. 

**Syntax**

```XML
<prosody pitch="value" contour="value" range="value" rate="value" duration="value" volume="value"></prosody>
```

**Attributes**

| Attribute | Description | 
|-----------|-------------|
| pitch | **Optional.** Indicates the baseline pitch for the text. You may express the pitch as:<ul><li>An absolute value, expressed as a number followed by "Hz" (Hertz). For example, 600Hz.</li><li>A relative value, expressed as a number preceded by "+" or "-" and followed by "Hz" or "st", that specifies an amount to change the pitch. For example: +80Hz or -2st. The "st" indicates the change unit is semitone, which is half of a tone (a half step) on the standard diatonic scale.</li><li>A constant value:<ul><li>x-low</li><li>low</li><li>medium</li><li>high</li><li>x-high</li><li>default</li></ul></li></ul>.
| contour | **Optional.** Represents changes in pitch for speech content as an array of targets at specified time positions in the speech output. Each target is defined by sets of parameter pairs. For example: <br/><br/>`<prosody contour="(0%,+20Hz) (10%,-2st) (40%,+10Hz)">`<br/><br/>The first value in each set of parameters specifies the location of the pitch change as a percentage of the duration of the text. The second value specifies the amount to raise or lower the pitch, using a relative value or an enumeration value for pitch (see `pitch`). 
| range  | **Optional.** A value that represents the range of pitch for the text. You may express `range` using the same absolute values, relative values, or enumeration values used to describe `pitch`.
| rate  | **Optional.** Indicates the speaking rate of the text. You may express `rate` as:<ul><li>A relative value, expressed as a number that acts as a multiplier of the default. For example, a value of *1* results in no change in the rate. A value of *.5* results in a halving of the rate. A value of *3* results in a tripling of the rate.</li><li>A constant value:<ul><li>x-slow</li><li>slow</li><li>medium</li><li>fast</li><li>x-fast</li><li>default</li></ul></li></ul>
| duration  | **Optional.** The period of time that should elapse while the speech synthesis (TTS) engine reads the text, in seconds or milliseconds. For example, *2s* or *1800ms*.
| volume  | **Optional.** Indicates the volume level of the speaking voice. You may express the volume as:<ul><li>An absolute value, expressed as a number in the range of 0.0 to 100.0, from *quietest* to *loudest*. For example, 75. The default is 100.0.</li><li>A relative value, expressed as a number preceded by "+" or "-" that specifies an amount to change the volume. For example +10 or -5.5.</li><li>A constant value:<ul><li>silent</li><li>x-soft</li><li>soft</li><li>medium</li><li>loud</li><li>x-loud</li><li>default</li></ul></li></ul> 

> [!NOTE]
> Standards for well-formed, valid XML require attribute values to be enclosed in double quotation marks. For example, `<prosody volume="90">` is a well-formed, valid element, but `<prosody volume=90>` is not.

**Remarks**

Because prosodic attribute values can vary over a wide range, the speech recognizer interprets the assigned values as a suggestion of what the actual prosodic values of the selected voice should be. The text-to-speech (TTS) engine limits or substitutes values that are not supported. Examples of unsupported values are a pitch of 1 MHz or a volume of 120. 

Phonetic alphabets are composed of phones, which consist of letters, numbers, or characters, sometimes in combination. Each phone describes a unique sound of speech. This is in contrast to the Latin alphabet where any letter may represent multiple spoken sounds. Consider the different pronunciations of the letter "c" in the words "candy" and "cease", or the different pronunciations of the letter combination "th" in the words "thing" and "those". 

Although the TTS engine ignores the content of the `phoneme` element (it pronounces only the string specified in the `ph` attribute), place text content in the element so that devices without speech capability can still render something intelligible in place of speech.

Although each attribute individually is optional, you must specify at least one attribute. 

**Usage**

The `prosody` element may contain text and the following elements: `audio`, `break`, `p`, `phoneme`, `prosody`, `say-as`, `sub`, and `s`.

<!-- **emphasis**, **mark**, **voice**-->

**Example**

```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    <s>
    Your order for <prosody pitch="+1st" rate="x-slow" volume="50">8 books</prosody> 
    will ship tomorrow.
    </s>
</speak>
```

<a name="say-as-Element"></a>
## **say-as** element  

An optional element that indicates the content type (such as number or date) of the element's text. This provides guidance to the speech synthesis engine about how to pronounce the text. 

**Syntax**

```XML
<say-as interpret-as="string" format="digit string" detail="string"> <say-as>
```

**Attributes**

| Attribute | Description | 
|-----------|-------------|
| interpret-as | **Required.** Indicates the content type of element's text. For a list of types, see the table below. | 
| format | **Optional.** Provides additional information about the precise formatting of the element's text for content types that may have ambiguous formats. SSML defines formats for content types that use them (see table below). |
| detail | **Optional.** Indicates the level of detail to be spoken. For example, this attribute might request that the speech synthesis engine pronounce punctuation marks. There are no standard values defined for `detail`. |

<!-- I don't understand the last sentence. Don't we know which one Cortana uses? -->

The following are the supported content types for the `interpret-as` and `format` attributes. Include the `format` attribute only if `interpret-as` is set to date and time.

| interpret-as | format | Interpretation |
|--------------|--------|----------------|
| address | | The text is spoken as an address. The speech synthesis engine pronounces:<br /><br />`I'm at <say-as interpret-as="address">150th CT NE, Redmond, WA</say-as>`<br /><br />As  "I'm at 150th court north east redmond washington." |
| cardinal, number | | The text is spoken as a cardinal number. The speech synthesis engine pronounces:<br /><br />`There are <say-as interpret-as="cardinal">3</say-as> alternatives`<br /><br />As "There are three alternatives." |
| characters, spell-out | | The text is spoken as individual letters (spelled out). The speech synthesis engine pronounces:<br /><br />`<say-as interpret-as="characters">test</say-as>`<br /><br />As "T E S T." |
| date  | dmy, mdy, ymd, ydm, ym, my, md, dm, d, m, y | The text is spoken as a date. The `format` attribute specifies the date's format (*d=day, m=month, and y=year*). The speech synthesis engine pronounces:<br /><br />`Today is <say-as interpret-as="date" format="mdy">10-19-2016</say-as>`<br /><br />As "Today is October nineteenth two thousand sixteen." |
| digits, number_digit | | The text is spoken as a sequence of indiviual digits. The speech synthesis engine pronounces:<br /><br />`<say-as interpret-as="number_digit">123456789</say-as>`<br /><br />As "1 2 3 4 5 6 7 8 9." |
| fraction | | The text is spoken as a fractional number. The speech synthesis engine pronounces:<br /><br /> `<say-as interpret-as="fraction">3/8</say-as> of an inch`<br /><br />As "three eigths of an inch." |
| ordinal  | | The text is spoken as an ordinal number. The speech synthesis engine pronounces:<br /><br />`Select the <say-as interpret-as="ordinal">3rd</say-as> option`<br /><br />As "Select the third option". |
| telephone  | | The text is spoken as a telephone number. The `format` attribute may contain digits that represent a country code. For example, "1" for the United States or "39" for Italy. The speech synthesis engine may use this information to guide its pronunciation of a phone number. The phone number may also include the country code, and if so, takes precedence over the country code in the `format`. The speech synthesis engine pronounces:<br /><br />`The number is <say-as interpret-as="telephone" format="1">(888) 555-1212</say-as>`<br /><br />As "My number is area code eight eight eight five five five one two one two." |
| time | hms12, hms24 | The text is spoken as a time. The `format` attribute specifies whether the time is specified using a 12-hour clock (hms12) or a 24-hour clock (hms24). Use a colon to separate numbers representing hours, minutes, and seconds. The following are valid time examples: 12:35, 1:14:32, 08:15, and 02:50:45. The speech synthesis engine pronounces:<br /><br />`The train departs at <say-as interpret-as="time" format="hms12">4:00am</say-as>`<br /><br />As "The train departs at four A M." |

**Usage**

The `say-as` element may contain only text.

**Example**

The speech synthesis engine speaks the following example as "Your first request was for one room on October nineteenth twenty ten with early arrival at twelve thirty five P M."
 
```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    <p>
    Your <say-as interpret-as="ordinal"> 1st </say-as> request was for <say-as interpret-as="cardinal"> 1 </say-as> room
    on <say-as interpret-as="date" format="mdy"> 10/19/2010 </say-as>, with early arrival at <say-as interpret-as="time" format="hms12"> 12:35pm </say-as>.
    </p>
</speak>
```

<a name="speak-Element"></a>
## **speak** element  

The root element of the SSML document. 

**Syntax**

```XML
<speak version="1.0" xmlns="http://www.w3.org/2001/10/synthesis" xml:lang="string"></speak>
```

**Attributes**

| Attribute | Description | 
|-----------|-------------|
| version | **Required.** Indicates the version of the SSML specification used to interpret the document markup. The current version is 1.0. | 
| xml:lang | **Required.** Specifies the language of the root document. The value may contain a lowercase, two-letter language code (for example, **en**), or the language code and uppercase country/region (for example, **en-US**).  |
| xmlns | **Required.** Specifies the URI to the document that defines the markup vocabulary (the element types and attribute names) of the SSML document. The current URI is http://www.w3.org/2001/10/synthesis. |

**Usage**

The `speak` element may contain only text and the following elements: `audio`, `break`, `p`, `phoneme`, `prosody`, `say-as`, `sub`, and `s`.

<!-- **emphasis**, **lexicon**, **mark**, **voice**-->

**Example**
     
```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    This is the text that is spoken by Cortana.
</speak>
```

<a name="sub-Element"></a>
## **sub** element  

An optional element that specifies a string of text that is pronounced in place of the element's text.

**Syntax**

```XML
<sub alias="string"></sub>
```

**Attributes**

| Attribute | Description | 
|-----------|-------------|
| alias    | **Required.** Specifies the substitute text to speak. |

**Remarks**

Before synthesizing a phrase, the text-to-speech (TTS) engine normalizes it. The normalization process converts symbols, numbers, and other non-orthographic entities into text representing the spoken value of these entities. For example, normalization converts "$1.99" into "one dollar and ninety-nine cents." 

Use a `sub` element to create a custom text value for any text element. Because the TTS engine processes `sub` elements before normalizing the phrase, the substitute text is normalized before being synthesized.

**Usage**

The `sub` element may contain only text (no elements).

**Example**

The following instructs the text-to-speech engine to pronounce the string "SAPI" as "Speech Application Programming Interface".

```XML
<speak version="1.0"
 xmlns="http://www.w3.org/2001/10/synthesis"
 xml:lang="en-US">
    <sub alias="Speech Application Programming Interface">SAPI</sub>
</speak>
```

