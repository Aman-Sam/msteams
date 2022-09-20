---
title: Manage your apps with the Developer Portal
description: In this article, learn how to configure, distribute, and manage your apps using the Developer Portal for Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
---

# Manage your apps in Developer Portal

After you create or upload your app, you can manage your apps in Developer Portal with the following:

* [Overview](#overview)
* [Configure](#configure)
* [Advanced](#advanced)
* [Publish](#publish)

## Overview

In the **Overview** section, you can see the following components to manage your app:

* Dashboard

  * In the **Dashboard** under **Overview** section, you can see the following components for your app:
    * **Teams store validation**: App validation tool checks your app package against the test cases Microsoft uses when reviewing your app.
    * **Announcement**: Latest updates of your apps on Developer Portal for Teams
    * **Active users (Preview)**: Shows you the active user count
    * **Basic information**: Shows you the App ID, Version, Manifest version, and so on.

    :::image type="content" source="../../assets/images/tdp/dashboard-page.png" alt-text="The screenshot is an example that shows the Overview page of the app you created in Developer Portal for Teams.":::

* Analytics

    In the **Analytics** page under **Overview** section, you can see the total number of active users for your app. For more information, see [Analyze your app's usage](analyze-your-apps-usage-in-developer-portal.md).

## Configure

To install and render your app in Teams, you must include a set of configurations that Teams recognizes. To upload your apps in Teams, you need to have app manifest, which contains all the app details to display your app in Teams. This can be achieved with the help of components and tools that are available in Developer Portal.

In the **Configure** section, you can see the following components to manage and access your app:

* **Basic information**: This section shows and allows you to edit the App name, App ID, Descriptions, Version, Developer Information, App URLs, Application (client) ID, and Microsoft Partner Network ID.
* **Branding**: This page shows the app icon details.
* **App features**: You can add the following features to your app:
  * Personal app
  * Bot
  * Connector
  * Scene
  * Group and channel app
  * Messaging extension
  * Meeting extension
  * Activity feed notification
* **Permissions**: This section allows you to give Device permissions, Team permissions, Chat or Meeting permissions, and User Permissions for your app.
* **Single sign-on**: This section allows you to add App ID URI that is configured in the Azure AD for your app to authenticate users with single sign-on (SSO).

   > [!NOTE]
   > Developer Portal is not used to configure SSO, but it supports SSO configuration that is done for a bot app.

* **Languages**: You can set up or change the language of your app.
* **Domain**: You can add the domains to load your apps in the Teams client (For example: *.example.com).

:::image type="content" source="../../assets/images/tdp/configure.png" alt-text="The screenshot is an example that shows how to configure features to manage and access your app in Developer Portal.":::

## Advanced

In the **Advanced** section, you can see the following components to manage your app in Developer Portal:

* **Owners**

    Each app includes an **Owners** page, where you can share your app registration with others in your org. You can add **Administrator** and **Operative** role to manage who can change the settings of your app. The **Operative** role has the same permissions as the **Administrator** role except to delete an app.

    To add an owner:

    1. In the **Advanced** section, select **Owners**.
    1. Select **Add an owner**.
    1. Enter a name and select a user ID from the drop-down list.
    1. Under **Role**, select **Operative** or **Administrator**.
    1. Select **Add**.

* **App content**: You can configure your app with the following additional features:
  
  * Loading indicator: Displays an indicator to let users know your hosted app content (For example: Tabs and Task modules) is loading.
  * Full-screen mode: Displays a personal app without an app header. It's only supported for the published apps to your org.

* **Environments**

    You can configure environments and global variables to help transition your app from your local runtime to production. Global variables are used across all environments.

    To set up an environment:

    1. In the Developer Portal, select the **Apps** that you're working.
    1. Go to **Environments** under **Advanced** section and select **+ Add an environment**.
    1. Select **Add**.

  * **Global variables**

      1. Select **Add a global variable** to create configuration variables for your environment.

      To use global variables:

      Use the variable names instead of hard-coded values to set your app configurations.

      1. Enter `{{` in any field in the Developer Portal. A dropdown with all the variables you've created for the chosen environment along with the global variables appears.  
      1. Before downloading your app package (for example, when getting ready to publish to the Teams store), select the environment you want to use. Your app configurations update automatically based on the environment.

* **Plan and pricing**: You can link a SaaS offer that you've created in the Partner center for your app.
* **Admin settings**:
  * App Customization: You can customize your app
  * Block app by default: You can block your app by default for users until a tenant admin chooses to enable it.

## Publish

You can publish your app to your org or to the Teams store.

* **Publish your app to org**:

   1. In the app **Overview** page, under **Publish**, select **Publish to Org**.
   1. Select **Publish your App**.

* **Publish your app to store**:

   1. In the app **Overview** page, under **Publish**, select **Publish to Store**.
   1. Select **Publish**.

   > [!NOTE]
   > The app validation tool checks your app package against the test cases that Microsoft uses to review your app. Resolve errors or warnings and read the **App submission checklist** before submitting your app.

   You can download the app package by selecting **Download app package** button from the Publish to store page.

* **App package**: The app package describes how your app is configured that includes app features, required resources, and other important attributes in manifest. The Icon tab shows the icon used for your app.

## Test your app directly in Teams

The Developer Portal provides options for testing and debugging your app:

* On the **Overview** page, you can see a snapshot whether your app is configured and is validated against Teams store test cases.
* The **Preview in Teams** button launches your app quickly in the Teams client for debugging.

## Use tools to create app features

The Developer Portal also includes tools to help you build key features of Teams apps. The following are the tools:

* **Scene studio**: Design [custom Together Mode scenes](~/apps-in-teams-meetings/teams-together-mode.md) for Teams meetings.
* **Adaptive Cards editor**: Create and preview Adaptive Cards to include with your apps.
* **Microsoft identity platform management**: Register your apps with Azure Active Directory to help users sign in and provide access to APIs.
* **Teams store app validation**: Check your app package against the test cases that Microsoft uses to review your app.
* **Bot management**: Add conversational bots to your app that communicate with users, respond to their questions, and proactively notify them about changes and other events.

To add a bot:

1. In the Developer Portal, select **Tools** in the left pane.
1. Select the **Bot management**.
1. In the Bot management page, select **New Bot**.
1. Enter the name and select **Add**.

   :::image type="content" source="../../assets/images/tdp/tools-in-dev-portal.png" alt-text="The screenshot is an example that shows the tools in developer portal, which helps you to build key features.":::

From the Developer Portal, you can go to Bot Framework Portal and configure your bot to update icon and other properties.

## See also

[Include a SaaS offer with your Microsoft Teams app](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
