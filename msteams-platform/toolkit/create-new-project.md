---
title: Create a new Teams app
author: zyxiaoyuer
description: In this module, learn how to create a new Teams app using Teams Toolkit using Visual Studio Code.
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
zone_pivot_groups: teams-toolkit-platform
---
::: zone pivot="visual-studio-code-v5"

# Create a new Teams app

In this section, you can learn how to create a new Teams project using Microsoft Visual Studio Code.

## Create a new Teams project using Visual Studio Code

You can build a new Teams project by selecting **Create a New App** in Teams Toolkit. You can start from built-in Teams app templates or start from official Teams app samples in Teams Toolkit. What's more, Teams Toolkit v5 supports to start with Outlook Add-in templates to build your own Outlook Add-ins.

:::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-capabilities-tabapp_1.png" alt-text="Screenshot shows the App Capability options.":::

To start with Teams capabilities, you can create the following types of Teams app:

| App Types | Definition |
| --- | --- |
| **Scenario-based Teams apps** | This group of templates are designed for particular abstracted business scenarios that your teams app can serve for. For example notification bot, command bot, SSO-enabled tab, or Dashboard tab app. |
| **Basic Teams apps** | Basic Teams apps are just hello world Teams tab, bot, or message extension that you can create and customize based on your requirement. |
| **Extend Teams App across Microsoft 365** | This group of Teams app can be installed and run on Outlook and Office.com. |

## Create a new Teams app

The process to create a new Teams app is similar for all types of apps.

To create a basic Teams app:

1. Open **Visual Studio Code**.

1. Select the **Teams Toolkit** > **Create a New App**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/create-project.png" alt-text="Screenshot shows the Create New Project button in the Teams Toolkit sidebar.":::

1. In this example, select **Tab** as app capability.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-capabilities-tabapp_1.png" alt-text="Screenshot shows the App Capability to select.":::

1. Select **Basic Tab** as app capability.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-basic-tab.png" alt-text="Screenshot shows to select App Feature using a Tab as Basic Tab.":::

1. Select **JavaScript** as the programming language.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-language-tab_1.png" alt-text="Screenshot shows the programming language to select.":::

1. Select **Default folder** to store your project root folder in the default location.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-default-location.png" alt-text="Screenshot shows the default location option to select.":::

    <details>
    <summary>Learn to change the default folder:</summary>

    1. Select **Browse**.

        :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-browse_1.png" alt-text="Screenshot shows the Browse option highlighted to browse for storage.":::

    1. Select the location for project workspace.

        :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder_1.png" alt-text="Screenshot shows the Select Folder option highlighted.":::

    The folder you select is the location for your project workspace.
    </details>

    1. Enter a suitable name for your app, such as helloworld, as the application name. Ensure that you use only alphanumeric characters. Press **Enter**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/enter-name-tab1.png" alt-text="Screenshot shows where to enter the app name.":::

   The Teams tab app is created in a few seconds.

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/tab-app-created.png" alt-text="Screenshot shows the app created." lightbox="../assets/images/teams-toolkit-v2/first-tab/tab-app-created.png":::

### Directory structure for different app types

Teams Toolkit provides all components for building an app. After creating the project, you can view the project folders and files under **EXPLORER** section.

<br>
<details>
<summary><b>Directory structure for basic Teams app</b></summary>

The following example shows a basic Teams tab app directory structure:

| Folder name | Contents |
| --- | --- |
| `.vscode` | Settings for VS Code to build and debug your Teams app. |
| `appPackage` | App manifest(previously called Teams app manifest) file and icon files that Teams used to recognize your Teams app. |
| `env` | Stores different environment parameters. |
| `infra` | Azure `bicep` template files. Used for deploy your Teams app to Azure. |
| `src` | Source code for the Tab capability, including your front-end app, UI components and the privacy notice, terms of use, |
| `src\components\` | The main app which handles the initialization and routing. |
| `src\index.jsx` | Entry point for the front-end app. |
| `teamsapp.yml` | This configuration file defines the Teams Toolkit behavior for provision, deploy, and publish lifecycle. You can customize this file to change the behavior of Teams Toolkit in each lifecycle. |
| `teamsapp.local.yml` | This overrides teamsapp.yml with actions that enable local execution and debugging. |

> [!NOTE]
> If you have a bot or message extension app, relevant folders are added to the directory structure.

To learn more about the directory structure of different types of basic Teams apps, see the following table:

| App Type | Links |
| --- | --- |
| For tab app | [Build your first tab app using JavaScript](../sbs-gs-javascript.yml) |
| For bot app | [Build your first bot app using JavaScript](../sbs-gs-bot.yml) |
| For message extension app | [Build your first message extension app using JavaScript](../sbs-gs-msgext.yml) |

</details>
<br>
<details>
<summary><b>Directory structure for scenario-based Teams app</b></summary>

The following example shows a scenario-based notification bot Teams app directory structure:

The new project folder contains the following content:

| Folder name | Contents |
| --- | --- |
| `.vscode` | Settings for VS Code to build and debug your Teams app. |
| `appPackage` | App manifest file and icon files that Teams used to recognized your Teams app. |
| `env` | Stores different environment parameters. |
| `infra` | Azure `bicep` template files. Used for deploy your Teams app to Azure. |
| `teamsapp.yml` | This configuration file defines the Teams Toolkit behavior for provision, deploy, and publish lifecycle. You can customize this file to change the behavior of Teams Toolkit in each lifecycle. |
| `teamsapp.local.yml` | This overrides teamsapp.yml with actions that enable local execution and debugging. |

The core notification implementation is stored in the **src** folder and it contains:

| File name | Contents |
| --- | --- |
| `src\adaptiveCards\` | Templates for Adaptive Card. |
| `src\internal\` | Generated initialize code for notification functionality. |
| `src\index.ts` | The entry point to handle bot messages and send notifications. |
| `.gitignore` | File to exclude local files from the bot project. |
| `package.json` | The npm package file for the bot project. |

> [!NOTE]
> If you have a command bot, workflow bot, SSO-enabled tab, or SPFx tab app, relevant folders are added to the directory structure.

To learn more about the directory structure of different types of scenario-based Teams apps, see the following table:

| App Type | Links |
| --- | --- |
| For notification bot app | [Send notification to Teams](../sbs-gs-notificationbot.yml) |
| For command bot app | [Build command bot](../sbs-gs-commandbot.yml) |
| For workflow bot app | [Create Teams workflow bot](../sbs-gs-workflow-bot.yml) |
| For SPFx tab app | [Build a Teams app with SPFx](../sbs-gs-spfx.yml) |

</details>
<br>

## See also

* [Teams Toolkit Overview](teams-toolkit-fundamentals.md)
* [Build a Teams app with Blazor](../sbs-gs-blazorupdate.yml)
* [Build a Teams app with C# or .NET](../sbs-gs-csharp.yml)
* [Prerequisites for all types of environment and create your Teams app](tools-prerequisites.md)
* [Prepare to build apps using Microsoft Teams Toolkit](build-environments.md)

::: zone-end

::: zone pivot="visual-studio-code-v4"

## Create a new Teams project using Teams Toolkit

> [!IMPORTANT]
>
> We've introduced the [Teams Toolkit v5](~/toolkit/teams-toolkit-fundamentals.md) extension within Visual Studio Code. This version comes to you with many new app development features. We recommend that you use Teams Toolkit v5 for building your Teams app.
>
> Teams Toolkit v4 extension will soon be deprecated.

In this section, you can learn how to create a new Teams project using Microsoft Visual Studio Code and Visual Studio.

## Create a new Teams project for Visual Studio Code

You can build a new Teams project by selecting **Create a new Teams app** in Teams Toolkit. You can create the following types of apps in Teams Toolkit:

| App Types | Definition |
| --- | --- |
| **Basic Teams apps** | Basic Teams apps are tab, bot, or message extension that you can create and customize based on your requirement. |
| **Scenario-based Teams apps** | Scenario-based Teams apps are notification bot, command bot, workflow bot, SSO-enabled tab, or SPFx tab app and these are suitable for one particular scenario. For example, a notification bot is suitable to send notifications and not used for chat. |

## Create a new Teams app

The process to create a new Teams app is similar for all types of apps except SPFx tab app, workflow bot, and notification bot.

**To create a basic Teams app**:

1. Open **Visual Studio Code**.

1. Select the **Teams Toolkit** > **Create a new Teams app**.

    :::image type="content" source="toolkit-v4/images/create-project-v4.png" alt-text="screenshot shows the Create New Project button in the Teams Toolkit sidebar.":::

1. Select **Start with a Teams capability**.

    :::image type="content" source="toolkit-v4/images/select-app-type-v4.png" alt-text="Screenshot shows the option to select app type." lightbox="toolkit-v4/images/select-app-type-v4.png":::

1. Ensure that **Tab** is selected as app capability.

    :::image type="content" source="toolkit-v4/images/select-capabilities-tabapp_1-v4.png" alt-text="Select App Capability":::

1. Select **JavaScript** as the programming language.

    :::image type="content" source="toolkit-v4/images/select-language-tab_1-v4.png" alt-text="Screenshot showing how to select the programming language.":::

1. Select **Default folder** to store your project root folder in the default location.

    :::image type="content" source="toolkit-v4/images/select-default-location-v4.png" alt-text="Select default location":::

    <details>
    <summary>Learn to change the default folder:</summary>

    1. Select **Browse**.

        :::image type="content" source="toolkit-v4/images/select-browse_1-v4.png" alt-text="Select browse for storage":::

    1. Select the location for project workspace.

        :::image type="content" source="toolkit-v4/images/select-folder_1-v4.png" alt-text="select-folder for storage":::

    The folder you select is the location for your project workspace.
    </details>

1. Enter a suitable name for your app, such as helloworld, as the application name. Ensure that you use only alphanumeric characters. Press **Enter**.

    :::image type="content" source="toolkit-v4/images/enter-name-tab1-v4.png" alt-text="Screenshot showing where to enter the app name.":::

    By default, your app project opens in a new window. You can open your app project in the current window as well.

    :::image type="content" source="toolkit-v4/images/new-window-notification-v4.png" alt-text="New window notification":::

   The Teams tab app is created in a few seconds.

    :::image type="content" source="toolkit-v4/images/tab-app-created-v4.png" alt-text="Screenshot showing the app created." lightbox="toolkit-v4/images/tab-app-created-v4.png":::

### Directory structure for different app types

Teams Toolkit provides all components for building an app. After creating the project, you can view the project folders and files under **EXPLORER** section.

<br>
<details>
<summary><b>Directory structure for basic Teams app</b></summary>

The following example shows a basic Teams tab app directory structure:

| Folder name | Contents |
| --- | --- |
| `.fx\configs` | Configuration files that you can customize for the Teams app. |
| - `.fx\configs\azure.parameters.<envName>.json` | Parameters file for Azure bicep provision for every environment. |
| - `.fx\configs\config.<envName>.json` | Configuration file for every environment. |
| - `.fx\configs\projectSettings.json` | Global project settings that apply to all environments. |
| `tabs` | Code for the Tab capability needed at runtime, such as the privacy notice, terms of use, and configuration tabs. |
| - `tabs\src\index.jsx` | Entry point for the front-end app, where the main app component is rendered with `ReactDOM.render()`. |
| - `tabs\src\components\App.jsx` | Code for handling URL routing in the app. It calls the [Microsoft Teams JavaScript client library](~/tabs/how-to/using-teams-client-library.md) to establish communication between your app and Teams. |
| - `tabs\src\components\Tab.jsx` | Code to implement the UI of your app. |
| - `tabs\src\components\TabConfig.jsx` | Code to implement the UI that configures your app. |
| `templates\appPackage` | App manifest template files, and the app icons: color.png and outline.png. |
| - `templates\appPackage\manifest.template.json` | App manifest for running the app in local or remote environment.  |
| `templates\azure` | `bicep` template files. |

> [!NOTE]
> If you have a bot or message extension app, relevant folders are added to the directory structure.

To learn more about the directory structure of different types of basic Teams apps, see the following table:

| App Type | Links |
| --- | --- |
| For tab app | [Build your first tab app using JavaScript](~/sbs-gs-javascript.yml) |
| For bot app | [Build your first bot app using JavaScript](~/sbs-gs-bot.yml) |
| For message extension app | [Build your first message extension app using JavaScript](~/sbs-gs-msgext.yml) |

</details>
<br>
<details>
<summary><b>Directory structure for scenario-based Teams app</b></summary>

The following example shows a scenario-based notification bot Teams app directory structure:

The new project folder contains the following content:

| Folder name | Contents |
| --- | --- |
| `.fx` | Project level settings, configuration, and environment information. |
| `.vscode` | VS code files for local debug. |
| `bot` | The bot source code. |
| `templates` | Templates for app manifest and corresponding Azure resources. |

The core notification implementation is stored in the **bot** folder, and it contains:

| File name | Contents |
| --- | --- |
| `src\adaptiveCards\` | Templates for Adaptive Card.  |
| `src\internal\` | Generated initialize code for notification functionality. |
| `src\index.ts` | The entry point to handle bot messages and send notifications. |
| `.gitignore` | File to exclude local files from the bot project. |
| `package.json` | The npm package file for the bot project. |

> [!NOTE]
> If you have a command bot, workflow bot, SSO-enabled tab, or SPFx tab app, relevant folders are added to the directory structure.

To learn more about the directory structure of different types of scenario-based Teams apps, see the following table:

| App Type | Links |
| --- | --- |
| For notification bot app | [Send notification to Teams](~/sbs-gs-notificationbot.yml) |
| For command bot app | [Build command bot](~/sbs-gs-commandbot.yml) |
| For workflow bot app | [Create Teams workflow bot](~/sbs-gs-workflow-bot.yml) |
| For SPFx tab app | [Build a Teams app with SPFx](~/sbs-gs-spfx.yml) |

</details>
<br>
<details>
<summary><b>Directory structure for multi-capability app</b></summary>

You can add more features to your existing Teams app by using **Add features**. For example, if you add a bot app to the existing tab app, Teams Toolkit adds the bot folder with relevant files and code.

The following image shows the directory structure of a tab app:

   :::image type="content" source="toolkit-v4/images/tabapp-directory-v4.png" alt-text="Tab app directory structure":::

The following image shows the directory structure of tab app with bot feature:

   :::image type="content" source="toolkit-v4/images/tab-app-with-bot-app-v4.png" alt-text="Tab app with bot app directory structure":::

</details>

## See also

* [Teams Toolkit Overview](~/toolkit/teams-toolkit-fundamentals.md)
* [Build a Teams app with Blazor](~/sbs-gs-blazorupdate.yml)
* [Build a Teams app with C# or .NET](~/sbs-gs-csharp.yml)
* [Prerequisites for all types of environment and create your Teams appPre](~/toolkit/tools-prerequisites.md)
* [Prepare to build apps using Teams Toolkit](~/toolkit/build-environments.md)
* [Provision cloud resources](~/toolkit/provision.md)
* [Deploy Teams app to the cloud](~/toolkit/deploy.md)

::: zone-end
