---
title: Prerequisites to create a SaaS offer
description: Learn how to configure APIs required to create a SaaS offer and build a landing page for your SaaS offer.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high 
ms.date: 01/31/2023
---
# Prerequisites to create an offer

:::row:::
   :::column:::
      :::image type="icon" source="~/assets/images/saas-offer/monetize-flow1.png" link="include-saas-offer.md" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="~/assets/images/saas-offer/monetize-flow2a.png" link="prerequisites.md" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="~/assets/images/saas-offer/monetize-flow3.png" link="create-saas-offer.md" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="~/assets/images/saas-offer/monetize-flow5.png" link="Test-preview-for-monetized-apps.md" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="~/assets/images/saas-offer/monetize-flow6.png" link="publish-saas-offer-app.md" border="false":::
   :::column-end:::
:::row-end:::

To create a SaaS offer, you must have the required technical information and fulfill the technical configurations. It helps negate any blockers while creating the offer.

To create a SaaS offer:

> [!div class="checklist"]
>
> * [Set up Microsoft and Microsoft Entra account](#set-up-microsoft-and-azure-ad-accounts)
> * [Create a landing page](#create-a-landing-page)
> * [Gather the required technical information](#technical-requirements)
> * [Perform API integrations](#api-integration) specific to sell through Microsoft offers

The technical configurations differ based on the listing option. The following illustration can help you understand the configurations for each offer type.

:::image type="content" source="../../../../assets/images/saas-offer/tech-config-offer.png" alt-text="Diagram shows the technical configuration per the type of listing option.":::

> [!NOTE]
> The *Contact me* listing option have no technical configurations to be done.

## Set up Microsoft and Microsoft Entra accounts

To start with, you must set up the required accounts to create an offer.

* Enable Microsoft Accounts (MSA) and ensure you have a [Microsoft Partner Center account](/partner-center/marketplace/open-a-developer-account).

* Microsoft Entra ID provides an easier and secure purchase experience. Enable [Microsoft Entra ID](https://azure.microsoft.com/services/active-directory/) for authenticating buyers on your site.  With [Microsoft Entra integration](/partner-center/marketplace/azure-ad-saas), you can automatically provision the users to their SaaS apps and also allow buyers to sign in to your app using Microsoft Entra single sign-on (SSO). For more information, see [Microsoft Entra ID and transactable SaaS offers](/partner-center/marketplace/azure-ad-saas).

## Create a landing page

After a user successfully purchases a subscription plan, commercial marketplace directs them to the offer landing page where they can manage the subscription (such as assign a license to a specific user in their organization).

Ensure to register your landing page as an Microsoft Entra application. Enable SSO using Microsoft Entra ID and Microsoft Graph to retrieve buyer information and to confirm and activate the subscription. For complete instructions, see the following articles:

* [Build the landing page for your transactable SaaS offer](/partner-center/marketplace/azure-ad-transactable-saas-landing-page).
* [Build landing page for your free or trial SaaS offer](/partner-center/marketplace/azure-ad-free-or-trial-landing-page)

### Best practices for landing pages

Consider the following approaches when building a landing page for the Teams app you’re monetizing. See an example landing page in the [End-user purchase experience](end-user-purchase-experience.md).

* Provide the name and details of the offer and user's account details.
* Enable users to sign in from offer landing page only using the same Azure AD credentials they used to buy the subscription.
* Provide an introduction on how to use your app.
* Add ways to get support, such as FAQs, knowledge base, or contact email.
* Provide a link that makes it easy for the subscriber to get back to the landing page.

### Technical requirements

When you create the SaaS offer, you must provide the following technical information during the [offer configuration](create-saas-offer.md#add-the-technical-information).

* **Landing page URL**: The SaaS site URL that users get redirected to after purchasing your offer from the commercial marketplace. It triggers the configuration process from the newly created SaaS subscription. This URL receives a token that can be used to call the fulfillment APIs to get provisioning details for your interactive registration page.

* **Connection webhook URL**: For all asynchronous events that Microsoft needs to send to you (for example, when a SaaS subscription has been canceled), we require you to provide a [connection webhook URL](/partner-center/marketplace/create-new-saas-offer-technical). We call this URL to notify you of the event. Define it in the **Technical configuration** page and you receive subscription changes from the user.

* **Azure AD tenant ID**: Inside the Azure portal, we need you to register an Azure AD app so we can add it to the access control list (ACL) of the API to make sure you're authorized to call it. You can find the tenant ID under **App registrations** in Azure portal.

* **Azure AD application ID**: The Azure AD application ID is associated with your publisher ID in your Partner Center account. You must use the same application ID for all offers in that account.

## API integration

API integrations are specific for Sell through Microsoft listing option, in addition to the basic setup. When the user purchases the offer and is redirected to the landing page from the configuration link, a set of user information is required to confirm and activate the subscription.

> [!NOTE]
> API integrations can also be done after the user purchases the SaaS app subscription.

### Integrate with SaaS fulfillment API

Integrating with the SaaS Fulfillment APIs help to manage the lifecycle of a subscription plan once the user purchases the plan.

In general, you implement the following steps using the APIs once a subscription is purchased and the customer selects to configure:

  1. You receive a notification about the purchase where your landing page URL opens with the [purchase identification token](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle).
  1. You must pass the token by calling SaaS Resolve API to retrieve subscription details.
  1. After the user sign in and configuration, you must then call the Activate Subscription API to notify the commercial marketplace that the subscription is activated.

For comprehensive instructions and API reference, see [SaaS Fulfillment APIs](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis) and [SaaS Fulfillment purchase flow](/partner-center/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle) documentation.

### Integrate with Graph usageRights API

Integrate with Graph usageRights API to manage user permissions at the time of app launch by a customer who has a purchase license. You're required to determine the user’s permissions for the app with a Graph call to the usageRights API.

You can call Graph APIs to determine if the currently logged in user with a valid subscription of the plan has access to your app. To call Graph usageRights API to check user permissions, follow the steps:

  1. Get user OBO token: [Get access on behalf of a user](/graph/auth-v2-user).
  1. Call Graph to get the user’s object ID: [Use the Microsoft Graph API](/graph/use-the-api).
  1. Call usageRights API to determine the user has a license to the plan: [List user usageRights API](/graph/api/user-list-usagerights?view=graph-rest-beta&tabs=http&preserve-view=true).

  > [!NOTE]
  >
  > * You need to have a minimum `User.Read` permissions to call usageRights.
  > The usageRights API is currently in beta version. After the version is updated to V1, users must upgrade from beta to V1 version.
  > * If the Azure AD app is used for both SaaS Fulfillment APIs and usageRights API, ensure that the tenant under which the Azure AD app is created is either the publishing tenant or the associated tenant in the Partner Center.

For detailed information, see [usageRights Graph API](/partner-center/marketplace/isv-app-license-saas).

To determine if the tenant for the Microsoft Entra app is part of the Partner Center setup, follow these steps:

  1. Sign in  to [Microsoft Partner Center](https://partner.microsoft.com/) with the publisher account that is used to publish the SaaS offer.
  1. On the upper-right corner, select the **Settings** icon.
  1. Select **Account Settings**.
  1. On the left pane, select **Tenants**.
    You can see all tenants associated with the Microsoft Partner Network (MPN) account. The tenant, who is the owner of the Azure AD app, must be available in the list. If the tenant isn’t on the list, you can use the **Associate Azure ID** button to link the tenant.

Integrating the APIs and building your landing page to manage subscriptions helps to manage and track your offers right from the start and provide a seamless user experience.

## Next step

> [!div class="nextstepaction"]
> [Create your SaaS offer](create-saas-offer.md)

## See also

* [Monetize your app](monetize-overview.md)
* [SaaS app listing requirements](/partner-center/marketplace/marketplace-criteria-content-validation)
* [Create a commercial marketplace account in Partner Center](/partner-center/create-account)
