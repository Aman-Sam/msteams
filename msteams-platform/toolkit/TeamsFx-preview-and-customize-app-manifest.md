---
title: Customize Teams App Manifest in Teams Toolkit
author: surbhigupta
description: In this module, learn how to edit, preview and customize Teams App Manifest in different environment.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
---

# Customize Teams app manifest

The Teams app manifest describes how your app integrates into the Microsoft Teams product.

::: zone pivot="visual-studio-code"

## Customize Teams app manifest for Visual Studio Code

The Teams app manifest describes how your app integrates into the Microsoft Teams product. For more information on Manifest, see [App manifest schema for Teams](../resources/schema/manifest-schema.md). This section covers:

* [Preview manifest file in local environment](#preview-manifest-file-in-local-environment)
* [Preview manifest file in remote environment](#preview-manifest-file-in-remote-environment)
* [Sync local changes to Developer Portal](#sync-local-changes-to-developer-portal)
* [Customize your Teams app manifest](#customize-your-teams-app-manifest)
* [Validate manifest](#validate-manifest)

The manifest template file `manifest.template.json` is available under `templates/appPackage` folder after scaffolding. The template file with placeholders, and the actual values are resolved by Teams Toolkit using files under `.fx/configs` and `.fx/states` for different environments.

To preview manifest with actual content, Teams Toolkit generates preview manifest files under `build/appPackage` folder:

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

You can preview manifest file in local and remote environments.

* [Preview manifest file in local environment](#preview-manifest-file-in-local-environment)
* [Preview manifest file in remote environment](#preview-manifest-file-in-remote-environment)

## Preview manifest file in local environment

To preview manifest file in local environment, you can press **F5** to run local debug. It generates default local settings for you, then the app package and preview manifest builds under `build/appPackage` folder.

You can also preview local manifest file by two methods

* By using preview option in codelens
* By using **Zip Teams metadata package** option

The following steps help to preview local manifest file by using preview option in codelens:

1. Select **Preview** in the codelens of `manifest.template.json` file.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Screenshot is an example showing the preview in the codelens of manifest file." lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png":::

1. Select **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Screenshot is an example of showing the selection of local in the environment.":::

The following steps help to preview local manifest file by using **Zip Teams metadata package** option:

1. Select `manifest.template.json` file.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Screenshot is an example of showing the selection of manifest.template.json.":::

1. Select the Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: icon in the Visual Studio Code toolbar.

1. Select **Zip Teams metadata package** under **DEPLOYMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Screenshot is an example of showing the selection of zip Teams metadata package.":::

1. Select **local**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="Screenshot is an example of showing the selection of local in the environment.":::

Following image is a preview local:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Screenshot is an example of showing the preview of local." lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png":::

## Preview manifest file in remote environment

To preview manifest file using Visual Studio Code:

* Select **Provision in the cloud** under **DEVELOPMENT** in Teams Toolkit extension
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="Screenshot is an example of showing the selection of provision in the cloud resource.":::

To preview manifest file using command palette. You can trigger **Teams: Provision in the cloud** from command palette.

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="Screenshot is an example of showing provision cloud resource using command palette." lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png":::

It generates configuration for remote Teams app, and builds package and preview manifest under `build/appPackage` folder.

You can also preview manifest file by two methods in remote environment

* By using preview option in codelens
* By using **Zip Teams metadata package** option

The following steps help to preview manifest file by using preview option in codelens:

1. Select **Preview** in the codelens of `manifest.template.json` file.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="Screenshot is an example of showing preview in the codelens of manifest file.":::

1. Select your environment.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Screenshot is an example of showing the adding of environment.":::

   > [!NOTE]
   > If there are more than one environment, you need to select the environment you want to preview.

The following steps help to preview manifest file by using **Zip Teams metadata package** option in remote environment:

1. Select `manifest.template.json` file.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="Screenshot is an example of showing the selection of manifest.template.json.":::

1. Select the **Teams Toolkit** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: icon in the Visual Studio Code Activity Bar.

1. Select **Zip Teams metadata package** under **DEPLOYMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="Screenshot is an example of showing the selection of zip Teams metadata package.":::

1. Select your environment.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="Screenshot is an example of showing the adding of environment.":::

   > [!NOTE]
   > If there are more than one environment, you need to select the environment you want to preview.

## Sync local changes to Developer Portal

After previewing the manifest file, you can sync your local changes to Developer Portal by the following ways:

> [!NOTE]
> For more information on Developer Portal, see [Developer Portal for Teams](../concepts/build-and-test/teams-developer-portal.md).

1. Deploy Teams app manifest.

   You can deploy Teams app manifest in any of the following ways:

   * Right-click `manifest.template.json` file, and select **Deploy Teams app manifest** from context menu.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="Screenshot is an example of showing the selection of deploy Teams app manifest.":::

   * Trigger **Teams: Deploy Teams app manifest** from command palette.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="Screenshot is an example of showing the deploy from command palette.":::

2. Update to Teams platform.

   You can update to Teams platform in any of the following ways:

   * Select **Update to Teams platform** on the upper left-corner of `manifest.{env}.json`.

   * Trigger **Teams: Update manifest to Teams platform** on the menu bar of `manifest.{env}.json`.

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="Screenshot is an example of showing the update to Teams platform on the menu bar of manifest." lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png":::

You can also trigger **Teams: Update manifest to Teams platform** from the command palette:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="Screenshot is an example of showing the selection of Teams: update manifest to Teams platform from the command palette.":::

> [!NOTE]
> Trigger from editor codelens or menu bar updates current manifest file to Teams platform. Trigger from command palette requires selecting target environment.

 CLI command:

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> The change updates to Dev Portal. Any manual updates in Dev Portal are overwritten.

If the manifest file is outdated due to configuration file change or template change, select any one of the following actions:

* **Preview only**: Local manifest file is overwritten according to current configuration.
* **Preview and update**: Local manifest file is overwritten according to current configuration and also updated to Teams platform.
* **Cancel**: No action is taken.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="Screenshot is an example of showing,the navigation to select preview only, preview and update and cancel options when the manifest file is outdated due to configuration or template change.":::

## Customize your Teams app manifest

Teams Toolkit consists of the following manifest template files under `manifest.template.json` folder across local and remote environments:

* `manifest.template.json`
* `templates/appPackage`

During the local debug or provision, Teams Toolkit loads manifest from `manifest.template.json`, with the configurations from `state.{env}.json`, `config.{env}.json`, and creates Teams app in [Dev Portal](https://dev.teams.microsoft.com/apps).

### Supported placeholders in manifest.template.json

The following list provides supported placeholders in `manifest.template.json`:

* `{{state.xx}}` is pre-defined placeholder and it's value is resolved by Teams Toolkit, defined in `state.{env}.json`. Ensure not to modify the values in `state.{env}.json`
* `{{config.manifest.xx}}` is a customized placeholder and it's value is resolved from `config.{env}.json`

**To add customized parameter**

1. Add customized parameter as follows:</br>
   a. Add a placeholder in `manifest.template.json` with pattern `{{config.manifest.xx}}`.</br>
   b. Add a config value in `config.{env}.json`.

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. You can go to configuration file by selecting any one of the config placeholders **Go to config file** or **View the state file** in `manifest.template.json`.

### Validate manifest

During operations such as, **Zip Teams metadata package**, Teams Toolkit validates the manifest against its schema. The following list provides different ways to validate manifest:

* In VSC, trigger `Teams: Validate manifest file` from command palette:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="Screenshot is an example of showing Teams validate manifest file from command palette.":::

* In CLI, use command:

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can go to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Screenshot is an example of showing preview values for local and dev environment.":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can go to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Screenshot is an example of showing the selection of an environment.":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Screenshot is an example of showing the preview values for all environments.":::

::: zone-end

::: zone pivot="visual-studio"

## Customize Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Screenshot is an example of showing the navigation to open manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

### Customize app manifest in Teams Toolkit

There are two types of placeholders in `manifest.template.json`:

* `{{state.xx}}` is pre-defined placeholder, whose value is resolved by Teams Toolkit, defined in `state.{env}.json`. It's recommended not to modify the values in `state.{env}.json`.
* `{{config.manifest.xx}}` is customized placeholder, whose value is resolved from `config.{env}.json`.

You can add a customized parameter by:

* Adding a placeholder in `manifest.template.json` with pattern: `{{config.manifest.xx}}`.
* Adding a config value in `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### Preview app manifest in Teams Toolkit

You can preview values in app manifest in two ways:

* When you hover over the placeholder in `manifest.template.json`, then you can see the values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Screenshot is an example showing when you hover over placeholder, can view the values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Screenshot is an example showing when you hover over key beside placeholder can view the same values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. You can follow the guidance inside the hover to generate corresponding values.

### Preview manifest file

You can sideload for local, or deploy for Azure to preview the manifest file. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Screenshot is an example of showing preview manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Screenshot is an example of showing the navigation to zip app package for local and Azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer section, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Screenshot is an example of showing the list of Teams toolkit menus from solution explorer." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** file under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Screenshot is an example of showing the preview manifest menu for local and Azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer section. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Screenshot is an example of showing the navigation to update manifest in Teams developer portal." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

The changes are updated to Teams Developer Portal.

> [!NOTE]
>
> * Select **Overwrite and update** or **Cancel** from the **Warning** dialog box to make any manual updates that can be overwritten in the Developer Portal.
> * When you create a Teams command bot using Visual Studio, two app IDs are registered in Azure Active Directory. You can identify the app IDs in the Developer Portal as **Application client ID** under Basic information and existing **Bot ID** under **App features**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Screenshot is an example of showing the update warning." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)
* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)
* [Deploy Teams app to the cloud using Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
