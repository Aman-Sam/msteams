---
title: Add Resources of Teams Toolkit v4 to Teams apps
author: MuyangAmigo
description: Learn how to add resources of Teams Toolkit v4, advantages, limitations, and capabilities.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# Add cloud resources of Teams Toolkit v4 to Teams app

> [!IMPORTANT]
>
> We've introduced the [Teams Toolkit v5](../teams-toolkit-fundamentals.md) extension within Visual Studio Code. This version comes to you with many new app development features. We recommend that you use Teams Toolkit v5 for building your Teams app.
>
> Teams Toolkit v4 extension will soon be deprecated.

Teams Toolkit allows you to provision the cloud resources for hosting your app. You can add the cloud resources according to your development needs. The advantage of adding more cloud resources in TeamsFx is that you can autogenerate all configuration files and connect to Teams app by using Teams Toolkit.

> [!NOTE]
> If you've created SharePoint Framework (SPFx) based tab project, you can't add Azure cloud resources.

## Add cloud resources

You can add cloud resources in the following ways:

### To add cloud resources by using Teams Toolkit in Microsoft Visual Studio Code

   1. Open your Teams app project in **Visual Studio Code**.
   1. Select **Teams Toolkit** from the Visual Studio Code activity bar.
   1. Select **Add features** in the **DEVELOPMENT** section.

        :::image type="content" source="images/select-feature-updated_1-v4.png" alt-text="Add feature from Teams Toolkit":::

### To add cloud resources by using Command Palette

   1. Open your Teams app project in Visual Studio Code.

   1. Select **View** > **Command Palette...** or **Ctrl+Shift+P**.

      :::image type="content" source="images/Teams-add-features-v4.png" alt-text="Add feature from command palette":::

   1. Select **Teams: Add features**.

      :::image type="content" source="images/Teams-add-features1_1-v4.png" alt-text="Type add feature and enter":::

      A list of cloud resources appears.

   1. Select the **Cloud resources** to add to your project.

      :::image type="content" source="images/updated-final-cloud_1-v4.png" alt-text="final":::

   You need to provision for each environment after you have successfully added the resource in your Teams app.

### Add cloud resources using TeamsFx CLI

* Before you add cloud resources, ensure that you change the directory to your **project directory**.
* The following table lists the capabilities and required commands:

  |Cloud Resource|Command|
  |---------------|----------|
  | **Azure Functions**|`teamsfx add azure-function`|
  | **Azure SQL Database**|`teamsfx add azure-sql`|
  | **Azure API Management**|`teamsfx add azure-apim`|
  | **Azure Key Vault**|`teamsfx add azure-keyvault`|

## Types of cloud resources

In the following scenarios, TeamsFx integrates the Azure services with your Teams app:

* [Azure Functions](/azure/azure-functions/functions-overview): A serverless solution to meet your on-demand requirements, such as creating web APIs for your Teams app back-end.
* [Azure SQL Database](/azure/azure-sql/database/sql-database-paas-overview): A platform as a service (PaaS) database engine to serve as your Teams app data store.
* [Azure API Management](deploy.md): An API gateway can be used to administer APIs created for Teams apps and publish them so other apps can consume them, such as Power app.
* [Azure Key Vault](/azure/key-vault/general/overview): Safeguard cryptographic keys and other secrets used by cloud apps and services.

## Changes after adding Azure resources

The following changes appear after adding Azure cloud resources in your project:

* New parameters added to `azure.parameter.{env}.json` to provide the required information for provision.
* New content is included to ARM template under `templates\azure`. The files are in `templates\azure\teamsfx` folder for the Azure resources.
* Teams Toolkit regenerates the files under `templates\azure\teamsfx` folder to ensure configuration required for TeamsFx is up to date for added Azure resources.
* `.fx\configs\projectSettings.json` is updated to track the available resources in your project.

The following additional changes appear after adding resources in your project:

|Resources|Changes|Description|
|---------------|---------------|-----------------------------|
|**Azure Functions**|The Azure Functions template code is added into a subfolder with path `yourProjectFolder\api`</br></br>`launch.json` and `task.json` are updated under `.vscode` folder.| Includes a hello world http trigger template into your project.</br></br> Includes necessary scripts for Visual Studio Code to be executed when you want to debug your app locally.|
|**Azure API Management**|An open API specification file added into a subfolder with path `yourProjectFolder\openapi`.|Defines your API after publishing. It's the API specification file.|

## See also

* [Teams Toolkit Overview](teams-toolkit-fundamentals.md)
* [Provision cloud resources](provision.md)
* [Create a new Teams app](create-new-project.md)
* [Add capabilities to Teams apps](add-capability-v4.md)
* [Deploy to the cloud](deploy.md)
