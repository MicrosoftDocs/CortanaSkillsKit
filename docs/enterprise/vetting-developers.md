---
title: Vetting Cortana consumer skill developers
description: Describes the process for approving or rejecting third-party Cortana developers.
label: Conceptual

ms.date: 03/26/2019
ms.topic: article

keywords: cortana
---

# Vetting Cortana consumer skill developers

## Developer settings

Developers can create and test skills without using the Developer Settings page. The intent is to allow developers to test their skills on their own before submitting them for approval. However, developers need to be vetted before they can configure a skill for group or world, both of which allow other people to use it. To vet the developers, we have integrated Microsoft OneVet into the process via the Cortana Channel Configuration page.

All Developer and Publisher information is entered on a tab called `Developer Settings`, which appears on the Cortana Configuration page. The Microsoft Certification team will pass the data from the form to OneVet, which will screen for:

- **Trade Sanctions Screening:** Determinse whether someone is part of a sanctioned entity, with whom Microsoft can't do business.
- **Email Verification:** Verifies whether an individual has ownership of a specified email address.
- Domain Verification: **[According to the [OneVet website](https://microsoft.sharepoint.com/:w:/r/teams/OneVet/_layouts/15/Doc.aspx?sourcedoc=%7B80A84EBE-D407-4BB7-8A83-3707CB9A725B%7D&file=Vetting%20API%20-%20Domain%20Verification%20API%20Guide.docx&action=default&mobileredirect=true&DefaultItemOpen=1), this appears to be the same thing as email verification.]**
- **Business Verification:** Validates an entity's official name and address. This helps determine if a business is legitimate

The vetting results will be visible only to the Certification Team via the OneVet interface.

## Vetting approval

Once the developer settings are filled in and submitted, they can't be changed. The developer setting fields and the `Save` and `Submit` buttons are disabled in order to prevent changes. The Group and World tabs are disabled until the developer data is successfully processed. or until the certification team overrides the vetting process. **[Does the cert team send a notification for approval? Or for failure?]**

Once the developer is approved, the Group and World tabs are enabled, and the Developer Settings tab displays an `Approved` text. The Developer Setting fields and buttons remain disabled.

Developers only need to be vetted once, unless they make changes to their information (see [Editing developer settings for an approved developer](#editing-developer-settings-for-an-approved-developer)). Once approved, the developer's settings are carried over to all skills developed with that Azure Account. **[Since this is for consumer skills, wouldn't this be the email associated with an MSA?]**

## Vetting rejection

If the developer is not approved, then this notification will be displayed at the top of the configuration page: `This developer has not been approved. Please resubmit valid data or contact skillspub@microsoft.com.`

If you feel there's been a mistake, or that you should be approved, you can resubmit your data, or contact the Certification Team at skillspub@microsoft.com.

<!-- ## Override vetting flow

<!-- diagram goes here --> 

<!--## Override vetting status

The Cert team can override a developer's Vetting Status using the OneVet UI. When the vetting status is changed the approval callback modifies the "Approved" flag in the metadata store. 
There should be a label on the configuration page to contact skillspub@microsoft.com for assistance.
Example OneVet Request screen with Override button

<!-- screenshot goes here -->

## Editing developer settings for an approved developer

A developer who has already been vetted and approved can edit all of the developer settings except for developer email. Making changes will cause the Cortana Channel Configuration page to display an `Under Review` message while the new developer data is vetted again. If the developer already has any skills in production, or deployed for testing, they will not be reviewed again. They will remain unchanged and continue functioning. **[What happens to those skills if the developer is rejected?]**

<!-- ## Handling rejected developers

The Certification Team, either notified by email or by using the OneVet UI reporting, reviews the recent rejected developer information and decides if further steps need to be taken.

The team can decide to ignore the reject developer, contact the developer and/or look to see if the developer has any production skills that need to be disabled. 

Using the developer's email and Certification Admin tool the Cert team could identify the pertinent skills in production.

If a production skill is to be disabled the developer would be notified.

## Developer settings tab

A new tab will be added to the Cortana channel configuration page.

This tab will be the Developer Settings tab. Where the developer will enter the developer, support and publisher data.

Cortana Channel Configuration page with new tab

<!-- screenshot goes here -->

<!--When the tab is open it will display the developer and publisher data that was previously in the World Settings tab

## Opened developer settings tab

This data that will be used for OneVet vetting. Some of data will not be need for vetting and is only for the certification team and the publication process.

Consolidating the developer/publisher data this way also simplifies the bloated World settings page and segregates developer data from skill specific data.

Note: This scheme limits the developer MSA to a specific set of developer and publisher data.

<!-- screenshot goes here -->

## The developer/publisher data

The Developer/Publisher fields collected on the Developer tab (*required):

- Email - This field is not editable  Retrieved from the developer object created when the skill was registered with Cortana.
Note: This is the only developer email that will be vetted.
- Developer Account Type (radio control)
- First name
- Last name
- Email
- Phone number
- Address 1
  Address 2
- City/District
- Zip code
- Country
  Developed by (for ISVs)
- Developer or Company Website URL
  Support Contact
- Email
- Website URL
  Publisher information
- Name
- Email
- Phone number

<!--Hopefully, portions of this data can be pre-populated using data gleaned from the MSA Azure account -->

The Developer Settings page will have `Back`, `Save` and `Submit for Approval` buttons. Pressing `Back` will return you to the channels page. Pressing `Save` will save the current data, without submitting, and `Submit` will submit the data for approval by the Certification Team.

`Submit` will lock the data on the page, and start the vetting process.
