---
title: Prepare to build apps with Teams Toolkit
author: surbhigupta
description: Learn about build environments such as SPFx of Teams Toolkit in Visual Studio Code. Toolkit integrates Azure Functions capabilities for building apps.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# Prepare to build apps using Teams Toolkit

Teams Toolkit supports different environments for creating apps. Teams Toolkit helps to integrate Azure Functions capabilities and cloud services in the Teams app that you've built.

:::image type="content" source="../assets/images/buildapps-TTK_1.png" alt-text="Prepare to build apps using Teams Toolkit" lightbox="../assets/images/buildapps-TTK_1.png":::

## Build environments

Teams Toolkit in Visual Studio Code offers set of environments to build your Teams app. You can choose any of the following environments:

* JavaScript or TypeScript
* SharePoint Framework (SPFx)

### Create your Teams app using JavaScript or TypeScript

The apps built with JavaScript or TypeScript have the following advantages:

* App comes with its own UI and UX capabilities that are rich and user friendly.
* Provides quick upgrades to the existing apps.
* Distributes apps on multiple platforms, such as Android and iOS.
* Compatible for creating an app with the existing APIs.

Teams Toolkit in Visual Studio Code supports building the following apps using JavaScript or TypeScript:

* Tab app: Your tab app can have web-based content. You can have a custom tab for your web content in Teams or add Teams-specific functionality to your web content.
* Bot app: Bot can be chatbot or conversational bot that allows you to do simple and repetitive tasks such as customer service or support staff.
* Notification bot: You can send messages in Teams channel or group or personal chat by notification bots with HTTP request.
* Command bot: You can automate repetitive tasks using a command bot. Command bot helps you to respond simple queries or commands sent in chats.
* Workflow bot: You can interact with an Adaptive Card enabled by the Adaptive Card action handler feature in the workflow bot app.
* Message extension: You can interact with your web service through buttons and forms in the Microsoft Teams client.

### Create your Teams app using SPFx

Teams Toolkit in Visual Studio Code allows you to create tab app using SPFx. This app has the following advantages:

* Provides easy integration with data residing in SPFx to your Teams.
* Integrates your SPFx solution with your business APIs secured with Microsoft Azure Active Directory (Azure AD).
* Gives you access to various open-source tools.
* Creates powerful applications that can deliver a great UX.
* Integrates with other Microsoft 365 workloads easily.
* Delivers flexibility to host applications wherever needed.

## Support for Azure Functions

You can use Teams Toolkit to integrate [Azure Functions](/azure/azure-functions/functions-overview) capabilities into building apps. You can focus on the pieces of code that matter, and Azure Functions handles the rest.
Azure Functions provides "compute on-demand" in two significant ways:

1. Allows you to implement system's logic into your readily available blocks of code. These blocks are called functions.
1. Meets the requirement with as many resources and function instances as necessary as the requests increase.

Azure Functions integrates with an array of [cloud services](add-resource.md#types-of-cloud-resources) to provide feature-rich implementations. The following are the common scenarios for Azure Functions:

* Building a web API
* Processing to database changes
* Processing IoT data streams
* Managing message queues

## See also

* [Teams Toolkit Overview](teams-toolkit-fundamentals.md)
* [Developer Portal for Teams](../concepts/build-and-test/teams-developer-portal.md)
* [Create a new Teams project](create-new-project.md)
* [Build your first Teams app](../get-started/get-started-overview.md#build-your-first-teams-app)
