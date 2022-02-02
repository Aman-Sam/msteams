---
title: Create a new Teams project Using Teams Toolkit
author: zyxiaoyuer
description:  Create new Teams project Using Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# Create a new Teams app using Teams Toolkit

Once you have Teams Toolkit installed you have two options for creating a new app. You can either start from a basic starter project using the **Create a new Teams app** option, or you can adapt a sample app by using the **View samples** option.

## Create a new Teams app using a new project

You can choose **Create a new Teams app** and then select from a number of capabilities: Tab, Bot, Messaging Extension, or a Tab using the SharePoint Framework (SPFx). You must choose at least one, but you can add as many of these capabilities to your Teams app as you need. The following guides help you to scaffold a new Teams starter app using each of them:

- [Create a new Teams Tab app (React)](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=2)
- [Create a new Teams Bot app](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&branch)
- [Create a new Message Extension app](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=6&branch)
- [Create a new Teams Tab app (SharePoint Framework)](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&branch)

## Create a new Teams app using sample code

You can also create a new project by exploring the **sample gallery** and choosing an existing sample as a starting point for your new app. These samples already have some functionality, for example a todo list with an Azure backend, or integration with the Microsoft Graph Toolkit. Follow these steps to create an app from one of the samples (if no folder is open in VS Code you'll skip step 2):

 1. Open **Teams Toolkit** from Visual Studio Code.
 1. Select **DEVELOPMENT** section in Tree View.
 1. Select **View samples**. The sample gallery appears as shown in the following image:
   
    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/view samples.png" alt-text="samples":::

You can explore and download samples and either run apps locally or remotely to preview in the Teams web client. Follow the instructions for each sample, or  choose **View on GitHub** to open the sample within the TeamsFx-Samples repository and browse the source code.

## See also

* [Provision cloud resources](provision.md)
* [Deploy Teams app to the cloud](deploy.md)
* [Publish your Teams app](TeamsFx-collaboration.md)
* [Manage multiple environments](TeamsFx-multi-env.md)
* [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)
