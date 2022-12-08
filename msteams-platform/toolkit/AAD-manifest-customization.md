---
title: Edit Azure Active Directory manifest in Teams Toolkit
author: zyxiaoyuer
description:  Describes Managing Azure Active Directory application in Teams Toolkit
ms.author: surbhigupta
ms.localizationpriority: medium 
ms.topic: overview
ms.date: 05/20/2022
---

# Edit Azure AD manifest

The [Microsoft Azure Active Directory (Azure AD) manifest](/azure/active-directory/develop/reference-app-manifest) contain definitions of all the attributes of an Azure AD application object in the Microsoft identity platform.

Teams Toolkit now manages Azure AD application with the manifest file as the source of truth during your Teams application development lifecycle.

This section covers:

* [Customize Azure AD manifest template](#customize-azure-ad-manifest-template)
* [Azure AD manifest template placeholders](#azure-ad-manifest-template-placeholders)
* [Author and preview Azure AD manifest with code lens](#author-and-preview-azure-ad-manifest-with-code-lens)
* [Deploy Azure AD application changes for local environment](#deploy-azure-ad-application-changes-for-local-environment)
* [Deploy Azure AD application changes for remote environment](#deploy-azure-ad-application-changes-for-remote-environment)
* [View Azure AD application on the Azure portal](#view-azure-ad-application-on-the-azure-portal)
* [Use an existing Azure AD application](#use-an-existing-azure-ad-application)
* [Azure AD application in Teams application development lifecycle](#azure-ad-application-in-teams-application-development-lifecycle)

## Customize Azure AD manifest template

You can customize Azure AD manifest template to update Azure AD application.

1. Open `aad.template.json` in your project.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add template.png" alt-text="template":::

2. Update the template directly or [reference values from another file](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#Placeholders-in-AAD-manifest-template). You can see several customization scenarios here:
  
   * [Add an application permission](#add-an-application-permission)
   * [Preauthorize a client application](#preauthorize-a-client-application)
   * [Update redirect URL for authentication response](#update-redirect-url-for-authentication-response)

3. [Deploy Azure AD application changes for local environment](#deploy-azure-ad-application-changes-for-local-environment).
  
4. [Deploy Azure AD application changes for remote environment](#deploy-azure-ad-application-changes-for-remote-environment).

### Add an application permission

If the Teams application requires more permissions to call an API with additional permissions, you need to update `requiredResourceAccess` property in the Azure AD manifest template. You can see the following example for this property:

```JSON

   "requiredResourceAccess": [
    {
        "resourceAppId": "Microsoft Graph",
        "resourceAccess": [
            {
                "id": "User.Read", // For Microsoft Graph API, you can also use uuid for permission id
                "type": "Scope" // Scope is for delegated permission
            },
            {
                "id": "User.Export.All",
                "type": "Role" // Role is for application permission
            }
        ]
    },
    {
        "resourceAppId": "Office 365 SharePoint Online",
        "resourceAccess": [
            {
                "id": "AllSites.Read",
                "type": "Scope"
            }
        ]
    }
]
```

* `resourceAppId` property is used for different APIs. For `Microsoft Graph`, and `Office 365 SharePoint Online` enter the name directly instead of UUID, and for other APIs use UUID.

* `resourceAccess.id` property is used for different permissions. For `Microsoft Graph`, and `Office 365 SharePoint Online` enter the permission name directly instead of UUID, and for other APIs use UUID.

* `resourceAccess.type` property is used for delegated permission or application permission. `Scope` means delegated permission and `Role` means application permission.

### Preauthorize a client application

You can use `preAuthorizedApplications` property to authorize a client application to indicate that the API trusts the application. Users don't consent when the client calls it exposed API. You can see the following example for this property:

```JSON

    "preAuthorizedApplications": [
        {
            "appId": "1fec8e78-bce4-4aaf-ab1b-5451cc387264",
            "permissionIds": [
                "{{state.fx-resource-aad-app-for-teams.oauth2PermissionScopeId}}"
            ]
        }
        ...
    ]
```

`preAuthorizedApplications.appId` property is used for the application you want to authorize. If you don't know the application ID and know only the application name, use the following steps to search application ID:

1. Go to [Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) and open **Application Registrations**.

1. Select **All applications** and search for the application name.

1. Select the application name and get the application ID from the overview page.

### Update redirect URL for authentication response

  Redirect URLs are used while returning authentication responses such as tokens after successful authentication. You can customize redirect URLs using property `replyUrlsWithType`. For example, to add `https://www.examples.com/auth-end.html` as redirect URL, you can add it as the following example:

``` JSON
"replyUrlsWithType": [
    ...
    {
        "url": "https://www.examples.com/auth-end.html",
        "type": "Spa"
    }
]
```

## Azure AD manifest template placeholders

The Azure AD manifest file contains placeholder arguments with {{...}} statements it's replaced during build for different environments. You can build references to config file, state file, and environment variables with the placeholder arguments.

### Reference state file values in Azure AD manifest template

The state file is located in `.fx\states\state.xxx.json`. The following example shows typical state file:

> [!NOTE]
> xxx represents different environment.

``` JSON
{
    "solution": {
        "teamsAppTenantId": "uuid",
        ...
    },
    "fx-resource-aad-app-for-teams": {
        "applicationIdUris": "api://xxx.com/uuid",
        ...
    }
    ...
}
```

You can use this placeholder argument in the Azure AD manifest: `{{state.fx-resource-aad-app-for-teams.applicationIdUris}}` to point out `applicationIdUris` value in `fx-resource-aad-app-for-teams` property.

### Reference config file values in Azure AD manifest template

The config file is located in `.fx\configs\config.xxx.json`. The following example shows config file:

``` JSON
{
  "$schema": "https://aka.ms/teamsfx-env-config-schema",
  "description": "description.",
  "manifest": {
    "appName": {
      "short": "app",
      "full": "Full name for app"
    }
  }
}
```

You can use the placeholder argument in the Azure AD manifest: `{{config.manifest.appName.short}}` to refer `short` value.

### Reference environment variable in Azure AD manifest template

If you don't need to enter permanent values in Azure AD manifest template. For example, when the value is a secret. Azure AD manifest template file supports reference environment variables values. You can use the syntax `{{env.YOUR_ENV_VARIABLE_NAME}}` in the tool as parameter values to resolve the current environment variable values.

## Author and preview Azure AD manifest with CodeLens

Azure AD manifest template file has CodeLens to review and edit.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/preview view.png" alt-text="previewview":::

### Azure AD manifest template file

There's a preview CodeLens at the beginning of the Azure AD manifest template file. Select the CodeLens to generate an Azure AD manifest based as per your environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add codelens.png" alt-text="addcodelens":::

### Placeholder argument CodeLens

Placeholder argument CodeLens helps you to see the values for local debug and develop your environment. If you hover the mouse on the placeholder argument, it shows tooltip box for the values of all the environments.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add arguments.png" alt-text="addarguments":::

### Required resource access CodeLens

It's different from official [Azure AD manifest schema](/azure/active-directory/develop/reference-app-manifest) that `resourceAppId` and `resourceAccess` ID in `requiredResourceAccess` property only supports UUID. Azure AD manifest template in Teams Toolkit also supports user readable strings for `Microsoft Graph` and `Office 365 SharePoint Online` permissions. If you enter UUID, code lens shows user readable strings, otherwise, it shows UUID.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add resource.png" alt-text="addresource":::

### Pre-authorized applications CodeLens

CodeLens shows the application name for the pre-authorized application ID for the `preAuthorizedApplications` property.

## Deploy Azure AD application changes for local environment

1. Select `Preview` CodeLens in `aad.template.json`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy1.png" alt-text="deploy1":::

2. Select **local** environment.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy2.png" alt-text="deploy2":::

3. Select `Deploy Azure AD Manifest` CodeLens in `aad.local.json`.

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy3.png" alt-text="deploy3":::

4. The changes for Azure AD application used in local environment are deployed.
  
## Deploy Azure AD application changes for remote environment

1. Open the command palette and select: `Teams: Deploy Azure Active Directory application manifest`.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy4.png" alt-text="deploy4":::

2. Additionally you can right click on the `aad.template.json` and select `Deploy Azure Active Directory application manifest` from the context menu.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy5.png" alt-text="deploy5":::

## View Azure AD application on the Azure portal

1. Copy the Azure AD application client ID from `state.xxx.json` () file in the `fx-resource-aad-app-for-teams` property.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view1.png" alt-text="view1":::

   > [!NOTE]
   > xxx in the client ID indicates the environment name where you have deployed the Azure AD application

2. Go to [Azure portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) and sign in to Microsoft 365 account.
  
   > [!NOTE]
   > Ensure that login credentials of Teams application and M365 account are the same.

3. Open [App Registrations page](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), search the Azure AD application using client ID that you copied before.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view2.png" alt-text="view2":::

4. Select Azure AD application from search result to view the detail information.
  
5. In Azure AD app information page, select the `Manifest` menu to view manifest of this application. The schema of the manifest is same as the one in `aad.template.json` file. For more information about manifest, see [Azure Active Directory application manifest](/azure/active-directory/develop/reference-app-manifest).
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view3.png" alt-text="view3":::

6. You can select **Other Menu** to view or configure Azure AD application through its portal.
  
## Use an existing Azure AD application

You can use the existing Azure AD application for the Teams project. For more information, see [use an existing Azure AD application for your Teams application](https://github.com/OfficeDev/TeamsFx/wiki/Customize-provision-behaviors#use-an-existing-aad-app-for-your-teams-app).

## Azure AD application in Teams application development lifecycle

You need to interact with Azure AD application during various stages of your Teams application development lifecycle.

1. **To create Project**

      You can create a project with Teams Toolkit that comes with single-sign-on (SSO) support by default such as `SSO-enabled tab`. For more information on how to create a new app, see [create new Teams application using Teams Toolkit](create-new-project.md). An Azure AD manifest file is automatically created for you in `templates\appPackage\aad.template.json`. Teams Toolkit creates or updates the Azure AD application during local development or while you move the application to the cloud.

2. **To add SSO to your Bot or Tab**

      After you create a Teams application without built-in SSO, Teams Toolkit progressively helps you to add SSO for the project. As a result, an Azure AD manifest file is automatically created for you in `templates\appPackage\aad.template.json`.

      Teams Toolkit creates or updates the Azure AD application during next local debug session or while you move the application to the cloud.

3. **To build Locally**

    Teams Toolkit performs the following functions during local debug:

    * Read the `state.local.json` file to find an existing Azure AD application. If an Azure AD application already exists, Teams Toolkit reuses the existing Azure AD application. Otherwise you need to create a new application using the `aad.template.json` file.

    * Initially ignores some properties in the manifest file that requires more context, such as `replyUrls` property that requires a local debug endpoint during the creation of a new Azure AD application with the manifest file.

    * After the local dev environment starts successfully, the Azure AD application's `identifierUris`, `replyUrls`, and other properties that aren't available during creation stage are updated accordingly.

    * The changes you've done to your Azure AD application are loaded during next local debug session. You can see [Azure AD application changes](https://github.com/OfficeDev/TeamsFx/wiki/) applying manually.

4. **To provision for cloud resources**

      You need to provision cloud resources and deploy your application while moving your application to the cloud. At the stages, like local debug, Teams Toolkit will:

      * Read the `state.{env}.json` file to find an existing Azure AD application. If an Azure AD application already exists, Teams Toolkit re-uses the existing Azure AD application. Otherwise you need to create a new application using the `aad.template.json` file.

      * Initially ignore some properties in the manifest file that requires more context such as `replyUrls` property requires frontend or bot endpoint during the creation of a new Azure AD application with the manifest file.

      * After other resources provision completes, the Azure AD application's `identifierUris`, and replyUrls are updated according to the correct endpoints.

5. **To build application**

    * Deploy to the cloud command deploys your application to the provisioned resources. It doesn't include deploying Azure AD application changes you made.

    * For more information on how to deploy Azure AD application changes for remote environment, see [Deploy Azure AD application changes for remote environment](#deploy-azure-ad-application-changes-for-remote-environment).

    * Teams Toolkit updates the Azure AD application according to the Azure AD manifest template file.

## Limitations

1. Teams Toolkit extension doesn't supports all the properties listed in Azure AD manifest schema.
  
      The following table lists the properties that aren't supported in Teams Toolkit extension:

      |**Not supported properties**|**Reason**|
      |-----------|----------|
      |`passwordCredentials`|Not allowed in manifest|
      |`createdDateTime`|Read-only and can't change|
      |`logoUrl`|Read-only and can't change|
      |`publisherDomain`|Read-only and can't change|
      |`oauth2RequirePostResponse`|Doesn't exist in Graph API|
      |`oauth2AllowUrlPathMatching`|Doesn't exist in Graph API|
      |`samlMetadataUrl`|Doesn't exist in Graph API|
      |`orgRestrictions`|Doesn't exist in Graph API|
      |`certification`|Doesn't exist in Graph API|

2. Currently `requiredResourceAccess` property is used for user readable resource application name or permission name strings only for `Microsoft Graph` and `Office 365 SharePoint Online` APIs. For other APIs, you need to use UUID instead. Perform the following steps to retrieve IDs from Azure portal:

    * Register a new Azure AD application on [Azure portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
    * Select `API permissions` from the Azure AD application page.
    * Select `add a permission` to add the permission you need.
    * Select `Manifest`, from the `requiredResourceAccess` property, where you can find the IDs of API, and the permissions.

## See also

* [Preview and Customize app manifest in Toolkit](TeamsFx-preview-and-customize-app-manifest.md)
