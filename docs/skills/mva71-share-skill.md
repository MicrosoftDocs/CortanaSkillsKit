---
title: Sharing your Cortana Skill to a group
description: Describes how to share your Cortana Skill to a group.

ms.date: 09/26/2018
ms.topic: article

keywords: cortana
---

# Sharing your Cortana skill to a group

<!--
|   |   |
| - | - |
| ![](../images/video-icon.png) | [Watch a video](https://mva.microsoft.com/en-US/training-courses/getting-started-with-cortana-skills-18241?l=IjcRvxeoE_1611787171) about sharing your Cortana skill to a group. |
-->

In [Using profile data in your Cortana skill](https://docs.microsoft.com/en-us/cortana/skills/mva52-using-profile-data), you learned how to make user profile data available to your Cortana skill by updating the skill's channel configuration settings. 

That module described using **Publish to self** option, which is the best publishing option to use when you are developing and testing a skill. **Publish to self** makes the skill available only to you. You must be logged in to your Microsoft account to use and test the skill.

When you are done testing your skill and ready to share it with other users, you have the following additional publishing options:

* **Publish to group**, which lets you deploy the skill to a specified group of users.
* **Publish to world**, which makes your completed skill available to all Cortana users after it has passed certification.

In this module, you'll learn how to publish the **Mixtape** skill developed in previous modules to a group. In [Publishing your Cortana skill](https://docs.microsoft.com/en-us/cortana/skills/mva72-publish-skill), you'll learn how to publish your completed skill.

For more information on Cortana publishing options, [Publishing Cortana Skills](https://docs.microsoft.com/en-us/cortana/skills/publish-skill)

## Step 1 - Create a group

To create a group of users who can use and test your Cortana skill, update the skill's **Publish to group** channel configuration settings. 

In the **Add user's Microsoft accounts** box, specify the members of the group by entering an email address associated with a Microsoft account for each user. The email account does not have to be a Microsoft account, such as an Outlook or Hotmail account, but it must be associated with a registered Microsoft account. Separate the email addresses with a semicolon.

![Publish to Group](../images/mva71-publish-group.png)

To create the group, click **Publish latest changes**. 

![Create Group](../images/mva71-group-created.png)

## Step 2 - Invite users to join the group

Users in the group can access the skill using the group access URL. Invite them to join the group by send them the URL.

![Send URL](../images/mva71-send-URL.png)

Opening the URL in a browser displays a prompt asking if the user wants to join the group.

![Join Group](../images/mva71-join-group.png)

Click **Accept** to accept the invitation and recieve a confirmation.

![Confirm Join](../images/mva71-confirm-join.png)

Each user in the group who has accepted the invitation should now have access to the skill in Cortana.

![Skill Access](../images/mva41-tada.png)

To leave the group, a user can open the group access URL and click **Leave**.

## Step 3 - Test your published skill

Once you have published your skill to the group, any group member can invoke the skill. For example, any group member can direct Cortana to invoke the Mixtape skill:

*Ask Mixtape to make me a mixtape.* 

Cortana prompts for credentials, if necessary, and launches the Mixtape skill:

![Launch Skill](../images/mva41-tada.png)
