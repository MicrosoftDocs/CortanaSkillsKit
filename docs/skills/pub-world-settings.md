---
title: World Group Settings
description: Describes how to fill out World Group section when publishing a Cortana skill.
ms.topic: article
ms.date: 05/24/2019
ms.topic: article
ms.author: v-daturc

keywords: cortana
---

# World Settings

Deploying your Cortana skill to **World** will submit your skill for review. Once it has passed review, your skill will be published in all markets that you specified when you registered your bot.

>[!TIP]
> If you complete some of the required fields but need to continue later, click on the `Save and Close` button at the bottom of the page. This will save the data you've already entered, and allow you to resume later.

For more information about the requirements for publishing to **World**, visit the [Cortana skills Kit Certification Requirements](./skill-review-guidelines.md) page.


![World Settings - not configured](../media/images/world_settings-not_configured.png)

1. On the *Configure Cortana* page, you'll need to enter the following information under the **World Settings** section.
    Complete the required fields that are marked with an asterisk (`*`).

    For more information about the bot configuration fields, visit the [Connect a bot to Cortana](https://docs.microsoft.com/azure/bot-service/bot-service-channel-connect-cortana) page.

    1. **Skill information** section

        ![Skills information](../media/images/world_settings-skill_information.png)

        * `Skill icon`: Click on the `Upload icon` button and select an icon for your Cortana skill.
        * `Display name`: This name is limited to 30 characters.
        * `Invocation name`:  This field displays the name that the user speaks (or types) to invoke your skill.
            >[!NOTE]
             > The invocation name field will contain the name that was previously defined in the setup process. The name can't be changed here.
        * `Short description`
        * `Long description`
        * `Sample Invocation Phrase`: Enter an invocation phrase and click on the `Add sample invocation phrase` button.
        * `Primary category`: Click the drop-down menu to select a category that matches your Cortana skill.
        * `Secondary category (Optional)`: Click the drop-down menu to select a secondary category.

            > [!NOTE]
            > Categories can be used in searching, so select categories that will help users find your skill.

        * `Tags`: Enter a unique word and click on the `Add` button.

            You can create more tags by repeating this step. Tags are similar to categories in that they can be used in searches to help users discover your skill.

        * `Supported platforms`: Select the platform(s) your skill supports.

    1. `Does this Cortana skill collect users' personal information?`: If you set this switch to `Yes`, you'll see the **Request user profile data** section.

        [Does this Cortana skill collect users' personal information?](../media/images/world_settings-collect_users_information-on.png)

        [Does this Cortana skill collect users' personal information?](../media/images/world_settings-collect_users_information-on-user_data.png)

    <!-- 3. **Developer Account** section

        ![Developer Account Type - Developer](../media/images/world_settings-developer_account-developer.png)  ![Developer Account Type - Company](../media/images/world_settings-developer_account-company.png)

        `Developer Account Type`: Click on the radio button matching your type.

        - If you are an individual or student developer, then select `Developer`.

        - If you are part of a company, then select `Company`.

    4. **Developer Information** section: Note that all of the fields on this form are required.

        ![Developer Information](../media/images/world_settings-developer_information.png) -->

    <!-- 5. **Support Contact** section
        This is where you provide contact information for the Cortana team to reach you.

        ![Support Contact](../media/images/world_settings-support_contact.png)

    6. **Publisher Information** section

        ![Publisher Information](../media/images/world_settings-publisher_information.png) -->

    1. **Privacy policy and terms of use** section

        [Privacy policy and terms of use](../media/images/world_settings-privacy_policy_terms_of_use.png)

    1. **Validation and testing instructions** section

        [Validation and testing instructions](../media/images/world_settings-validation_testing_instructions.png)

1. Click on the `Save` button.

         [Back to Channels, Save, Submit for Review](../media/images/world_settings-back-save-submit.png)

1. Click `Submit for review`.

    The `Submit for review` button is enabled only after all of the required fields are completed.

    [Back to Channels, Save, Submit for Review](../media/images/world_settings-back-save-submit.png)

    [Submit for Review - enabled](../media/images/world_settings-back-save-submit-active.png)

    >[!IMPORTANT]
    > After submission for review, you will not be able to edit the properties you entered, or delete your Cortana skill. See the [Withdrawing Your Submission](publish-skill.md#withdrawing-your-submission) section.

1. After you submit the skill for review, the **World Settings** section displays the following changes.

    * The `Save` button and `Submit for Review` button are removed.

        [Reset Group, Back to Channels, Save changes](../media/images/world_settings-back-submitted-approved.png)

    * The `World Setting` link is updated.

        [World Settings - submitted](../media/images/world_settings-submitted.png)

        This message under the `World Setting` link shows the review status for your Cortana skill (`Submitted`, `Not accepted`, or `Accepted`). The Cortana Certification Team reviews all third-party skills before they can be released. If the team has any concerns or questions during the review process, you will receive an email message at the address you specified. If it's rejected, then the details and reasons for rejection are provided. If all requirements are met, then your Cortana skill is accepted and deployed.

    >[!TIP]
    > If you run into any technical issues, or otherwise need help, please email the **Cortana Skills Kit Support Team** at [skillsup@microsoft.com](mailto:skillsup@microsoft.com).
