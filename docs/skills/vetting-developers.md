---
title: Reviewing Cortana consumer skill developers
description: Describes the process for approving or rejecting third-party Cortana developers.
label: Conceptual

ms.date: 04/09/2019
ms.topic: article
ms.author: v-daturc@microsoft.com

keywords: cortana
---

# Reviewing Cortana consumer skill developers

## Developer settings

As a developer, you can create and test skills without filling in the Developer Settings page. The intent is to allow you to test your skills on your own before submitting them for approval. However, all developers need to be reviewed before they can configure a skill for group or world, both of which allow other people to use it. Developers must go through Microsoft's internal review process before they can access the group or world configuration pages. Once you're approved,  the Developer Settings tab displays an approval message, and the Group and World tabs are enabled.

All developer and publisher information is entered on a tab called `Developer Settings`, which appears on the Cortana Configuration page. The Microsoft Certification team will pass the data to the review team. The review results will be visible only to the Certification Team and the developer.

## Developer approval

The Group and World tabs remain disabled until the developer data is successfully processed and the developer is approved. Once you're approved, the Group and World tabs are enabled, and the Developer Settings tab displays an approval message.

No notification will be sent to the developer when the process is complete. You have to check the `Developer settings` page for the status message. After you're approved, you'll see the following message:

`Congratulations! Your developer setting have been reviewed and approved.`

After your approval, the `Save` and `Submit for Review` buttons on the Developer Settings page remain disabled unless you enter new data into one or more of the fields.

Developers only need to be reviewed once, unless you make changes to your information (see [Editing developer settings for an approved developer](#editing-developer-settings-for-an-approved-developer)). Once approved, your developer's settings are carried over to all skills developed with your Microsoft Account (MSA) email address.

## Developer not approved

If you are not approved, then the Group and World tabs remain disabled, and this notification is displayed at the top of the settings page:

`Unfortunately, your developer settings have not been approved. Please contact skillpub@microsoft.com.`

If you feel this is a mistake, or that you should be approved, contact the Certification Team at skillspub@microsoft.com.

It's also possible that you'll see a message like this:

`Something went wrong while processing your developer settings. Please contact skillpub@microsoft.com.`

When you contact us, please make sure to include your Microsoft Account (MSA) identifier, which is the email address you used when setting up your Azure account.

## Editing developer settings for an approved developer

If you have already been reviewed and approved, you can edit all of the developer settings except for the developer email (which is your MSA ID).  Making changes will cause the settings page to display an `Under Review` message while the new data is reviewed. If you already have skills in production, or deployed for testing, those skills will remain unchanged and will continue functioning as before.

If the changes to your data cause you to be rejected, then your current skills may be reviewed again. They will continue to function unless and until they're reviewed, at which time they may or may not be re-approved.

## The developer/publisher data

Most of the fields collected on the Developer tab are self-explanatory. Fields with an asterisk (*) are required. Other information follows the screenshot.

![Page tabs](../media/images/vetting-buttons-02.png)

![Data entry fields](../media/images/vetting-dev-info.png)

**Developer information**

- Email - This field is not editable. It's the email address (MSA identifier) that you used when you set up your Azure account.
- Developed by (for ISVs) - If the person who owns the MSA used to register the skill didn't develop it, fill this in with the name of whoever did develop the skill.
- Developer or Company Website URL - Specifically, this should point to either support or help pages.

**Support Contact** - Remember, we must have a way to contact you in case your skill has a problem. This email (or URL) is the contact that we'll use first.

- Email
- Website URL - This can be the same URL that you entered above.

**Publisher information**

- Name - This information is mainly used to differentiate between the publisher and the developer. If they're the same person (or company), you can enter the same information in both the developer and publisher fields.
- Email
- Phone number

<!--Hopefully, portions of this data can be pre-populated using data gleaned from the MSA Azure account -->

![Page buttons](../media/images/vetting-buttons-01.png)

Pressing `Back to Channels` will return you to the channels page, without saving anything you've entered. Pressing `Save` will save the current data, without submitting. `Submit for Review` will submit the data for approval by the Certification Team.

Once you press `Submit for Review`, the data on the page is locked, and the reviewing process is started.