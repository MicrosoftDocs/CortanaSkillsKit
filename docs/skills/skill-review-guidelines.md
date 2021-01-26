---
title: Cortana Skills Publishing Review Guidelines
description: Describes the requirements for publishing a skill to the world.
ms.assetid: 6dad0848-3886-4729-90fa-0bcd424b3561
ms.date: 12/28/2018
ms.topic: article
keywords: cortana
--- 

# Cortana skills certification requirements

This document describes the guidelines and requirements used by Microsoft to review your skill submission. We use these guidelines to ensure a diverse catalog of high-quality, engaging Cortana Skills for customers worldwide. After your skill is reviewed and approved, you may make it publicly available through Cortana across all Cortana endpoints.

## 1. Guiding Principles

Adhering to these guidelines will enhance your skill’s appeal and audience.

### 1.1 Offer as much value to your user as you can using voice

Users interact with Cortana through natural language conversation. You should use natural interactions to reduce complexity as much as possible.

Your skill provides value if using your skill is faster, easier, more novel, or more natural to use than the alternatives. Designing your skill based on scenarios that make your skill stand out in these ways will help you meet this guideline.

### 1.2 Don’t mislead the user

Don't mislead users about your skill or your skill’s capabilities. Present your skill in a way that helps users understand what it does and how to use it. Microsoft will not publish, and may take down, skills that purposefully attempt to mislead users.

### 1.3 Don’t attempt to cheat customers, the system, or the ecosystem.

There is no place in Cortana for fraudulent, manipulative, or malicious skills.

## 2. General Guidelines

<a name="2.1-distinct-function-and-accurate-representation"></a>
### 2.1 Distinct function and accurate representation

#### 2.1.1 

Your skill should accurately describe its functions, features, and any important limitations it has, including required or supported input devices.

#### 2.1.2

Your skill may not use a name or icon similar to that of any other skills. Also, your skill may not claim to be from a company,government body, or other entity if you don't have permission from them to make that claim.

#### 2.1.3

Your skill must be fully functional, and must provide appropriate functionality for each targeted device family.

#### 2.1.4

Your skill submission keywords may not exceed seven unique terms. Each of them should be relevant to your skill.

#### 2.1.5

Your skill submission must use distinct and informative description, sample utterances, and other related metadata like category descriptors.

#### 2.1.6

Invocation names must be unique, readily identifiable words. Invocation names may include prepositions (for example, "of", "to", "for"), or articles (for example, "this", "that", "the") but the names may not consist only of prepositions or articles.

#### 2.1.7

The skill profile image, name, keywords, and description must NOT:

- Be offensive or explicit.
- Include third party trademarks, service marks, or logos that you do not have the rights to use.
- Impersonate or imply endorsement by a third party that has not endorsed your skill.
- Use names unrelated to the skill.
- Use Microsoft logos, trademarks, or service marks unless you have permission from Microsoft.
- Be too long or verbose. The description should be 8-10 words.

#### 2.1.8

Invocation names should not conflict with, or attempt to override, the invocation phrases of existing Cortana functionality. For example, the invocation name "AskMicrosoft" conflicts with the supported invocation phrase "Ask" since the user would have to say, "Hey Cortana, ask AskMicrosoft" in order to invoke your skill.

#### 2.1.9

Invocation names and titles should not include "Microsoft", "Windows", "Cortana", or any other trademarks of Microsoft.

Additionally, avoid using the term "bot" in the invocation name, because it's not user friendly for Cortana users. It can also be confused with Microsoft's use of the term “bot.”

#### 2.1.10

Invocation names and skill names (titles) should not consist of proper nouns, names, or places unless you have exclusive rights to use that name in a commercial application.


#### 2.1.11

 Microsoft will review your skill to confirm that it meets certain minimum requirements prior to publication in the Cortana Skills Store. However, you are solely responsible for: (1) your skill; (2) its content and actions; (3) compliance with all applicable laws; and (4) compliance with the Cortana Skills Kit Program Agreement (the agreement you agreed to when you signed up in the Cortana dev center the first time), Privacy Statement, Cortana Skills Kit Review Guidelines and other documentation related to the Cortana Skills Kit Program. Microsoft's review and publication of your skill to the Cortana Skills Store is not an endorsement of your skill.

### 2.2 Security

Your skill must not jeopardize or compromise user security, or the security or functionality of Cortana services, the device the Cortana services are offered on, system, or related systems.

#### 2.2.1 

Your skill must not attempt to change or extend the described functionality through any form of dynamic inclusion of code that is in violation of Cortana Skills Kit Review Guidelines. For example, your skill’s associated service should not prompt a user to download a remote executable and subsequently execute that executable in a manner that is not consistent with the described functionality of your skill.

#### 2.2.2 

Your skill’s service must not contain or enable malware as defined by the Microsoft criteria for [malware and potentially unwanted applications](https://www.microsoft.com/security/portal/mmpc/shared/objectivecriteria.aspx).

#### 2.2.3

Your skill must operate as described in its description, profile, terms of service, and privacy policy. You must notify Microsoft in advance if you make any substantial, material changes to your skill or related service. Such changes will require a review. Microsoft has the right, in its sole discretion, to intermittently review skills in the Cortana Skills Store and remove skills from the Cortana Skills Store without notice.

### 2.3 Skill is Testable

The skill must be testable. If it is not possible to test your skill for any reason, including but not limited to the items below, your skill may fail this requirement.

#### 2.3.1

If your skill requires login credentials, provide us with a working demo account using the `Notes to Tester` field.

#### 2.3.2 

If your skill requires access to a server, the server must be functional. 

### 2.4 Usability

#### 2.4.1

Your skill should provide an appropriate experience across all Cortana endpoints, even when that endpoint does not support rich, visual interaction. If your skill offers experiences that make no sense on limited-capability devices, then it should provide a graceful failure experience on these types of devices. For example, if your skill requires showing a hero card for a sensible interaction, your skill might say "Sorry, I need a screen for that" when invoked on a standalone speaker device with no screen.

#### 2.4.2 

Your skill should be responsive. The user should not have to wait long periods of time for your skill to respond to an interaction. A good guideline is that responses should take no longer than 5 seconds to generate.  

#### 2.4.3

Your skill should attempt to properly manage the state of the conversation. For example, if your skill is centered around a "question and answer" scenario, then your skill should appropriately end the conversation.

#### 2.4.4

Your skill should follow Cortana and Bot Framework suggested practices for conversational and interactive design. For Cortana guidance, see [Understanding types of conversations](./mva31-understanding-conversations.md).

#### 2.4.5

Skills must not include in-conversation advertisements. Some exceptions apply. You should work directly with Microsoft if you intend to add advertisements in your skill experience.

### 2.5 Personal Information

#### 2.5.1 

The Cortana Skills Kit Program may enable you to receive personal information from users, with the user’s consent. Microsoft and Cortana take privacy very seriously. For this reason, all skills must maintain a privacy policy. You must provide users with access to your privacy policy by entering the privacy policy URL in the Cortana Skills Portal when you publish your skill. Your privacy policy must inform users of the personal information accessed, collected, or transmitted by your skill; how that information is used, stored,and secured; and indicate the types of parties to whom it is disclosed. It must describe the controls that users have over the use and sharing of their information, how they may access their information, and it must comply with all applicable laws and regulations. Your privacy policy must be kept up to date as you add new features and functionality to your skill.

#### 2.5.2 

You may publish the personal information of customers of your skill to an outside service or third party through your skill or its metadata only after obtaining opt-in consent from those customers. Opt-in consent means the customer gives their express permission in the skill's user interface for the requested activity, after you have:

* Described to the customer how the information will be accessed, used, or shared, indicating the types of parties to whom it is disclosed, and
* Provided the customer a mechanism in the Cortana interface through which they can later rescind this permission and opt-out.

#### 2.5.3 

If you publish a person’s personal information to an outside service or third party through your skill or its metadata, but the person whose information is being shared is not a customer of your skill, you must obtain express written consent to publish that personal information, and you must permit the person whose information is shared to withdraw that consent at any time. If your skill provides a customer with access to another person’s personal information, this requirement would also apply.

#### 2.5.4 

If your skill collects, stores, or transmits personal information, it must do so securely, by using modern cryptography methods.

#### 2.5.5 

Your skill must not collect, store, or transmit highly sensitive personal information, such as health or financial data through Cortana.

#### 2.5.6

Your skill must not collect, store, or transmit personal information unrelated to its primary purpose, without first obtaining express user consent.

#### 2.5.7

If your skill requires a user account specific to your service, you must utilize the Cortana Skills Kit Connected Accounts feature.

#### 2.5.8

If you configured Cortana's channel to receive access to user profile and contextual data, Microsoft will get the user’s permission to share this information with your skill prior to the user running your skill for the first time. You should not store or retain this data unless you have consent from the user, and you provide the user a way to revoke consent and request that you remove or delete this data.

#### 2.5.9

Your skill must follow the following guidelines when collecting personal information:

| Data Type | Guideline |
|-----------|-----------|
| Personal and Identifying Information | You may use user information that is stored and shared through available skills kit APIs and the Cortana profile, so long as you expressly request consent for transfer of this data (this is enabled through the Cortana channel configuration). Your skill may not collect any other personal information through Cortana (but you may collect data through your own services or apps that the skill uses, within the terms of your own end-user agreements). |
| Payment Mechanisms | Your skill may not prompt for payment mechanisms or configuration through a Cortana skill.<br/><br/>Your skill may defer the payment to another mechanism (like an app or website) as long as it doesn’t use the skills kit infrastructure to complete the payment operation.<br/><br/>Additionally, your users may create and set up payment methods through other apps or sites that you may own, and associate them with your skill. |
| Authentication and Authorization | Your skill should only use mechanisms provided by the Cortana Skill API to authenticate or authorize users.<br/><br/>However, as added protection, your skill may ask for an identifying PIN. This PIN should not be used by your service for functionality other than the Cortana Skill. |
| Health Data | The Cortana Skills Kit Program and underlying platform does not meet data handling requirements of HIPAA (Health Insurance Portability and Accountability Act), as amended, or other related regulations. Do not allow your skill to collect personal health-related information regulated under these laws. |

<!-- PII: where's this enabled in the "skills kit platform"? A. bot framework, cortana channel configuration page-->
<!-- Need to understand what Payment Mechanism says before i can clean it up. -->

#### 2.5.10

Your skill should not request more data from users than is necessary to fulfill the request.

#### 2.5.11

Your skill must not share or sell user data collected through skills unless the user has granted you rights to do so and is educated on how to revoke these rights.

<!-- How's this related to 2.5.2 and 2.5.3? -->

#### 2.5.12

All Cortana Skills require a privacy policy and defined terms of service. Microsoft has provided guidelines that may help you comply with these requirements ([Privacy policy](privacy-policy-guidelines.md) and [Terms of Use](terms-of-use.md)). You agree to assume all risk and liability arising from your use of these resources, and that Microsoft is not responsible for any issues arising out of your use of them.

The privacy policy and terms of service must be publicly available, and accessible to any user. Web pages are the preferred method of delivery. Users should not be required to download documents containing the policy or terms, as this could violate the security guidelines described in section [2.2 Security](#22-security) of this document.

### 2.6 Localization

You must localize your skill within the Cortana Skills Portal for all languages that the skill supports. The text of your skill’s description must be localized in each language that you declare. If your skill is localized such that some features are not available in a localized version, you must clearly state or display the limits of localization in the skill's description. The experience provided by a skill must be reasonably similar in all languages that it supports.

Currently, the only locale that the Cortana Skills Kit platform supports is en-US.

### 2.7 Other Guidelines 

#### 2.7.1 

Keep your Microsoft account email active because Cortana use it for all correspondence.

#### 2.7.2 

Your skill must not contact or attempt to integrate emergency services or support.

#### 2.7.3 

Your skill must not clone or duplicate another skill.

#### 2.7.4 

If your skill includes human interaction with end users (for example, customer service or user support), you must provide notice to users of this fact prior to the skill’s first interaction with the user.

#### 2.7.5 

You must have a way for your users to report abuse to you (a contact email address will suffice), and for you to handle access and deletion requests (for example, if someone deletes their account and wants all their data deleted as well).

## 3. Content Guidelines

The following guidelines apply to content and metadata offered for distribution in the Cortana Skills Store. Content means your skill name, publisher name, skill icon, skill description, the images, sounds, videos and text contained in the skill, the tiles, notifications, error messages exposed through your skill, and anything that’s delivered from a server or that your skill connects to. Because skills and the Cortana Skill Store are used around the world, these requirements will be interpreted and applied in the context of regional and cultural norms.

Metadata and other content you submit to accompany your skill may contain only content that would merit an [Entertainment Software Rating Board (ESRB)](https://www.esrb.org/ratings/ratings_guide.aspx) rating of ESRB EVERYONE 10+ or lower, or a [Pan European Game Information (PEGI)](https://pegi.info/) rating of 12 or lower.

### 3.1 Content Including Names, Logos, Original and Third Party

All content in your skill and associated metadata must be either originally created by the skill provider, appropriately licensed from the third-party rights holder, used as permitted by the rights holder, or used as otherwise permitted by law.

### 3.2 Harm to Others

Your skill must not contain any content that facilitates or glamorizes extreme or gratuitous violence, human rights violations, or the creation or illegal use of weapons against a person or animal in the real world.

### 3.3 Defamatory, Libelous, Slanderous and Threatening

Your skill must not contain any content that is defamatory, libelous, slanderous, or threatening.

### 3.4 Offensive Content

Your skill and associated metadata must not contain potentially sensitive or offensive content. Content may be considered sensitive or offensive in certain countries/regions because of local laws or cultural norms. In addition, your skill and associated metadata must not contain content that advocates discrimination, hatred, or violence based on considerations of race, ethnicity, national origin, language, gender, age, disability, religion, sexual orientation, status as a veteran, or membership in any other social group.

### 3.5 Alcohol, Tobacco, Weapons and Drugs

Your skill must not contain any content that facilitates or glamorizes excessive or irresponsible use of alcohol or tobacco products, drugs, or weapons.

### 3.6 Adult Content

Your skill must not contain or display content that a reasonable person would consider pornographic or sexually explicit, or content that drives traffic to pornography sites.

### 3.7 Illegal Activity

Your skill must not contain content or functionality that encourages, facilitates, or glamorizes illegal activity in the real world.

You are solely responsible for determining the legality of your skill in its targeted locale. Microsoft will remove any skills determined to be unlawful in locations where they are published.

### 3.8 Excessive Profanity and Inappropriate Content

Your skill must not contain excessive or gratuitous profanity, or contain or display content that a reasonable person would consider to be obscene.

### 3.9 Gambling

Your skill must not facilitate or promote online gambling services, including but not limited to, online casinos, sports betting, lotteries, or games of skill if they offer prizes of cash or other value.

### 3.10 Health

Your skill must not represent itself as, or provide services as, a health care provider, a health plan, or a health care clearinghouse or collect information regulated under HIPAA (Health Insurance Portability and Accountability Act) or other relevant laws. If your skill provides health information, you should also provide a disclaimer in your skill description that adequately discloses to the user that such information is not a substitute for advice from a medical professional. Skills providing fitness functionality, including activity monitoring (calories burned, steps taken, etc.), weight data, and BMI (body mass index) are allowed.

### 3.11 Spam

Your skill must not spam users in any way. Spam may include skills whose primary purpose is to drive traffic to a website or app rather than provide a useful function to the user, or skills that push content to a user's mobile devices or email without the user's permission.

### 3.12 Country/Region Specific Requirements

Skills may not contain content that is offensive in any country or region that it targets. Content may be considered offensive in certain countries or regions because of local laws or cultural norms. The skills kit is only supported in the US at this time.

### 3.13 Promotion

Skills must not directly or indirectly engage in or benefit from promotional practices that are deceptive or harmful to users or the developer ecosystem. This includes, for example, using deceptive ads on websites, apps, or other properties, including notifications that are similar to system notifications and alerts; engaging in unsolicited promotion via SMS services; offering compensation for enabling skills, including money, digital or physical goods.

### 3.14 Termination

If these Cortana Skills Kit Review Guidelines are not followed, Microsoft reserves the right, at its sole discretion and without any obligation to do so, to review and remove content and to terminate your skill from Cortana Services and remove you from the Cortana Skill Store.

<!-- By "...and remove you from the Cortana Skill Store", do you mean remove the skill from the store, or remove all of their skills from the store?  -->