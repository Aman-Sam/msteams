---
title: In-app purchase flow for the monetization of apps
description: Learn the basic tasks and concepts needed to implement in-app purchases and trial functionality in teams apps.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
localization_priority: Normal 
---

# In-app purchases

Microsoft Teams provide APIs that you can use to implement the in-app purchases to upgrade from free to paid Teams apps. In-app purchase allows you to convert users from free to paid plans directly from within your app.

> [!NOTE]
> In-app purchases for Teams apps is currently available only in [**Developer preview**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

## Implement in-app purchases

To offer an in-app purchase experience to the users of your app, ensure the following:

* App is built on [Teams client SDK library](https://github.com/OfficeDev/microsoft-teams-library-js).

* App is enabled with a transactable [SaaS offer](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md).

* App is enabled with [RSC permissions](#update-manifest).

* App is invoked with [`openPurchaseExperience` API](#purchase-experience-api).

In-app purchase experience can be enabled either by updating **manifest.json** file or by enabling **Show in-app purchase offers** from **Permissions** section of your **Developer Portal**.

### Update manifest

To enable in-app purchase experience, update your Teams app **manifest.json** file by adding the RSC permissions. It allows your app users to upgrade to a paid version of your app and start using new functionalities. The update for app manifest is as follows:

```json

"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
             "name": "InAppPurchase.Allow.User",
             "type": "Delegated"
            }
        ]
}
```

### Purchase Experience API

To trigger in-app purchase for the app, invoke the `openPurchaseExperience` API from your web app.

Following is an example of calling the API from the app:

```json
<body> 
<div> 
<div class="sectionTitle">openPurchaseExperience</div> 
<button onclick="openPurchaseExperience()">openPurchaseExperience</button> 
</div> 
</body> 
<script> 
   function openPurchaseExperience() {
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
      console.log("callback is being called");
      callbackcalled = true;  
      if (!!e && typeof e !== "string") {
            e = JSON.stringify(e);
            alert(e);
        }
        return;
      });
      console.log("after callback: ",callbackcalled);
    } 
</script> 
```

## End-user in-app purchasing experience

The following example shows the users to purchase subscription plans for a fictional Teams app called *Contoso Tasks for Teams*:

1. In the Teams **Store**, find and select the app.

1. In the app details dialog, select **Buy a subscription** or **Add for me**. 

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="Buying the subscription for the selected app." border="true":::

    
1. **Add for me** offers a free trial version of the app and later **Upgrade** it to a paid version.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="Upgrading to the subscription for the selected app." border="true":::

1. In the **Choose a subscription plan** dialog, choose the plan and select **Checkout**.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="Selecting the appropriate subscription plan." border="true":::

1. Complete the transaction and select **Configure now** to set up your subscription.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="Setting up the subscription." border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="Landing page of the subscription." border="true":::

## Next step

> [!div class="nextstepaction"]
> [Test preview for monetized apps](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## See also

* [Include a SaaS offer with your Microsoft Teams app](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [Create a Software as a Service (SaaS) offer](include-saas-offer.md#create-your-saas-offer)