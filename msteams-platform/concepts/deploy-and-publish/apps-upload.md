---
title: Upload your custom app
description: Learn how to sideload your app in Microsoft Teams. Sideloading is common when testing and debugging an app during development.
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
---

# Upload your app in Microsoft Teams

You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store. This makes sense in the following scenarios:

* You want to test and debug an app locally yourself or with other developers.
* You built an app just for yourself. For example, to automate a workflow.
* You built an app for a small set of users, such as, your work group.

> [!IMPORTANT]
> Currently, sideloading apps are available in Government Community Cloud (GCC), but are not available for GCC-High and Department of Defense (DOD).

## Prerequisites

* Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.
* [Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.
* Make sure that your app is running and accessible via HTTPs.

## Upload your app

You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.

1. Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).
1. Select **Apps** and choose **Upload a custom app**.
1. Select your app package .zip file. An install dialog displays.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Screenshot showing an example of a Teams app install dialog.":::
1. Add your app to Teams.

> [!NOTE]
> `onInstallationUpdateActivityAsync()` method is used to get Microsoft Teams Locale while adding the bot to Microsoft Teams.

## Troubleshoot upload issues

If your app fails to sideload, do the following until the issue resolves:

1. Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).
1. [Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.
1. Ensure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).

## Access your app

Teams provides several ways to open apps. For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## Update your app

You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time). However, you must reinstall if you change any app configurations.

## Remove your app

To remove your app, right click the app icon in Teams and select **Uninstall**.

> [!NOTE]
> You can't remove personal bot activity entirely. If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.

## Next step

> [!div class="nextstepaction"]
> [Use your Teams app](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)

## See also

* [Configure default install options](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Maintain your published Microsoft Teams app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
