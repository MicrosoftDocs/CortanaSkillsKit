---
title: Configure a connected account for Microsoft's identity server
description: Describes how to configure a connected account for Microsoft's identify service in Cortana's channel configuration settings.

ms.assetid: D7B5F7D3-12E9-4DB1-BC6F-1EC3FB1812C5
ms.date: 06/28/2019
ms.topic: article

keywords: cortana
---

# Configure authentication for Microsoft's identity server

If your skill uses a Microsoft service that requires an OAuth access token to authenticate the user, use Cortana's Connected Service feature. With the Connected Accounts feature, you specify a few OAuth settings and then Cortana handles all the work to get the token.

> [!NOTE]
> You can use *any* vendor's identity manager that manages resources for their services. The manager *must*
> support OAuth 2 code authentication flow.

Before configuring your skill for a Connected Account, you need to update your bot's registration to specify the redirect URL.

1. Navigate to [https://apps.dev.microsoft.com/#/appList](https://apps.dev.microsoft.com/#/appList).
1. Click your bot's name in the list. 
1. Under **Platforms**, click **Add Platform**.
1. Click **Web**.
1. Set the redirect URL to `https://www.bing.com/agents/oauth`. 
1. click **Save**.

Next, you need to update the Cortana channel configuration settings for your skill. One of the channel configuration options is to specify a connected account (see **Manage user identity**). The following steps walk you through adding a connected service.

1. Under the **Manage user identity through connected services** section press the option to enable it.
1. Fill in the form.
  
    | Item | Description  |
     |------|--------------|
    | **Sign in at invocation** | Select this option if you want Cortana to sign in the user at the time they invoke your skill.
    | **Sign in when required** | Select this option if you use a Bot Framework's SignIn card to sign in the user. Typically, you use this option if you want to sign in the user only if they use a feature that requires authentication. When your skill sends a message that includes the SignIn card as an attachment, Cortana ignores the SignIn card and performs the authorization flow using the Connect Account settings. |
    | **Account name** | The name of your skill that you want displayed when the user signs in to your skill. |
    | **Client ID for third-party services** | Your bot's application ID. You received the ID when you registered your bot. |
    | **Space-separated list of scopes** | Specify the scopes that the service requires (see the service's documentation). |
    | **Authorization URL** | Set to `https://login.microsoftonline.com/common/oauth2/v2.0/authorize`. |
    | **Token options** | Send auth on the `GET` request or via `POST` (recommended). |
    | **Grant type** | Select `Authorization code` to use code grant flow (recommended). Select `Implicit` to use implicit flow. |
    | **Token URL** | If you select `Authorization code`, set to `https://login.microsoftonline.com/common/oauth2/v2.0/token`. |
    | **Client secret/password for third party services** | The bot's password. You received the password when you registered your bot. |
    | **Client authentication scheme** | Select `Credentials in request body`. |

1. Save the skill.

If you previously configured the channel and want to update it to include a connected service:

1. Navigate to the [Bot Framework portal](https://dev.botframework.com/bots) and select your bot.
1. Press the **Edit** button next to the Cortana channel.
1. Specify the steps above to configure the connected account.

<!--

The following are the tasks you need to do to use Microsoft identity as a connected service in your skill. 

1. Register your skill in the Microsoft ecosystem.
2. Update your skill to use connected accounts. 

#### Register your skill in the Microsoft ecosystem

If you created a bot and registered it with Azure Bot Services, it is already registered in the Microsoft ecosystem. If not, the following steps show you how to register a new skill in the Microsoft ecosystem.

1. Navigate to [https://apps.dev.microsoft.com/portal/quickstart](https://apps.dev.microsoft.com/portal/quickstart).
2. Click **Web**.
3. Provide the following information:
    1. **Application Name** 
    2. **Contact Email**
3. Click **Create**.
4. Enter `https://www.bing.com/agents/oauth` as the redirect URL and save.
5. Click **go to settings** to continue configuring your skill.
6. On the configuration page, click **Generate new password** to generate an application secret. Make sure to save it somewhere safe!

If you already registered your bot, you need to edit the registration to add the redirect URL. To add authentication support to an already registered bot, follow these steps.

1. Navigate to [https://apps.dev.microsoft.com/#/appList](https://apps.dev.microsoft.com/#/appList).
2. Select your bot from the list of apps. 
3. Under **Platforms**, click **Add Platform**.
4. Click **Web**.
5. Set the redirect URL to `https://www.bing.com/agents/oauth` and click **Save**.
6. The password used for authentication is your bot's password. 

-->



## Next steps

For more information about using authentication, see [Adding authentication to your skill](./authentication.md).
