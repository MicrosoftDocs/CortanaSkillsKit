---
title: Test Group Settings
description: Describes how to fill out Test Group section when publishing a Cortana skill.
ms.topic: article
ms.date: 05/24/2019
ms.topic: article


keywords: cortana
---

# Test Group Settings

Deploying to **Test Group** makes your Cortana skill available to a group of users that you specify, using individual MSA email addresses. Typically, you create a test group to have others test your Cortana skill and provide feedback. It's a really good idea to test and update your skill before making it generally available.

![Test Group Settings - not configured](../media/images/test_group_settings-not_configured.png)

1. On the **Configure Cortana** page, under the **Test Group Settings** section, enter the following information.

    Complete the required fields that are marked with an asterisk (*).

    >[!NOTE]
    > For more information about the bot configuration fields, visit the [Connect a bot to Cortana](https://docs.microsoft.com/azure/bot-service/bot-service-channel-connect-cortana) page.

    1. **Skill information** section

        ![Skill information](../media/images/test_group_settings-skill_information.png)

        * `Skill icon`: Click on the `Upload icon` button and select an icon for your Cortana skill. Skill icons should be square (44x44 pixels), and in PNG format.
        * `Display name`: The length of the name is limited to 30 characters.
        * `Invocation name`: This field displays the name that the user speaks (or types) to invoke your skill.
            >[!NOTE]
            > The invocation name shown was previously defined in the setup process, and can't be changed here.

    2. Request user profile data

        ![Request user profile](../media/images/test_group_settings-request_user_profile_data-empty.png)

        Click on **Add a user profile request** and select the user profile information from the drop-down menu. Repeat to select additional user profile data.

        >[!IMPORTANT]
        > You are allowed to collect user profile data only to add to your skill's functionality. See section [2.5 Personal Information](./skill-review-guidelines.md#25-personal-information) in the [Cortana skills certification requirements page](./skill-review-guidelines.md).

        ![Request user profile - all](../media/images/default_settings-request_user_profile_data-all.png)

        >[!TIP]
        > For more information about the bot configuration fields, visit the  [Connect a bot to Cortana](https://docs.microsoft.com/azure/bot-service/bot-service-channel-connect-cortana) page.

    3. Group
        ![MSA email addresses - empty](../media/images/test_group_settings-group-empty.png)
        * `Member email`: Enter an MSA e-mail address and click Add. You can enter multiple MSA e-mail addresses by using semicolons to separate them.

            ![MSA email addresses](../media/images/test_group_settings-group-contoso_hotmail.png)

1. When you're done, click on the `Create Group` button. The button is enabled only after all of the required fields are completed.

    ![Back to Channels](../media/images/test_group_settings-back-create.png)

    ![Create Group - enabled](../media/images/test_group_settings-back-create-active.png)

1. After your test group is created, the **Test Group Settings** section displays the group information.

    ![Group - created](../media/images/test_group_settings-group-contoso_hotmail-group_access_url.png)

    * `Member email`: Shows the list of member email addresses.

    * `Group Access URL`: The URL that your group members will use to access your skill.
        * >[!IMPORTANT]
            > You must manually send an email message to the designated MSA users listed in the `Member email` field. This email will be your user's only invitation to join the skill test group. The message must include the URL from the `Group Access URL` field.
            >
            > When an MSA user clicks on the **Group Access URL** in the message, they have the option to accept or decline joining the skill test group. If the user accepts, then access is granted to test your Cortana skill. If the user declines to join, then access is denied.

    * The `Reset Group` button is added and the `Create Group` button is replaced by the `Save changes` button.

        ![Reset Group, Back to Channels, Save changes](../media/images/test_group_settings-reset-back-save.png)

    * The **Test Group Setting** link is updated.

        ![Test Group Settings - configured](../media/images/test_group_settings-configured.png)
