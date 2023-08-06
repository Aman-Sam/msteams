---
title: Teams Toolkit Visual Studio Overview
author: zyxiaoyuer
description: Learn about Teams Toolkit, it's installation, navigation, and user journey. Teams Toolkit is available for Visual Studio.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
---

# Teams Toolkit Visual Studio Overview

::: zone pivot="visual-studio-v17.6"

Teams Toolkit makes it simple to get started with app development for Microsoft Teams using Visual Studio.

* Start with a project templates for common line-of-business app scenarios or from a sample.
* Save setup time with automated app registration and configuration.
* Run and debug to Teams directly from familiar tools.
* Smart defaults for hosting in Azure using infrastructure-as-code and Bicep.
* Bring your app to your organization or the Teams App Store using built-in publishing tools.

:::image type="content" source="images/teams-toolkit-user-journey3VS-v4.png" alt-text="User Journey of the Teams Toolkit"  lightbox="images/teams-toolkit-user-journey3VS-v4.png":::

## Available for Visual Studio

Teams Toolkit v4 is available for free for Visual Studio 2022 Community, Professional, and Enterprise. For more information about installation and setup, see [install Teams Toolkit](./install-Teams-Toolkit-v4.md).

| Teams Toolkit | Visual Studio |
| - | ------------- |
| Installation | Available in the Visual Studio Installer |
| Build with | C#, .NET, ASP.NET, Blazor |

::: zone-end

## Features

The following list provides the key features of Teams Toolkit:

::: zone pivot="visual-studio-v17.6"

* [Project templates](#project-templates)
* [Automatic registration and configuration](#automatic-registration-and-configuration)

::: zone-end

### Project templates

You can start directly with the capability-focused templates such as tabs, bots, and message extensions or by following existing samples if you're already familiar with Teams app development. Teams Toolkit reduces the complexity of getting started with templates for common line-of-business app scenarios and smart defaults to accelerate your time to production.

::: zone pivot="visual-studio-v17.6"
:::image type="content" source="images/create-new-app-vs_2-v4.png" alt-text="Create new Teams app menu in VS Code":::
::: zone-end

### Automatic registration and configuration

You can save time and let the toolkit automatically register the app in Teams Developer Portal. When you first run or debug the app, configure settings, such as Azure Active Directory (Azure AD) automatically. Sign in with your Microsoft 365 account to control where the app is configured and customized the included Azure AD manifest when you need flexibility.

::: zone pivot="visual-studio-v17.6"

#### TeamsFx .NET SDK Reference docs

* [Microsoft.Extensions.DependencyInjection Namespace](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Microsoft.TeamsFx Namespace](/../dotnet/api/Microsoft.TeamsFx)
* [Microsoft.TeamsFx.Configuration Namespace](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Microsoft.TeamsFx.Conversation Namespace](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Microsoft.TeamsFx.Helper Namespace](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## See also

* [Build tabs for Teams](~/tabs/what-are-tabs.md)
* [Build bots for Teams](~/bots/what-are-bots.md)
* [Build Message extensions](~/messaging-extensions/what-are-messaging-extensions.md)
* [Create a new Teams app](create-new-project-v4.md)
* [Provision cloud resources](provision-v4.md)
* [Deploy Teams app to the cloud](deploy-v4.md)
* [Publish Teams apps](publish-v4.md)
