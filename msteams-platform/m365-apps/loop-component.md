---
title: Guidelines for building Loop components
description: In this article, learn how to build a Adaptive card based Loop component.
ms.author: mobajemu
ms.date: 06/15/2023
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
---

# Guidelines for building Loop components

## Overview

Loop component is an evolution of Fluid component - a way to collaborate with a team through loop whether it’s in chat, email, meeting, or Loop page. Loop component stays in sync no matter how many places the content lives across Microsoft 365 apps.

Adaptive Card-based Loop component allows M365 developers to build Loop experiences while building upon their existing message extension-based M365 integrations. With AC-based Loop components, users are empowered to bring live business data into chats and email messages, and complete workflows without switching apps . For developers, components adhere to M365 platform's 'build once, works everywhere' philosophy which ensure that your Loop component will automatically work seamlessly across Teams and Outlook, and in every additional host app enabled, including the new Loop app.

> [!NOTE]
> Adaptive Card-based Loop components are available in public preview.

## Getting started

There are a few pre-requisites needed before building an Adaptive Card-based Loop component:

> [!div class="checklist"]
>
> 1. Build a search-based Message Extension
> 1. Add link unfurling support to the Message Extension
> 1. Use Universal Actions for Adaptive Cards
> 1. Extend your Teams Message Extension across Microsoft 365

In the subsequent sections we dive deeper into these pre-requisites.

### Build a search-based message extension

To begin building an Adaptive Card based Loop component, firstly follow the steps to [build a Message Extension with a Search command and Link unfurling](../messaging-extensions/what-are-messaging-extensions.md).

[Search commands](../sbs-messagingextension-searchcommand.yml) allow end-users to search an external system for information. The users can select an item from the search result and insert them in chat and mail as a rich interactive card. The inserted card is the [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)-based Loop component.

### Add link unfurling support

[Link unfurling](../messaging-extensions/how-to/link-unfurling.md) allows for unfurling URLs inserted in a chat or mail message body into a rich, live, and actionable card. Link unfurling improves the user experience by letting users complete a task in their context while also providing a rich preview of the underlying content. Additionally, link unfurling support is essential to make the experience portable across Teams and Outlook.

### Use Universal Actions for Adaptive Cards

[Universal Actions](../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md) for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both Teams and Outlook. Your Message Extension app must use [Adaptive Card spec 1.6](https://github.com/microsoft/adaptivecards/pull/7105) in your AC payloads to support actionability across Teams and Outlook hubs.

### Extend your Teams message extension across Microsoft 365

Extending your message across Microsoft 365 products allows you to build your extension once and run it everywhere available within Microsoft 365. It entails updating the app manifest, adding the Microsoft 365 channel to your bot, and sideloading it into Microsoft Teams. For more details, refer to the topic, [Extending a Teams message across Microsoft 365](extend-m365-teams-message-extension.md).

## Build Loop components

Once you have met all the requirements, you can now upgrade the Adaptive Card into a Loop component that is rich, actionable, and portable across Microsoft 365 applications. There are two steps to building a Loop component based Adaptive Card:

1. Ensure the Adaptive Card adheres to the [Loop component UX guidelines](loop-ux-guide.md) to build an actionable and coherent Adaptive Card based experience for your end users.
1. Enable Loop component by including the URL that uniquely identifies the card in the [metadata.webUrl](https://adaptivecards.io/explorer/Metadata.html) field of your Adaptive Card payload. This is required to support portability via the Copy button present in the Loop header.

## Test your Loop component

### Setup your dev environment to test in Teams

To configure, distribute, and manage your application use the Developer Portal for Teams. More detailed instructions on registering your application can be found at [Manage your apps with the Developer Portal](../concepts/build-and-test/teams-developer-portal.md). The Developer Portal provides options for testing and debugging your app:

- On the **Overview page**, you can see a snapshot of whether your app's configurations validate against Teams store
  test cases.
- The **Preview in Teams** button lets you launch your app quickly in the Teams client for debugging.

:::image type="content" source="images/developer-portal-overview.png" alt-text="A screenshot of the Developer Portal overview page with the Preview in Teams button highlighted":::

### Setup your dev environment to test in Outlook

To turn on the Adaptive Card based Loop component in Outlook.com:

1. Follow the steps on [Teams App Camp (microsoft.github.io)](https://microsoft.github.io/app-camp/) to create a search-based ME.
1. Create a M365 dev tenant following [these steps](https://developer.microsoft.com/en-us/microsoft-365/dev-program) or login with your test tenant credentials.
1. In the admin center of your test tenant, [enable Targeted Release for everyone](../microsoft-365/admin/manage/release-options-in-office-365.md).
1. Send an email from the tenant admin account to the help alias: acloops-preview-help@microsoft.com. Microsoft will verify the admin user and enable support for Loop components for this tenant.

   > [!NOTE]
   > For any help in building Adaptive Card-based Loop components reach out to acloops-preview-help@microsoft.com.

1. The Adaptive Card generated by your app now should be rendered as a Loop component
