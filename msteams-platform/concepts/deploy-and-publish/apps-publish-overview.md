---
title: Overview - Distribute your app
description: Describes the options for publishing your Microsoft Teams app.
ms.topic: conceptual
author: KirtiPereira
ms.author: surbhigupta
ms.localizationpriority: none
---

# Distribute your Microsoft Teams app

You can provide your Microsoft Teams app to an individual, team, organization, or anyone who wants to use it. How you distribute depends on several factors including users' needs, business, technical requirements, and your goals for the app.

## Upload your app in Teams

Sideload an app for personal use, collaborating with your team, or testing and debugging. This kind of distribution doesn't require a formal review process.

> [!IMPORTANT]
> Currently, sideloading apps are available in Government Community Cloud (GCC), but are not available for GCC-High and Department of Defense (DOD).

For more information, see [upload your app in Teams](apps-upload.md).

## Publish your app to your org

Make your app available to people in your org. This kind of distribution requires your Teams admin's approval.

For more information, see [manage your apps in the Teams admin center](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json).

### Government Community Cloud (GCC) organizations

In GCC Teams environments, compliant Microsoft apps are enabled by default. Before publishing an app, however, make sure that all the app's endpoints comply with your GCC organization's requirements.

> [!IMPORTANT]
>If your app includes a bot or messaging extension, you must select the **Microsoft Teams for Government** option when setting up a channel between your bot and Teams in Azure. For more information, see [connect a bot to channels](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true).

## Publish your app to the Teams store

Make your app available to everyone. This kind of distribution requires Microsoft approval.

For more information, see [publish to the Teams store](~/concepts/deploy-and-publish/appsource/publish.md).

## See also

* [Microsoft 365 App Compliance Program](/microsoft-365-app-certification/overview)

## Next step

> [!div class="nextstepaction"]
> [Configure app's default install options](~/concepts/deploy-and-publish/add-default-install-scope.md)
