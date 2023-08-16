---
title: Purchase and manage app subscriptions and licenses
description: Learn how to purchase, assign, and manage licenses for third-party apps in Teams.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.date: 04/06/2023
---

# Purchase and manage app subscriptions and licenses

The information in this article helps you understand the purchase experience from the customer end. You can add additional features and functionality to your Teams app through subscriptions. Users can purchase subscriptions and manage licenses for themselves, their team, or their organization directly from the Teams store.

## Subscription experience

The following example shows how users can purchase subscription plans for a fictional Teams app called *Recloud*:

1. In the Teams store, find and select the *Recloud* app.

1. In the app details dialog, select **Buy a subscription**.

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="Screenshot shows buying the subscription for the selected app.":::

1. Select your country or region to see subscription plans for your location.

1. In the **Choose a subscription plan** dialog, choose the plan you want and select **Checkout**.

    > [!NOTE]
    > Private plans are visible only to users of the organizations to whom the plans are made available. These plans are indicated with a **Special offer**:::image type="icon" source="~/assets/icons/special-icon.png"::: icon.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="Screenshot shows selecting the appropriate subscription plan.":::

1. In the **Checkout** dialog, provide any required information and select **Place order**.

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="Screenshot shows placing the subscription order.":::

1. When prompted, select **Set up now** to set up your subscription.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="Screenshot shows the option to set up your subscription.":::

1. Manage your subscription plan through the *Recloud* website (also known as a [landing page](prerequisites.md#create-a-landing-page)).

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="Screenshot shows User and Licenses screen to assign license.":::

When a new user launches the app for the first time, they're requested to provide consent to the app. Following is an example of the consent screen shown when calling for user profile data with minimum User.Read permission.

Consent dialog is part of the flow to get the users' license information and may vary based on ISV’s integration approach.

:::image type="content" source="../../../../assets/images/saas-offer/permissions-requested.png" alt-text="Screenshot shows the Permissions requested consent dialog.":::

## License management experience

The following example shows how users can manage licenses for third-party apps from the Teams store:

1. Go to **Microsoft Teams**.

1. Select **Apps** > **Manage your apps**.

    :::image type="content" source="../../../../assets/images/saas-offer/client-experience-1.png" alt-text="Screenshot shows the Apps screen to select Manage your app option.":::

1. Select **Subscriptions**. A tab appears with a list of purchases made in the tenant.
1. Choose an existing subscription from the list and select **Assign licenses**.

    :::image type="content" source="../../../../assets/images/saas-offer/client-experience-2.png" alt-text="Screenshot shows the Assign licenses option of the respective app under Subscription tab.":::

1. To view license utilization and assign licenses, select **Assign licenses**.

    :::image type="content" source="../../../../assets/images/saas-offer/view-license.png" alt-text="Screenshot shows the selected assigned licenses highlighted in red.":::

1. Search for the users or a team in the search box and select **Assign**. The license is assigned to the users or a team.

    :::image type="content" source="../../../../assets/images/saas-offer/assign-licenses.png" alt-text="Screenshot shows assigning license to a Team highlighted in red.":::

    You can view the list of assigned users or teams for the subscription and also check the status of the assignment.

    :::image type="content" source="../../../../assets/images/saas-offer/list-of-assigned-users.png" alt-text="Screenshot shows the list of assigned users with Assign licenses option highlighted in red.":::

1. If you want to unassign a license for a user or a team, select the users or a team from the list and select **Unassign**.

    :::image type="content" source="../../../../assets/images/saas-offer/unassign-button.png" alt-text="Screenshot shows the Unassign option highlighted in red to unassign the selected users.":::

## Admin purchasing experience

Admins can manage the app subscriptions and licenses in the Teams admin center. For more information, see [Purchase third-party Teams apps and manage subscriptions](/microsoftteams/purchase-third-party-apps).

## See also

* [Monetize your app](monetize-overview.md)
* [Set up Microsoft license management for third-party apps](manage-third-party-apps-license.md)
