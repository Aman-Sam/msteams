---
title: Create new project
author: Rajeshwari-v
description:  Describes about creating project
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: Create new project
---

# Create a new app

To build any app in Teams, you can use Teams toolkit either by creating a new project or by creating from samples.

(pictures used in this part is already in doc repo)

**To create new project**

1. Open Visual Studio code.
1. Open Teams Toolkit and select **Teams**:

![Teams Toolkit](~/assets/images/tools-and-sdks/teams-toolkit.png)

1. Select **Create a new Teams app**.

![Create project](~/assets/images/tools-and-sdks/create-project.png)

1. Select Create a new Teams app.

![Create new Teams app](~/assets/images/tools-and-sdks/create-new-project-intro.png)

1. Select the required app capability, such as tabs, bots, and messaging extensions. You can also select multiple capabilities. Fore more information on different capabilities, see [app-capabilities-support-matrix]

![Create capabilities](~/assets/images/tools-and-sdks/create-project-capabilities.png)

1. Select **Azure** or **SharePoint Framework(SPFx)** as per the requirement.

![Create frontend hosting type](~/assets/images/tools-and-sdks/create-project-hosting.png)

1. Select the cloud resource from the dropdown or select **OK** if you don't want to add any cloud resources. You can also also add cloud resources later.

![Create cloud resources](~/assets/images/tools-and-sdks/create-project-cloud-resources.png)

1. Select **JavaScript** or **TypeScript** for programming language

![Create programming language](~/assets/images/tools-and-sdks/create-project-programming-languages.png)

1. Select frontend framework for SharePoint Framework (SPFx) only.

![Create framework](~/assets/images/tools-and-sdks/spfx-which-framework.png)

1. Enter Webpart name and Webpart description of your choice.

1. Select workspace folder for the built project.
1. Enter name for your app, such as helloworld. You can only use alphanumeric characters.
1. Press **Enter** to continue.

You have created a new app.

## Create from samples

You can create an app with the help of samples for reference:

1. Open the the Teams Toolkit for Visual Studio Code.
1. Go to the **DEVELOPMENT** section in Tree View.
1. Select **View samples**. 

![View samples](~/assets/images/tools-and-sdks/view-sampels.png)

Explore and download samples from **Samples**.

![View samples screen](~/assets/images/tools-and-sdks/view-sampels_screen.png)

The following steps provide alternate way to open sample app:

1. Go to **DEVELOPMENT**.
1. Select **Create new project**.
1. Select **Start from samples**.
1. Select required sample from the list.

You can run each samples in preview mode for Teams web client. After, you download a sample app, you can see the instruction file with VS Code.

## See also

[Provision in the cloud](provision-in-the-cloud.md)
[[Add cloud resources](add-cloud-resources.md)
[Deploy to the cloud](deploy-to-the-cloud.md)