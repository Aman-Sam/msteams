---
title: Teams Toolkit Overview
author: zyxiaoyuer
description: In this module, learn Teams Toolkit, Installation of Teams Toolkit, and User journey of Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
---

# Teams Toolkit Overview

Teams Toolkit lets you create, debug, and deploy your Teams app right from Visual Studio Code.App development with the toolkit has the following advantages:

* Integrated identity
* Access to cloud storage
* Data from Microsoft Graph
* Azure and Microsoft 365 services with zero-configuration approach.

For Teams app development, similar to Teams Toolkit for Visual Studio, you can use [CLI tool](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), which consists of Toolkit `teamsfx`.

Teams Toolkit brings all tools needed for building a Teams app in one place.

## User journey of Teams Toolkit

Teams Toolkit automates manual work and provides great integration of Teams and Azure resources. The following image shows Teams Toolkit user journey:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey1.png" alt-text="User Journey of the Teams Toolkit" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

The main milestones of this journey are:

1. Start by creating a new project or trying a sample Teams app.
1. Add capabilities or edit manifest file as needed.
1. Use Microsoft 365 account to build and debug your Teams app.
1. Use Azure account to provision and deploy your app to cloud.
1. Publish your app to Teams.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-overview.png" alt-text="Teams Toolkit flow":::

## Manage your apps using Developer Portal

As Teams Toolkit is integrated with Developer Portal, you can configure, distribute, and manage your app using [Developer Portal for Teams](../concepts/build-and-test/teams-developer-portal.md) under DEPLOYMENT after creating an app. For more information, see [manage your Teams apps using Developer Portal](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Teams Toolkit flow":::
