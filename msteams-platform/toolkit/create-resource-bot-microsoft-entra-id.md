---
title: Create bot resource in Microsoft Entra ID
author: surbhigupta
description: Create an Azure bot resource in Microsoft Entra ID to add your bot app to Teams
ms.topic: how-to
ms.author: surbhigupta
ms.localizationpriority: medium
---
# Create a bot resource in Microsoft Entra ID

Your Teams bot app can access resources available in Microsoft Entra ID. You'll need to create a bot resource with Microsoft Entra ID. This process will register your bot app with Azure AI Bot Service and enable the bot app to connect to Teams channels.

In this section, you will:

- [Create bot resource](#create-a-bot-resource-in-azure-ad)
- [Configure the client secret](#create-client-secret)
- [Enable the bot resource for Teams](#enable-bot-for-teams)

## Create and deploy bot resource in Microsoft Entra ID

You can create a bot resource in Microsoft Entra ID for a single or multitenant app.

### To create and deploy bot resource

1. Open the [Azure portal](https://ms.portal.azure.com/) on your web browser.

1. Select the **Create a resource** icon.

    :::image type="content" source="../assets/images/meetings-side-panel/create-resource-azure-portal.png" alt-text="Screenshot shows the create a resource option in Azure portal.":::

    The **Create a resource** page appears.

1. Type **Azure bot** in the search box, and select the Azure bot from the options that appear.

    :::image type="content" source="../assets/images/authentication/select-azure-bot-marketplace.png" alt-text="Screenshot shows the azure bot in the azure marketplace.":::

    The **Azure Bot** page appears, and the plan is pre-selected as Azure Bot.

1. Select **Create**.

    :::image type="content" source="../assets/images/authentication/azure-bot-create.png" alt-text="Screenshot shows the azure bot plan selected in the azure bot creation screen.":::

    The **Create an Azure Bot** page appears.

1. Enter relevant details for the bot app.

    1. Under **Project details**, enter the following:

        1. Enter a unique identifier as the bot handle. It isn't the display name, and you can choose a different display name later.

        1. Select a subscription plan.

        1. Select the resource group that you want to provision for your bot app.

        1. Select the data residency option. Depending on your choice, this limits or doesn't limit the regions where data is stored and processed and the channels available for your bot.

        :::image type="content" source="../assets/images/authentication/create-azure-bot-screen.png" alt-text="Screenshot shows the main create azure bot screen.":::

            You can also create a new resource group.

            1. Select **Create new**.

                :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/create-new-resource.png" alt-text="Create new resource for provisioning." border="false":::

            1. Enter a name for the resource and select **OK**.

    1. Select the **Pricing** details.

        The standard price tier is selected by default. You can change your pricing tier, if needed.

    1. Select the **Microsoft App ID** details.

        1. Select the type of app in the **Microsoft App ID** section. Choose from User-assigned managed identity, Multi Tenant, and Single Tenant.

        1. Select **Use existing app registration** as the creation type.

            The fields for entering the app ID details appear.

        1. Enter the app ID for the Azure AD app you registered.

        1. Enter the app tenant ID for the Azure AD app you registered.

1. Select **Next : Tags >**.

    The **Tags** tab opens.

1. Enter the name and value tags for categorizing resources you provisioned.

    These steps aren't mandatory and you can skip them, if needed.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/create-bot-tags.png" alt-text="Create name and value tag pairs for categorizing resources for billing purpose." border="false":::

1. Select **Next : Review + create >**.

    Azure AD validates the project details. After successful validation, it creates the project and provisions the selected resources.

1. Select **Create** to create the bot after successful validation.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/review-create.png" alt-text="Create bot" border="false":::

     A message pops up on the browser stating that the deployment is being initialized.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/initialize-deploment.png" alt-text="Message stating deployment is initialized" border="true":::

    The **Overview** page appears that states the deployment is in progress. The deployment details are displayed on the page.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/deploy-progress.png" alt-text="Deployment in progress" border="false":::

1. Select **Go to resource** to view the bot details.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/bot-deployed.png" alt-text="Bot resource is deployed" border="false":::

     You can view the subscription details for the bot resource.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/bot-app-created.png" alt-text="Bot app is created" border="false":::

After you create your bot resource, you need to add a client secret and enable bot for working in Teams.

### Create client secret

A client secret is a string that the bot app uses to prove its identity when requesting a token from Azure AD.

#### To create client secret for the bot

1. Open the [Azure portal](https://ms.portal.azure.com/) on your web browser.
   The Microsoft Azure Bot page opens.

1. Enter the name of your Azure AD app in **Search** box, and open your app.

1. Select **Settings** > **Configurations**.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/bot-app-menu.png" alt-text="bot-config-menu.png":::

    The **Configuration** page appears.

1. Select the **Manage** link shown with **Microsoft App ID**.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/bot-config-manage.png" alt-text="Manage link for bot app configuration":::

     The **Certificates & secrets** page appears. The Manage  menu appears in left pane menu.

2. Select **+ New client secret**.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/new-client-secret.png" alt-text="Add new client secret" border="false":::

   The **Add a client secret** page appears.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/add-client-secret.png" alt-text="Add a client secret page" border="true":::

3. Enter the description.
4. Select the duration of validity for the secret.
5. Select **Add**.

   A message pops up on the browser stating that the client secret was updated. The client secret displays on the page.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/client-secret-added.png" alt-text="Client secret added":::

6. Select the copy button next to the **Value** of client secret.
7. Save the value that you copied for later use.

   > [!NOTE]
   > Ensure that you copy the value of client secret right after you create it. The value is visible only at the time when the client secret is created, and can't be viewed after that.
   >
### Enable bot for Teams

You must enable the Teams channel to let the bot interact with Microsoft Teams.

#### To enable bot app for Teams

1. Open the [Azure portal](https://ms.portal.azure.com/) on your web browser.
   The Microsoft Azure Bot page opens.

1. Enter the name of your Azure AD app in **Search** box, and open your app.

1. Select **Settings** > **Channels**.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/channel-menu.png" alt-text="Menu option for enabling bot for Teams " border="false":::

    The **Channels** page appears.

1. Move through the list of **Available Channels** to select **Microsoft Teams**.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/teams-channel.png" alt-text="Select Teams channel" border="false":::

    The message with **Terms of Service** appears.

1. Check to agree with the terms and select **Agree**.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/terms-service.png" alt-text="Terms of service for Teams channel" border="true":::

    The **Microsoft Teams** page appears with the default messaging option selected **Microsoft Teams Commercial (most common)**.

1. Select **Apply**.

    > [!NOTE]
    > If you want to change channel settings, you'd need to delete the channel and apply it again with new settings.
    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/teams-messaging.png" alt-text="Teams messaging options for bot" border="false":::

    A message pops up on the browser stating that the channel settings are being applied.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/msg-channel.png" alt-text="Message for Teams channel being applied" border="true":::

    The channel settings are applied.

1. Select **Close**.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/channel-applied.png" alt-text="Channel setting applied to bot." border="false":::

    The bot is now enabled to work with Teams.

    :::image type="content" source="../../assets/images/aad-configuration/bot-resource-aad/teams-added.png" alt-text="Bot is enabled for Teams":::

## See also

-
