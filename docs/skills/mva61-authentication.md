---
title: Using authentication in your Cortana Skill
description: Describes how to use authentication in your Cortana Skill.

ms.date: 07/16/2019
ms.topic: article

keywords: cortana
---

# Using authentication in your Cortana skill

> [!IMPORTANT]
> This page has been deprecated as we update our documentation to Azure Bot Service v4.

If your Cortana skill uses a service that requires authentication, you can let Cortana manage authentication by configuring the skill to use a connected service. You can specify whether to prompt the user for authentication credentials when Cortana invokes the skill.

Once the authentication takes place, Cortana uses an authentication token to manage authentication for the skill. Rather than prompting the user again for credentials, Cortana uses the token to authenticate the user. <!-- In this module, you'll learn how to customize the **Mixtape** skill developed in previous modules to use authentication. -->

For details about using authentication, see [Adding authentication to your skill](./authentication.md).
