---
title: Configure tenant publishing
description: Configuring the publishing process for enterprise skills.

ms.author: v-daturc
ms.date: 03/18/2019
ms.topic: article

keywords: cortana, enterprise, skills
---

# Configure tenant publishing

Once the skill is ready to be published, skill developers must complete the required fields on the tenant publish tab.

Many fields (like name and address) are self-explanatory, and will not be described here. Fields that may require more of a description will be described below.

## Skill information

![Tenant publishing screenshot](../media/images/TenantPub-08.png)

- Display Name (required) - Unique name that Cortana presents to the end user. Displayed in Directory, on Canvas Cards and in Bing Search
- Invocation Name (required) - Add a descriptive invocation name following the [Cortana Invocation Guidelines](https://docs.microsoft.com/en-us/cortana/skills/cortana-invocation-guidelines)
- Short description (required) - This description will show up in Cortana's Notebook.
- Long description (required) - This will be used as part of the certification process.
- Sample Invocation Phrase (required) - At least 3 examples, e.g. "Ask Outlook to show my urgent messages".
- Primary category (required) **<Sample categories?>**
- Secondary category (Optional)
- Tags (Optional) - These are used for consumer skills, but are ignored for enterprise skills.
- Supported platforms (required) - For enterprise skills, you must choose Windows 10.

## Developer Account

![Tenant publishing screenshot](../media/images/TenantPub-09.png)

You should always select `Company` for enterprise skills.
## Developer Information

![Tenant publishing screenshot](../media/images/TenantPub-07.png)

- Developer Account (required) - Developer  OR  Company
- First name (required)  - First Name of Microsoft Account owner
- Last name (required)  - Last Name of Microsoft Account owner
- Country (required) - 2 digit Country code. e.g. US; UK; CA; CN;

## Support Contact

![Tenant publishing screenshot](../media/images/TenantPub-06.png)

## Publisher information

![Tenant publishing screenshot](../media/images/TenantPub-05.png)

## Privacy policy and terms of use

![Tenant publishing screenshot](../media/images/TenantPub-04.png)

## Validation and testing instructions

![Tenant publishing screenshot](../media/images/TenantPub-01.png)

## Deployment Configuration

![Tenant publishing screenshot](../media/images/TenantPub-03.png)

- Deploy to entire tenant – publishes the enterprise skill to everyone
- Deploy to security groups – publishes the enterprise skill only to members of the associated security groups

>[!NOTE]
>In order for security groups to work, Cortana must be added as a service principal in your tenant by an IT administrator. See [Adding Cortana as a service principal](enterprise-cortana-service-principal.md) in the Appendix.

Once you've filled in all the required fields on the page, click `Submit for Review` to send the skill off to your administrators for certification. Alternatively, you can save this information at any point by pressing the `Save` button. Then you can return to the page and edit it at any time before you submit it for certification and publishing. Keep in mind that once it's submitted, the skill configuration cannot be changed.

![Tenant publishing screenshot](../media/images/TenantPub-02.png)
