---
title: Get started - Prerequisites
author: adrianhall
description: Learn how to get started with Microsoft Teams app development and set up your environment.
ms.author: adhal
ms.date: 05/19/2021
ms.topic: quickstart
---
# Prerequisites: Get started with Microsoft Teams app development

Before your create your first Teams app, you must install a few tools and set up your development environment.

## Install required tools

Some of the tools you need depend on how you you prefer to build your Teams app:

- [Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release) 
- A browser with developer tools - such as [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)
- If you're developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.  
- If you're developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).  Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.

> [!WARNING]
> There are known issues with `npm@7`, packaged with Node v15 and later. If you have problems running `npm install`, ensure you're using Node v14 (LTS)

## Install the Teams Toolkit

The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more. You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).

# [Visual Studio Code](#tab/vscode)

1. Open Visual Studio Code.
1. Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).
1. In the search box, enter _Teams Toolkit_.
1. Select on the green install button next to the Teams Toolkit.

You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

The following tools will be installed by the Visual Studio Code extension when they are needed.  If already installed, the installed version will be used instead.  If using Linux (including WSL), you must install these tools before use:

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.  It is installed within the project directory (using the npm `devDependencies`).

- [.NET SDK](/dotnet/core/install/)

    The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.  If you have not installed the .NET 3.1 (or later) SDK globally, the portable version will be installed.

- [ngrok](https://ngrok.com/download)

    Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.  You need to expose your development system to Teams through a tunnel.  A tunnel is not required for apps that only include tabs.  This package is installed within the project directory (using npm `devDependencies`).

# [Visual Studio 2019](#tab/vs)

You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.  If you're not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.

To install the Teams Toolkit extension:

1. Open Visual Studio 2019.
1. Select **Extensions** > **Manage Extensions**.
1. In the search box, enter _Teams Toolkit_.
1. Select the Teams Toolkit extension and select **Download**.

The extension will be downloaded.  Close Visual Studio 2019 to install the extension.

# [Command line](#tab/cli)

To install the TeamsFX CLI, use the `npm` package manager:

``` bash
npm install -g @microsoft/teamsfx-cli
```

Depending on your configuration, you may need to use `sudo` to install the CLI:

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

This is more common on Linux and macOS systems.

Ensure you add the npm global cache to your PATH.  This is normally done as part of the Node.js installer.  

You can use the CLI with the `teamsfx` command.  Verify that the command is working by running `teamsfx -h`.

> [!CAUTION]
> Before you can run TeamsFX in PowerShell terminals, you need to enable the "remote signed" execution policy for PowerShell.  For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).

---

## Install optional tools

Install browser tools for app development. For instance, if your app is written with React, you can use React Developer Tools:

- [React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:

- [Azure Tools for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer. This browser-based tool allows you to query Microsoft Graph outside of an app.

- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)

With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app (including to your org or the Teams store).

- [Developer Portal for Teams](https://dev.teams.microsoft.com/)

## Enable side-loading

During development, you will need to load your app within Teams without distributing it.  This is known as "sideloading".

1. If you have a Teams account, verify if you can sideload apps in Teams:

    1. In the Teams client, select **Apps**.
    1. Look for an option to **Upload a custom app**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Illustration showing where in Teams you can upload a custom app.":::

> [!NOTE]
> If you still can't sideload apps, talk to your Teams administrator. See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.

## Get a free Teams developer tenant (optional)

If you cannot see the sideload option, or you don't have a Teams account, you can get a free Teams developer account by joining the M365 developer program.  The registration process takes approximately two minutes.

1. Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).
1. Select **Join Now*- and follow the onscreen instructions.
1. When you get to the welcome screen, select **Set up E5 subscription**.
1. Set up your administrator account. Once you finish, you should see a screen like this.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Example of what you see after signing up for the Microsoft 365 developer program.":::

1. Log in to Teams using the administrator account you just set up.
1. Verify if you now have the **Upload a custom app** option.

## Get a free Azure account

If you wish to host your app or access resources within Azure, you will need an Azure subscription.  You can [create a free account](https://azure.microsoft.com/free/) before you begin.

## Sign in to your Microsoft 365 and Azure accounts

You will need access to two accounts:

- Your Microsoft 365 account credentials. This is the account that you use to sign in to Teams. If you're using an Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.
- - Your Azure credentials. This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.

# [Visual Studio Code](#tab/vscode)

1. Open Visual Studio Code
1. Select the Teams icon in the sidebar:

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="The Teams Icon in the Visual Studio Code sidebar.":::

1. Select **Sign in to M365**.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Location of the Accounts section used to sign-in.":::

1. The sign-in process will start using your normal web browser.  Complete the sign-in process for your M365 account.  You will be prompted when you can close the browser and return to Visual Studio Code.
1. Return to the Teams Toolkit within Visual Studio Code.
1. Select **Sign in to Azure**.

    > [!TIP]
    > If you have the Azure Account extension installed and are using the same account, you can skip this step.  You will automatically use the same account as you are using in other extensions.

1. The sign-in process will start using your normal web browser.  Complete the sign-in process for your Azure account.  You will be prompted when you can close the browser and return to Visual Studio Code.

When complete, the **ACCOUNTS** section of the sidebar will show the two accounts separately, together with the number of usable Azure subscriptions available to you.  Ensure you have at least one usable Azure subscription available.  If not, sign out and use a different account.

# [Visual Studio 2019](#tab/vs)

Visual Studio 2019 will prompt you to log in to each service as it is needed.  You do not need to sign in to your M365 and Azure accounts in advance.

# [Command line](#tab/cli)

1. Sign in to Microsoft 365 with the TeamsFX CLI:

    ``` bash
    teamsfx account login m365
    ```

    The sign-in process will start using your normal web browser.  Complete the sign-in process for your M365 account.  You will be prompted when you can close the browser.

2. Sign in to Azure with the TeamsFX CLI:

    ``` bash
    teamsfx account login azure
    ```

    The sign-in process will start using your normal web browser.  Complete the sign-in process for your Azure account.  You will be prompted when you can close the browser.

The account logins are shared between Visual Studio Code and the TeamsFX CLI.

---

## Next steps

Now that your development environment is configured, you can create, build, and deploy your first Teams app.

- [Create your first Teams app using React](first-app-react.md)
- [Create your first Teams app with Blazor](first-app-blazor.md)
- [Create your first Teams app using SharePoint Framework (SPFx)](first-app-spfx.md)
- [Create a conversational bot app](first-app-bot.md)
- [Create a messaging extension](first-message-extension.md)
