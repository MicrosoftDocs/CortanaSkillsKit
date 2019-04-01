---
title: Cortana invocation guidelines
description: Choose an invocation name that is easily spoken and readily recognized by the Cortana natural language speech engine.  
ms.assetid: 8887c784-abc1-434c-b0ef-01ec71ddf11d
ms.date: 04/01/2019
ms.topic: article
keywords: cortana
---

# Invocation name guidelines

The invocation name is an essential part of the natural language phrase or utterance that invokes your Cortana skill. Your invocation name must conform to the following requirements in addition to those found in section 2.1 of [Cortana Skills Kit Review Guidelines](skill-review-guidelines.md#2.1-distinct-function-and-accurate-representation).

### Avoid the term "bot" in the invocation name.

Avoid using the term "bot" in the invocation name because it's not user friendly for Cortana users. It can also be confused with Microsoft's use of the term “bot.”

### Avoid trademarked or copyrighted names.

Unless you have permission from the owner of a trademarked or copyrighted name, don't use it as an invocation name. If you do, your skill will probably not pass the publishing review.

All content in your skill and associated metadata must be either

- originally created by you (the skill provider)
- appropriately licensed from the third-party rights holder
- used as otherwise permitted by the rights holder
- or used as otherwise permitted by law.

### Must not be longer than three words.

An invocation name of more than three words is difficult to distinguish from the utterance.

### Avoid duplicate names.

Your skill must not clone or duplicate another skill. The name is verified when you configure your Cortana channel and specify your skills name. Duplicate names are rejected.

### Avoid the use of common proper nouns.

Invocation names and titles should not consist of proper nouns, names, or places unless you have exclusive rights to use that name in a commercial application.

## Invocation name recommendations

The following recommendations can improve recognition significantly.

### Specify a clear and easily recognized invocation name.​

When creating a language model, it is important that you define a "high quality" invocation name. If your invocation name is hard to pronounce or sounds similar to other words, Cortana might have difficulty recognizing it without introducing a disambiguation step. ​

### Avoid words that are homophones.​

Try not to include words that sound the same as another word but have different meanings like "peak/peek" or "wait/weight".  Also try to avoid overly-clever word plays that will cause collisions with common English words or phrases.​

### Use words with multiple syllables and invocation names with multiple words.​

Using invocation names with multiple syllables or words are easier to recognize.  ​

### Avoid compound words unless required for branding.

Compound words can be difficult to recognize.  

### Avoid hard to pronounce word​s.

An invocation name that contains difficult words to pronounce, such as Quinoa, makes it harder for your users to pronounce correctly, and for Cortana to understand.​

### Avoid names that combine multiple words into one.

An invocation name that combines multiple words into one increases the chance that Cortana will not recognize it. For example, instead of "sixSigma5," consider "six sigma 5" or "six sigma five".

### Prime speech recognition for your skill.

If your skill uses a Language Understanding Intelligence Service (LUIS) app from luis.ai, you can use the app to achieve optimal speech recognition performance when users invoke your skill. Although the system learns over time, seeding it with the highest probability intents leads to a better first experience. This in turn leads to greater usage and faster improvement of the system. ​For example, the user could ask your skill to play classical music in different ways with all of them returning the correct intent.

- Ask My Radio to play classical
- Ask My Radio to play classical music
- Ask My Radio for classical music
- Ask My Radio for some classical

<!-- This doesn't belong in a guidance doc. Check to see if it's elsewhere. 02/01/2019 (dt)
To specify your model:

1. Sign in to [Bot Framework](https://dev.botframework.com)
2. Click **My bots
3. Click your skill
4. Click **Settings
5. Scroll down and expand **Improve speech recognition through priming
6. Enter your LUIS app ID
7. Click **Save changes
 -->

## List of invocation phrases

Users invoke skills by saying an invocation phrase. The following are the invocation phrases that users may say to invoke your skill.

### Invocation phrase with connecting word

- Ask \<Invocation Name\> to \<Utterance\> 
- Ask \<Invocation Name\> about \<Utterance\> 
- Ask \<Invocation Name\> for \<Utterance\> 
- Ask \<Invocation Name\> if \<Utterance\> 
- Ask \<Invocation Name\> whether \<Utterance\> 
- Ask \<Invocation Name\> what about \<Utterance\> 
- Tell \<Invocation Name\> to \<Utterance\> 
- Tell \<Invocation Name\> that \<Utterance\> 
- Use \<Invocation Name\> to \<Utterance\> 
- Use \<Invocation Name\> and \<Utterance\> 
- Use \<Invocation Name\> for \<Utterance\> 
- Open \<Invocation Name\> for \<Utterance\> 
- Start \<Invocation Name\> to \<Utterance\> 
- Search \<Invocation Name\> for \<Utterance\> 
- Get \<Invocation Name\> to \<Utterance\> 
- Have \<Invocation Name\> send me \<Utterance\> 
- Have \<Invocation Name\> get me \<Utterance\> 
- Have \<Invocation Name\> find me \<Utterance\> 
- Have \<Invocation Name\> play me \<Utterance\> 
- Check \<Invocation Name\> for \<Utterance\> 
- Check \<Invocation Name\> if \<Utterance\> 
- See if \<Invocation Name\> has \<Utterance\> 
- See if \<Invocation Name\> can \<Utterance\> 

### Invocation phrase without user utterance

- Open \<Invocation Name\>
- Tell \<Invocation Name\>
- Ask \<Invocation Name\>
- Start \<Invocation Name\> 
- Launch \<Invocation Name\> 
- Run \<Invocation Name\> 
- Load \<Invocation Name\> 
- Begin \<Invocation Name\> 
- Use \<Invocation Name\> 
- Talk to \<Invocation Name\> 

### Invocation phrase without connecting word

- Ask \<Invocation Name\> \<Utterance\>
- Tell \<Invocation Name\> \<Utterance\>
- Use \<Invocation Name\>  \<Utterance\>
- Open \<Invocation Name\> \<Utterance\>
- Start \<Invocation Name\> \<Utterance\>
- Search \<Invocation Name\> \<Utterance\>