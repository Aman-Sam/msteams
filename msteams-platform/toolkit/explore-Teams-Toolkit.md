---
title: Explore Teams Toolkit 
author: zyxiaoyuer
description: Learn about Teams Toolkit UI elements and task pane for Visual Studio Code and Visual Studio.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
---
# Explore Teams Toolkit

::: zone pivot="visual-studio-code"

> [!IMPORTANT]
>
> * We've introduced the Teams Toolkit v5 extension within Microsoft Visual Studio Code. This version comes to you with many new app development features. We recommend that you use Teams Toolkit v5 for building your Teams app.
> * [Teams Toolkit v4](toolkit-v4/teams-toolkit-fundamentals-v4.md) extension will soon be deprecated.

::: zone-end

::: zone pivot="visual-studio"

> [!IMPORTANT]
>We've introduced the important changes in Teams Toolkit extension within Microsoft Visual Studio v17.7 with many new app development features. We recommend that you use Teams Toolkit v17.7 for building your Teams app.

::: zone-end

In this article, learn how to explore Teams Toolkit and its features in Visual Studio.

::: zone pivot="visual-studio-code"

## Take a tour of Teams Toolkit

Teams Toolkit appears within Visual Studio Code as an extension. After you install Teams Toolkit, it opens within the Visual Studio Code window.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/overview-vsc.png" alt-text="Screenshot shows the Overview of Teams Toolkit." lightbox="../assets/images/teams-toolkit-v2/teams-toolkit-v5/overview-vsc.png":::

| Serial No. | UI Elements | Definition |
| --- | --- | --- |
| 1 | **Documentation** | Access the Microsoft Teams Developer documentation. |
| 2 | **How-to Guides** | Access the how-to guides for app scenario and app development. |
| 3 | **Create a New App** | Create a new Teams app based on your requirement. |
| 4 | **View Samples** | Select and build existing app samples based on common use cases for a Teams app. |
| 5 | • **New File** <br> • **Open File** <br> • **Open Folder** <br> • **Clone Git Repository** | • Create a new file. <br> • Open an existing file. <br> • Open an existing folder. <br> • Clone a Git repository of your app project. |
| 6 | **Recent** | View the recent files. |
| 7 | **Get Started** | Explore Teams Toolkit and get an overview of the fundamentals. |

### Explore the Teams Toolkit task pane

You can explore the available functionalities from the Teams Toolkit task pane. The task pane appears only after you've created an app project using Teams Toolkit. The following video helps you to learn about the process of creating a new Teams app:

   :::image type="content" source="../assets/videos/bot-app.gif" alt-text="Graphical representation shows the steps to create a Teams app.":::

After you create a new Teams app project, the directory structure of the app appears in the left pane and the **`README`** file in the right pane.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/app-preview-page.png" alt-text="Screenshot shows the  app preview readme page of Teams Toolkit." lightbox="../assets/images/teams-toolkit-v2/teams-toolkit-v5/app-preview-page.png":::

Let's take a tour of Teams Toolkit.

 In Visual Studio Code activity bar, the following icons are relevant to Teams Toolkit:

| Select | To... |
| --- | --- |
| **Explorer** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | View the directory structure of the app. |
| **Run and Debug** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | Start the local or remote debug process. |
| **Teams Toolkit** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | View the task pane  in the Teams Toolkit. |

From the task pane, you can see the following sections:

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/accounts.png" alt-text="Screenshot shows the Accounts section.":::
   :::column-end:::
   :::column span="":::

        To develop a Teams app, you need the following accounts:
        
        * **Sign in to Microsoft 365**: Use your Microsoft 365 work or school account with a valid E5 subscription for building your app. If you don't have a valid account, you can join [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program) to get a free account before you start.

        * **Sign in to Azure**: Use your Azure account for deploying your app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/environment.png" alt-text="Screenshot shows the Environment section.":::
   :::column-end:::
   :::column span="":::

        To deploy your Teams app, you need the following environments:
        
       * **local**: Deploy your app in the default local environment with local environment configurations.

       * **dev**: Deploy your app in the default dev environment with remote or cloud environment configurations.

        You can create more environments, such as production or test, as you need.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/development.png" alt-text="Screenshot shows the Development section.":::
   :::column-end:::
   :::column span="":::

        To create and debug your Teams app, you need the following features:
        
       * **Create a New App**: Use the Teams Toolkit wizard to prepare project scaffolding for app development.

        * **View Samples**: Select any of the Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub and you can build the sample app.

        * **View How-to Guides**: Select to view Teams app scenario guides and development guides.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/deployment.png" alt-text="Screenshot shows the Lifecycle section.":::
   :::column-end:::
   :::column span="":::

        To provision, deploy, and publish your Teams app, you need the following features:
        
        * **Provision**: Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager, and it registers your app with Azure AD automatically.
        
        * **Deploy**: Deploy the source code to Azure.
       
        * **Publish**: Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/utility.png" alt-text="Screenshot shows the Utility section.":::
   :::column-end:::
   :::column span="":::

        To create an app package, validate an app, and publish in Developer Portal, you need the following features:

        * **Zip Teams App Package**: Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons.
        
        * **Validate Application**: Validate if Teams manifest file is in right schema or validate the Teams app package.
        
        * **Open Developer Portal to Publish**: Use Developer Portal to publish and manage your Teams app. 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/help-and-feedback.png" alt-text="Screenshot shows the Help section.":::
   :::column-end:::
   :::column span="":::

        To access more information on Teams Toolkit, you need the following documentation and resources:
        
        * **Documentation**: Select to access the Microsoft Teams Developer documentation.

        * **Get Started**: View Teams Toolkit Get started help within Visual Studio Code.

        * **Report Issues on GitHub**: Select to access GitHub page and raise any issues.
   :::column-end:::
:::row-end:::

<!--  
:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/feedback.png" alt-text="Screenshot shows the Feedback section.":::
   :::column-end:::
   :::column span="":::

        You can help us improve by giving us your feedbacks!
   :::column-end:::
:::row-end:::
-->

### To view how-to guides

1. Select **View How-to Guides** from the Teams Toolkit task pane under **DEVELOPMENT** section.

   The **View How-to Guides** menu appears.

2. Select the type of how-to guide that you want to view.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/view-how-to-guides.png" alt-text="Screenshot shows the how-to guides menu options." lightbox="../assets/images/teams-toolkit-v2/teams-toolkit-v5/view-how-to-guides.png":::

    * Select any one of the Teams app scenario guides to view the guide to develop an app for a common app scenario, such as sending notifications using a bot.
    * Select any one of the Teams app development guides to view a guide that helps in app development, such as embedding a dashboard tab in a Teams app.

::: zone-end

::: zone pivot="visual-studio"

## Explore Teams Toolkit for Visual Studio

Teams Toolkit appears as a workload in the app you've created in Visual Studio. For more information, see [How to create a Teams app](create-new-project.md). 

You can view Teams Toolkit in Visual studio in the following ways:

* Project
* Solution Explorer

# [Project](#tab/prj)

To view the Teams Toolkit from the **Project** menu, follow these steps:

1. Select **Project**.
1. Select **Teams Toolkit**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/teams-toolkit-installed.png" alt-text="Screenshot shows the Teams toolkit project menu.":::

# [Solution Explorer](#tab/solutionexplorer)

   To view Teams Toolkit under **Solution Explorer**, follow these steps:

1. Select **View** > **Solution Explorer** to view **Solution Explorer** panel.
1. Right-click on your app project name.
1. Select **Teams Toolkit**.

   > [!NOTE]
   > In this scenario the project name is **MyTeamsApp**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/ttk-solution explorer.png" alt-text="Screenshots the Teams toolkit operations from Project":::
  

---

After you've created your Teams app project, you can use the following options to develop and build your app:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-v5/ttk-solution explorer-options.png" alt-text="Teams toolkit operations from Project menu":::

|Function  |Description  |
|---------|---------|
|Prepare Teams App Dependencies     |Before you debug locally, ensure that you prepare your app for dependencies. This option helps you to set up the local debug dependencies and register Teams app in the Teams platform. You must have a Microsoft 365 account. For more information, see [how to debug your Teams app locally using Visual Studio](debug-local.md).         |
|Open Manifest File     | Helps you to open Teams app manifest file. Hover over the parameters to preview the values. For more information, see [how to edit Teams app manifest using Visual Studio](TeamsFx-preview-and-customize-app-manifest.md).         |
|Update Manifest in Teams Developer Portal     | Helps you to update the manifest file. When you update the manifest file, only then you can redeploy the manifest file to Azure without deploying the whole project again. Use this command to update your changes to remote. For more information, see [how to edit Teams app manifest using Visual Studio](TeamsFx-preview-and-customize-app-manifest.md).       |
|Add Authentication Code     | Helps you obtain signed-in Teams user token to access Microsoft Graph and other APIs. Teams Toolkit facilitates the interaction by abstracting from the Microsoft Azure Active Directory (Azure AD), which flows and integrates with simple APIs. For more information, see [how to add single sign-on to Teams app](add-single-sign-on.md).        |
|Provision in the Cloud     | Helps you to create Azure resources that host your Teams app. For more information, see [how to provision cloud resources using Visual Studio](provision.md).        |
|Deploy to the Cloud     | Helps you to copy your code to the cloud resources that you provisioned in Azure AD. For more information, see [how to deploy Teams app to the cloud using Visual Studio](deploy.md).        |
|Preview in Teams     | Launches the Teams web client and lets you preview the Teams app in your browser.         |
|Zip App Package     | Generates a Teams app package in the **Build** folder under the project. You can upload the app package to the Teams client and run the Teams app.         |

::: zone-end

## See also

* [Teams Toolkit Overview](teams-toolkit-fundamentals.md)
* [Create a new Teams app using Teams Toolkit](create-new-project.md)
* [App manifest schema](~/resources/schema/manifest-schema.md)
* [Prepare to build apps using Teams Toolkit](build-environments.md)

<!--  
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ui-elements.png" alt-text="Screenshot shows the UI Elements.":::

|Section|Features|Details
|---------|---------|--------|
| **1. ACCOUNTS** | &nbsp; | &nbsp; |
| &nbsp; |Microsoft 365 account|  Use your Microsoft 365 account with a valid E5 subscription for building your app.|
| &nbsp; | Azure Account |  Use your Azure account for deploying app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.|
|**2.ENVIRONMENT** |  &nbsp; | &nbsp;|
| &nbsp; |Local |Deploy your app in the default local environment with local machine environment configurations.|
| &nbsp; | Dev |Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need.|
| **3.DEVELOPMENT** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Teams Toolkit helps you to create and customize your Teams app project that makes the Teams app development work simpler. Create a new Teams app helps you to start with Teams app development by creating new Teams project using Teams Toolkit either by using **Create new project**|
| &nbsp; | View Samples | Select any of Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app.|
| &nbsp; | Add Features | It helps you to add additional Teams capabilities such as **Tab** or **Bot** or **Message extension** or **Command bot** or **Notification bot**, or **SSO enabled tab** optionally add Azure resources such as **Azure SQL Database** or **Azure Key Vault**, or **Azure function** or **Azure API Management** which fits your development needs to your current Teams app. You can also add **API connection** or **Single Sign-on** or **CI/CD workflows** for your Teams app.
| &nbsp; | Edit Manifest file | It helps you customize manifest file based on the app requirements |
| **4.DEPLOYMENT** | &nbsp; | &nbsp; |
| &nbsp;| Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager.|
| &nbsp; | Zip Teams metadata package| Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons. |
| &nbsp; | Deploy to the cloud| Deploy the source code to Azure.|
| &nbsp; | Publish to Teams| Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.|
| &nbsp; | Developer Portal for Teams| It is the primary tool for configuring, distributing, and managing your Microsoft Teams apps. You can collaborate with colleagues on your app, set up runtime environments, and much more. |
| **5.HELP AND FEEDBACK** | &nbsp; | &nbsp; |
| &nbsp; | Get Started |  View the Teams Toolkit Get started help within Visual Studio Code.|
| &nbsp; | Tutorials| Select to access different tutorials.|
| &nbsp; | Documentation| Select to access the Microsoft Teams Developer Documentation.|
| &nbsp; | Report issues on GitHub| It helps to get **Quick support** from product expert. Browse the existing issues before you create a new one, or visit [StackOverflow tag `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) to submit feedback.|
| **6.Explorer** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | It helps to view the directory structure of your app.|
| **7.Run and Debug** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | To start the local or remote debug process.|
-->
