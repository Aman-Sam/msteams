---
title: Collaborate on TeamsFx Project using Teams Toolkit
author: yanjiang
description:  Collaborate on TeamsFx Project using Teams Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# Collaborate on Teams project using Teams Toolkit

Multiple developers can work together to debug, provision and deploy for the same TeamsFx project, but it requires manually setting the right permissions of Teams App and Azure AD App.Teams Toolkit supports collaboration feature to allow  developers and project owner to invite other developers or collaborators to the TeamsFx project to debug, provision, and deploy the same TeamsFx project.

## Prerequisites

* Account prerequisites

    To provision cloud resources, you must have the following accounts. For more information, see, [prepare accounts to build Teams app](accounts.md).

  * Microsoft 365 subscription
  * Azure with valid subscription

* [Install Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Ensure you have a Teams app project opened in Microsoft Visual Studio code.

## Collaborate with other developers

The following list guides us to understand the collaboration process and its limitation:

### As project owner

> [!NOTE]
> Before adding collaborators for an environment, project owner needs to [provision](provision.md) the project first.

* In **ENVIRONMENT** section on Teams Toolkit, select **collaborators**. It displays the options **Add Microsoft 365 Teams App (with Microsoft Azure Active Directory (Azure AD) App) Owners** and **List Microsoft 365 Teams App (with Azure AD App) Owners** as shown in the following images:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="collaborators":::

* Select **Add Microsoft 365 Teams App (with Azure AD App) Owners** and add other Microsoft 365 account email address as collaborator. The account to be added must be on the same tenant as project owner for remote debug as shown in the image:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add envi":::

* To view collaborators in current environment, select **List Microsoft 365 Teams App (with Azure AD App) Owners**, then collaborators are listed in the output channel as shown in following image:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

* Push the project to GitHub.

> [!NOTE]
> Newly added collaborator doesn't receive any notification. Project owner needs to notify collaborator.

### As project collaborator

* Clone the project from GitHub.
* Log in to Microsoft 365 account.
* Log in to Azure account, which has contributor permission for all the Azure resources being used in this project.
* To preview your Teams app, deploy the project to remote.
* Launch remote to have a preview of the Teams app.

For more information, see [build and run your Teams app in remote environment](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

> [!NOTE]
> Collaborators must log in using the account added by project owner, which is under the same tenant with project owner.

### Limitation

You can't remove collaborators directly from Teams Toolkit extension. Perform the following steps to remove collaborators manually:

  1. Go to Teams Developer Portal and select your Teams app by name or app ID.
  2. Select **Owners** from left panel.
  3. Select and remove the collaborator.
  4. Go to [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), select **App registration** from left panel, and find your Azure AD App.
  5. Select **Owners** from left panel in Azure AD App management page.
  6. Select and remove the collaborator.

> [!NOTE]
> * Collaborator added to your project will not receive any notification. Project owner needs to notify collaborator offline.
> * Azure related permissions must be set manually by Azure subscription administrator on Microsoft Azure portal. Azure account must have contributor role for the subscription so that developers can work together to provision, and deploy TeamsFx project.

## See also

* [Provision cloud resources](provision.md)
* [Deploy Teams app to the cloud](deploy.md)
* [Manage multiple environments](TeamsFx-multi-env.md)
