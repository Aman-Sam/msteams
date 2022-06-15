---
title: Collaborate on TeamsFx Project using Teams Toolkit
author: yanjiang
description: Collaborate on TeamsFx Project using Teams Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# Collaborate on Teams project using Teams Toolkit

Multiple developers can work together to debug, provision and deploy for the same TeamsFx project, but it requires manually setting the right permissions of Teams App and Microsoft Azure Active Directory (Azure AD) App. Teams Toolkit supports collaboration feature to allow developers and project owner to invite other developers or collaborators to the TeamsFx project to debug, provision, and deploy the same TeamsFx project.

## Prerequisites

* Microsoft 365 subscription
* Azure with valid subscription
  
  For more information on different accounts, see [prepare accounts to build Teams app](accounts.md).

* [Install Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+

> [!TIP]
> Ensure you have a Teams app project opened in Visual Studio Code.

## Collaborate with other developers

The following lists guide us to understand the collaboration process and its limitation:

* As project owner

  > [!NOTE]
  > Before adding collaborators for an environment, project owner needs to [provision](provision.md) the project first.

  1. In **ENVIRONMENT** section on Teams Toolkit, select **collaborators**. It displays the options **Add Microsoft 365 Teams App (with Azure AD App) Owners** and **List Microsoft 365 Teams App (with Azure AD App) Owners** as shown in the following images:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="collaborators":::

  2. Select **Add Microsoft 365 Teams App (with Azure AD App) Owners** and add other Microsoft 365 account email address as collaborator. The account to be added must be on the same tenant as project owner for remote debug as shown in the image:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add envi":::

  3. To view collaborators in current environment, select **List Microsoft 365 Teams App (with Azure AD App) Owners**, then collaborators are listed in the output channel as shown in following image:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

  4. Push the project to GitHub

     > [!NOTE]
     > The newly added collaborators do not receive any notification. The Project owner needs to notify collaborator.

* As project collaborator

  1. Clone the project from GitHub.
  2. Log on to Microsoft 365 account.
  3. Log on to Azure account, it has contributor permission for all the Azure resources, which are used in the project.
  4. To preview your Teams app, deploy the project to remote.
  5. Launch remote to have a preview of the Teams app.

     > [!NOTE]
     > Collaborators must log in using the account that project owner adds under the same tenant with project owner. For more information, see [build and run your Teams app in remote environment](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

### Limitations

If you want to remove collaborators from Teams Toolkit extension, you need to remove manually as you can't remove them directly. Perform the following steps to remove collaborators manually:

* Using Developer Portal

  * Go to [Teams Developer Portal](https://dev.teams.microsoft.com/home) and select your Teams app by name or app ID
  * Select **Owners** from left panel
  * Select and remove the collaborator

* Using Azure Active Directory

  * Go to [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), select **App registration** from left panel, and find your Azure AD App
  * Select **Owners** from left panel in Azure AD App management page
  * Select and remove the collaborator

   > [!NOTE]
   >
   > * Collaborator added to your project doesn't receive any notification. Project owner needs to notify collaborator offline.
   > * Azure related permissions must be set manually by Azure subscription administrator on Azure portal. Azure account must have contributor role for the subscription so that developers can work together to provision, and deploy TeamsFx project.

## See also

* [Provision cloud resources](provision.md)
* [Deploy Teams app to the cloud](deploy.md)
* [Manage multiple environments](TeamsFx-multi-env.md)
