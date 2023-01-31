---
title: Explore Teams Toolkit 
author: zyxiaoyuer
description: Learn about Teams Toolkit UI elements and task pane for Visual Studio Code, and different functions for Visual Studio.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
---
# Explore Teams Toolkit

Teams Toolkit appears within Visual Studio Code as an extension. You can explore the Teams Toolkit look and feel within the Visual Studio Code. This section gives you a tour of Teams Toolkit and its features.

::: zone pivot="visual-studio-code"

## Take a tour of Teams Toolkit

After you install Teams Toolkit, it opens within the Visual Studio Code window.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1_1.png" alt-text="Overview of Teams Toolkit" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1_1.png":::

| Serial No. | UI Elements | Definition |
| --- | --- | --- |
| 1 | **Get Started** | Explore Teams Toolkit and get an overview of the fundamentals. |
| 2 | **Create a new Teams app** | Create a new Teams app based on your requirement. |
| 3 | **View samples** | Select and build existing app samples based on common use cases for a Teams app. |
| 4 | **Documentation** | Access the Microsoft Teams Developer documentation. |
| 5 | **Tutorials** | Access different tutorials. |
| 6 | • **New File** <br> • **Open File** <br>  • **Open Folder** <br>  • **Clone Git Repository**  |  • Create a new file. <br>  • Open an existing file. <br> • Open the existing folder. <br> • Clone the Git repository of your app project. |
| 7 | **Recent** | View the recent files. |

### Explore the Teams Toolkit task pane

The Teams Toolkit task pane appears only after you have created an app project using Teams Toolkit. Use the task pane to explore Teams Toolkit functionalities.

The following video gives you a brief overview of creating a Teams app project using Teams Toolkit:

   :::image type="content" source="../assets/videos/javascript-bot-app1_1.gif" alt-text="Create a Teams app":::

After you've created a new Teams app project, the Teams Toolkit task pane appears. It shows the directory structure of the app. In the right panel, the **`README`** file appears.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page_1.png" alt-text="First page of Teams Toolkit" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page_1.png":::

Let's take a tour of the Teams Toolkit.

 In Visual Studio Code activity bar, the following icons are relevant to the Teams Toolkit:

| Icon | Description |
| --- | --- |
| **Explorer** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | To view the directory structure of the app. |
| **Run and Debug** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | To start the local or remote debug process. |
| **Teams Toolkit** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | To view the task pane  in the Teams Toolkit. |

From the task pane, you can see the following sections:

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/accounts1_1.png" alt-text="accounts section":::
   :::column-end:::
   :::column span="":::

        To develop a Teams app, you need the following accounts:
        
        * **Sign in to Microsoft 365**: Use your [Microsoft 365 account](https://developer.microsoft.com/microsoft-365/dev-program) with a valid E5 subscription for building your app.

        * **Sign in to Azure**: Use your Azure account for deploying your app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/environment1.png" alt-text="Environment section":::
   :::column-end:::
   :::column span="":::

        To deploy your Teams app, you need the following environments:
        
        * **local**: Deploy your app in the default local environment with local environment configurations.

        * **dev**: Deploy your app in the default dev environment with remote or cloud environment configurations.

        You can create more environments, such as, production or test,  as you need.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/development_1.png" alt-text="Development section":::
   :::column-end:::
   :::column span="":::

        To create, customize, and debug your Teams app, you need the following features:
        
       * **Create a new app**: Use the Teams Toolkit wizard to prepare project scaffolding for app development.

        * **View samples**: Select any of the Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub and you can build the sample app.

        * **View how-to guides**: Select to view Teams app scenario guides and development guides. 
        
        * **Add features**: Add other Teams capabilities to the Teams app during the development process and add optional cloud resources suitable for your app.
       
        * **Preview your Teams app (F5)**: Press **F5** to debug and preview your Teams app.

        * **Edit manifest file**: Edit the Teams app manifest file with the Teams client.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deployment1.png" alt-text="Deployment section":::
   :::column-end:::
   :::column span="":::

        To provision, deploy, and publish your Teams app, you need the following features:
        
        * **Provision in the cloud**: Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager, and it registers your app with Azure AD automatically.

        * **Zip Teams metadata package**: Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons.
        
        * **Deploy to the cloud**: Deploy the source code to Azure.
       
        * **Publish to Teams**: Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.
        
        * **Developer Portal for Teams**: Use Developer Portal to configure and manage your Teams app. 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/help-and-feedback1.png" alt-text="Help and feedback section":::
   :::column-end:::
   :::column span="":::

        To access more information on Teams Toolkit, you need the following documentation and resources:
        
        * **Documentation**: Select to access the Microsoft Teams Developer documentation.

        * **Get started**: View Teams Toolkit Get started help within Visual Studio Code.
       
        * **Report issues on GitHub**: Select to access GitHub page and raise any issues.
   :::column-end:::
:::row-end:::

::: zone-end

::: zone pivot="visual-studio"

## Explore Teams Toolkit for Visual Studio

After Teams Toolkit installation, you can see Teams Toolkit options in the following ways:

# [Project](#tab/prj)

You can access Teams Toolkit under **Project**.

1. Select **Project** > **Teams Toolkit**.
    You can access different Teams Toolkit options.

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu_1_2.png" alt-text="Teams toolkit operations menu":::

# [Solution Explorer](#tab/solutionexplorer)

   You can access Teams Toolkit under **Solution Explorer**.

1. Select **View** > **Solution Explorer** to view **Solution Explorer** panel.
1. Right-click on your app project name.
1. Select **Teams Toolkit** to see the menu items.

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1_1_2.png" alt-text="Teams toolkit operations from Project":::

   > [!NOTE]
   > In this scenario the project name is **MyTeamsApp**.

---

After you've created your Teams app project, you can use the following options to develop and build your app in Teams Toolkit for Visual Studio:

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-menu-options_2.png"alt-text="Teams toolkit operations from Project menu":::

| Function | Description |
|---|---|
| Prepare Teams App Dependencies. | Before you debug locally, ensure that you prepare your app for dependencies. It helps to set up the local debug dependencies and register Teams app in the Teams platform. You need a Microsoft 365 account. For more information, see [how to debug your Teams app locally using Visual Studio](debug-local.md). |
| Open Manifest File. | To open Teams app manifest file, hover over the parameters to preview the values. For more information, see [how to edit Teams app manifest using Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md). |
| Update Manifest in Teams Developer Portal. | When you update the manifest file, only then you can redeploy the manifest file to Azure without deploying the whole project again. Use this command to update your changes to remote. For more information, see [how to edit Teams app manifest using Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md). |
| Add Authentication Code. | This option helps you to obtain signed-in Teams user token to access Microsoft Graph and other APIs. Teams Toolkit facilitates the interaction by abstracting from the Microsoft Azure Active Directory (Azure AD) which flows and integrations with simple APIs. For more information, see [how to add single sign-on to Teams app](add-single-sign-on.md). |
| Provision to the Cloud. | This option helps you to create Azure resources that host your Teams app. For more information, see [how to provision cloud resources using Visual Studio](provision-cloud-resources.md). |
| Deploy to the Cloud. |This option helps you to copy your code to the cloud resources that you provisioned in Azure AD. For more information, see [how to deploy Teams app to the cloud using Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio). |
| Preview in Teams. | This option launches the Teams web client and lets you preview the Teams app in your browser. |
| Zip App Package. | This option generates a Teams app package in the `Build` folder under the project. You can upload the package to the Teams client and run the Teams app. |

::: zone-end

## See also

* [Teams Toolkit Overview](teams-toolkit-fundamentals.md)
* [Create a new Teams app using Teams Toolkit](create-new-project.md)
* [App manifest schema](../resources/schema/manifest-schema.md)
* [Prepare to build apps using Teams Toolkit](build-environments.md)

<!--  
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ui-elements.png" alt-text="UI Elements":::

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
