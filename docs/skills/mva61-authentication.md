---
title: Using authenticationn in your Cortana skill
description: Describes how to use authentication in your Cortana skill.

ms.date: 09/25/2018
ms.topic: article

keywords: cortana
---

# Using authentication in your Cortana skill

|   |   |
| - | - |
| ![](../images/video-icon.png) | [Watch a video](https://mva.microsoft.com/en-US/training-courses/getting-started-with-cortana-skills-18241?l=obdsHxeoE_5811787171) about using authentication with your Cortana skill. |

If your Cortana skill uses a service that requires authentication, you can let Cortana manage authentication by configuring the skill to use a connected service. You can specify whether to prompt the user for authentication credentials when Cortana invokes the skill. 

Once the authentication takes place, Cortana uses an authentication token to manage authentication for the skill. Rather than prompting the user again for credentials, Cortana uses the token to authenticate the user. In this module, you'll learn how to customize the **Mixtape** skill developed in previous modules to use authentication.

For more information about adding authentication to your skill, see [Adding authentication to your skill](./authentication.md).

## Step 1 - Configure your skill to use authentication

As you learned in [Create your first Cortana skill](./mva22-hello-world.md) and [Building conversations](./mva32-building-conversations.md), you register a Cortana skill by connecting your bot to the Cortana channel.


To enable authentication for your Cortana skill, update the skill's authentication settings by clicking the **Authentication** menu tab.

![Enable Authentication](../images/mva61-enable-auth.png)

To use OAuth2 authentication, select **OAuth2** from the **Configs in Vault** list and click **Add**, or click the **Add OAuth 2** button.


![OAuth2 Configuration](../images/mva61-oauth2-config.png)

Some settings are required and others are optional, although it is recommended that you specify the optional **Scope** entry. Here are the key settings:

* **Name:** A string that identifies the configuration.
* **Domain:** The domain of your OAuth2 provider.
* **Client ID:** The application ID you specified when you registered your bot as a Cortana skill.
* **Auth URL:** Your OAuth2 provider's Auth URL.
* **Response Method:** The response method to authenticate, either *GET* or *POST*.
* **Response Type:** The response type, either *Code* or *Token*.
* **Client Auth Scheme:** The authentication scheme, either *Basic Authentication* or *Auth in Body*.
* **Client Secret:** The password generated when you registered your bot as a Cortana skill.
* **Token URL:** Your OAuth2 provider's Token URL.
* **Scope:** The level of access to authenticate.


To save the configuration, click **Create OAuth2 Config**. 

## Step 2 - Test the revised skill

After you configure authentication for a skill, Cortana prompts for credentials when a user invokes the skill. For example, direct Cortana to invoke the Mixtape skill:

*Ask Mixtape to play me a song.* 

Cortana prompts you to sign in using your Microsoft account credentials.

![Authorization Signin](../images/mva61-auth-signin.png)





