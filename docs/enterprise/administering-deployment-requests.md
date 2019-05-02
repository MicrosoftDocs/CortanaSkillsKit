---
title: Administering deployment requests
description: Deploying your enterprise skill in the tenant.

ms.author: v-daturc
ms.date: 03/21/2019
ms.topic: article

keywords: cortana
---

# Administering deployment requests

IT admins can manage Cortana skills for their company through the [IT Admin Portal](https://it-admin-portal-prod.azurewebsites.net). IT admins can approve (enable) or reject (withdraw) skills for their company.

1. Launch the IT portal.

    ![IT portal](../media/images/administering-deployment-requests-01.png)

1. Double click on the skill you want to manage.

    ![IT portal](../media/images/administering-deployment-requests-02.png)

1. If you click `Approve` you will be asked to confirm the action and enter an audit reason.

    ![IT portal](../media/images/administering-deployment-requests-03.png)

1. If you click `Reject` you will be asked to confirm the action and enter an audit reason.

    ![IT portal](../media/images/administering-deployment-requests-04.png)

1. If the skill was previously approved, you may take it down by clicking `Withdraw`.

The IT Administrator is responsible for sending notification to the skill owners on the skill information page.

>[!IMPORTANT]
>Currently, the IT Administration tool and the skill deployment process do not support versioning. To deploy a new version of a skill, you'll need to create the new version with a different name and invocation phrase that you'll use during development and testing. When the new skill is ready to be deployed, you'll need to
>1. remove the existing skill, and 
>1. change the name and invocation phrase for the new skill so they're the same as the skill you just removed.