---
title: Install Collaboration controls
author: surbhigupta
description: In this article, learn about installation of collaboration controls.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
---

# Install Collaboration controls

In this article, you'll learn how to install Collaboration Controls. The following are required to build and deploy Collaboration Manager applications using the Collaboration controls:

* **Power apps**: To build Model Driven Applications using the Collaboration controls.
* **M365 E3 or higher**: To deploy custom applications to Microsoft Teams and store tasks in Planner, files in SharePoint, and meetings in Outlook.

To install the components into a Power Platform environment the following roles are required:

* System customizer
* Environment maker

For more information on role privileges, see [Configure user security in an environment](/power-platform/admin/database-security#predefined-security-roles)

## Install the Collaboration controls solutions

You'll install the Collaboration controls into your dataverse environment via a private link. This link must not be shared with any other person inside or outside your organization.

You'll be able to configure and use the components within your own model-driven app only after receiving the link and installing Collaboration controls into your dataverse environment.

Collaboration Controls include the following solutions:

|**Settings solutions** | **Purpose** |
|---|---|
| Collaboration controls Settings | Hold the settings infrastructure that powers Collaboration controls |
| Collaboration controls Settings Objects | Provides pre-defined settings values that are used by the Collaboration controls.|

|**Collaboration solutions** | **Purpose** |
|---|---|
| Collaboration controls Tasks  | Includes the Tasks PCF (Power Apps component framework) control. |
| Collaboration controls Events | Includes the Events PCF control for Outlook and Teams meetings and bookings appointments. |
| Collaboration controls Notes | Includes the notes PCF control, which stores notes in Dataverse. |
| Collaboration controls Files | Includes the Files PCF control for accessing files on SharePoint. |
| Collaboration controls Core |Includes custom Collaboration APIs, the Collaboration Data Model and Virtual Tables for Events, Files and Task controls. |
| Collaboration controls Approvals | Includes the new Approvals PCF control. |
| Collaboration controls connector | Includes the new Collaboration Power Automate connector |

> [!NOTE]
> If you have an existing version of the controls installed in your environment, you might need to create a fresh environment and complete a new install to successfully upgrade to the latest version.

Before installation, you must be in a Power Platform environment or admin tenant. You'll need a dataverse environment with a database. If you don't have one, you'll need to [create a new one](/power-platform/admin/create-environment) to continue with the installation.

To install the solutions, begin by browsing to [Microsoft AppSource] and then complete the following steps:

1. Select **Get it now** button.
1. Sign in with your account, fill in the form and select **Continue**.

   :::image type="content" source="../assets/images/collaboration-control/preview-form.png" alt-text="Preview form "border="true":::

   :::image type="content" source="../assets/images/collaboration-control/overview.png" alt-text="overview collaboration control" border="true":::

   :::image type="content" source="../assets/images/collaboration-control/collaboration-controls-preview.png" alt-text="Collaboration control preview" border="true":::

1. You'll be directed to Power Platform Admin Center. Select an environment from the dropdown menu and agree to the terms and policy statements.

   > [!TIP]
   > If you see a permissions error when you select the environment, try selecting outside the environment dropdown menu to see if that resolves the issue.

   :::image type="content" source="../assets/images/collaboration-control/install-collaboration-control.png" alt-text="Install collaboration control" border="true":::

1. Select **Install**, installation might take approximately 15 minutes to complete.

   :::image type="content" source="../assets/images/collaboration-control/install-solution.png" alt-text="Collaboration control install" border="true":::

1. Go to [https://make.preview.powerapps.com/](https://make.preview.powerapps.com/environments/839eace6-59ab-4243-97ec-a5b8fcc104e4/home), it's also supported if you're signed up to Power Apps preview.

1. Ensure that you're in the environment the controls are installed into as you can view the environment and change it if necessary on the top right of the Power Apps portal.

   :::image type="content" source="../assets/images/collaboration-control/power-apps.png" alt-text="power apps" border="true":::

1. Select the **Solutions** tab to view all the solutions that you've installed in the right environment.

   :::image type="content" source="../assets/images/collaboration-control/solutions.png" alt-text="solutions collaboration control" border= "true":::

> [!NOTE]
> The Collaboration controls are preview and elements may change over time with potential for breaking changes. The Collaboration controls aren't supported in production environments.

After successful installation of all the Collaboration solutions into your environment, you'll be able to build a new model-driven app that can take advantage of the Collaboration control capabilities.
