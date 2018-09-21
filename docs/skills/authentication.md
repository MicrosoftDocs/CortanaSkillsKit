---
title: Adding authentication to your  Skills
description: Learn how to add authentication to your bot-based skill.
label: Conceptual
ms.assetid: 182bda3b-5466-4337-8399-72598116cd9f
ms.date: 05/03/2017
ms.topic: article

keywords: cortana
---

# Adding authentication to your skill

> [!NOTE]
> This documentation provides details around authenticating skills built using the Microsoft Bot Framework.
> 


There are two ways to add authentication to your skill.

* Link a Connected Account to your skill
* Use Bot Framework's [sign-in card](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#add-a-sign-in-card-to-a-message)

## Link a Connected Account to a Cortana skill

If your skill uses a service that requires user authentication using OAuth, you can use Cortana's Connected Account feature to get an access token to use with the service. All you need to do is provide Cortana a few OAuth settings and she takes care of the rest for you.

You decide whether Cortana signs in the user when they invoke your skill or only when they activate a feature of your skill that requires authentication. Cortana initiates your identity server's sign in process, which prompts the user to sign in. If you use the code grant flow, Cortana automatically re-authenticates the user using a refresh token until they disconnect the skill in Cortana’s Notebook, the refresh token expires, or the user changes their password. 

Cortana Skills supports OAuth's Code Grant flow and Implicit Grant flow. For information about adding a connected account to your skill, see [Manage user identity](https://docs.microsoft.com/en-us/bot-framework/channel-connect-cortana#manage-user-identity) in Cortana's channel configuration.

The Connected Account feature supports using a single identity service. If your skill calls different services that use different identity services, you can use Connected Account with one of the services, but you need to use a different mechanism to authenticate the user with the other services.

<!--
## Bot Framework sign-in card

Cortana does not currently support Bot Framework's sign-in card. Please use the Connected Accounts feature to enable authorization for your skill. 
-->


## Getting the cached access token 


If you configure Cortana's channel for connected accounts, Cortana sends the authentication token to your skill as entity data. From the point you ask Cortana to authenticate the user, each message's `entities` property includes an `AuthorizationToken` object.


The `AuthorizationToken` object contains the following properties:

| Name     | Type     | Description              |
|----------|----------|--------------------------|
| type | string | The object's type, which is set to AuthorizationToken. 
| token    | string   | The access token. This field is null if the user canceled the sign-in process or didn't give consent. |
| status   | string   | The status of the access token. The following are the possible values.<ul><li>1&mdash;The `token` field contains a valid access token. </li><li>2&mdash;Sign-in succeeded. This value is set on the first message following user sign in. The `token` field contains the access token.</li><li>3&mdash;Sign-in canceled by user. The `token` field is set to null.</li></ul>  |

The following shows an example of the `AuthorizationToken` object.

```json
{                             
    "type": "AuthorizationToken",  
    "token": string,
    "status": string                                
}
```

## Next steps

If you use a Microsoft service that requires users with Microsoft accounts, see [Configure authentication for Microsoft's identity server](configure-connected-account.md) for information about configuring Connected Account channel settings for Microsoft's identity server.
