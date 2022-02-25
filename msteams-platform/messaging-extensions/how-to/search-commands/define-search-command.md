---
title: Define messaging extension search commands
author: surbhigupta
description: Learn about messaging extension search commands for Microsoft Teams apps, to create a search command through app manifest and manually using code examples and sample.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: none
---
# Define messaging extension search commands

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Messaging extension search commands allow users to search external systems and insert the results of that search into a message in the form of a card. This document guides you on how to select  search command invoke locations, and add the search command to your app manifest.

> [!NOTE]
> The result card size limit is 28 KB. The card is not sent if its size exceeds 28 KB.

## Select search command invoke locations

The search command is invoked from any one or both of the following locations:

* Compose message area: The buttons at the bottom of the compose message area.
* Command box: By @mentioning in the command box.

  When search command is invoked from the compose message area, the user sends the results to the conversation. When it is invoked from the command box, the user interacts with the resulting card, or copies it for use elsewhere.

The following image displays the invoke locations of the search command:

![search command invoke locations](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## Add the search command to your app manifest

To add the search command to your app manifest, you must add a new `composeExtension` object to the top level of your app manifest JSON. You can add the search command either with the help of App Studio, or manually.

### Create a search command using App Studio

The prerequisite to create a search command is that you must already have created a messaging extension. For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).

To create a search command, follow these steps:

1. Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.
1. If you already created your app package in **App Studio**, select from the list. If you have not created an app package, import an existing one.
1. After importing app package, select **Messaging extensions** under **Capabilities**. You get a pop-up window to set up the messaging extension.
1. Select **Set up** in the window to include the messaging extension in your app experience. The following image displays the messaging extension set up page:

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. To create the messaging extension, you need a Microsoft registered bot. You can either use an existing bot or create a new bot. Select **Create new bot** option, give a name for the new bot, and select **Create**. The following image displays bot creation for messaging extension:

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.  
The following image displays command addition for messaging extension:

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. Select **Allow users to query your service for information and insert that into a message**. The following image displays the search command parameter selection:

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. Add a **Command Id** and a **Title**.
1. Select the location from where your search command must be invoked. The following image displays the search command invoke location:

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. Add your search parameter and select **Save**.

### Create a search command manually

To manually add your messaging extension search command to your app manifest, you must add the following parameters to your `composeExtension.commands` array of objects:

| Property name | Purpose | Required? | Minimum manifest version |
|---|---|---|---|
| `id` | This property is an unique ID that you assign to search command. The user request includes this ID. | Yes | 1.0 |
| `title` | This property is a command name. This value appears in the user interface (UI). | Yes | 1.0 |
| `description` | This property is a help text indicating what this command does. This value appears in the UI. | Yes | 1.0 |
| `type` | This property must be a `query`. | No | 1.4 |
|`initialRun` | If this property is set to **true**, it indicates this command should be executed as soon as the user selects this command in the UI. | No | 1.0 |
| `context` | This property is an optional array of values that defines the context the search action is available in. The possible values are `message`, `compose`, or `commandBox`. The default is `["compose", "commandBox"]`. | No | 1.5 |

You must add the details of the search parameter, that defines the text visible to your user in the Teams client.

| Property name | Purpose | Is required? | Minimum manifest version |
|---|---|---|---|
| `parameters` | This property defines a static list of parameters for the command. | No | 1.0 |
| `parameter.name` | This property describes the name of the parameter. This is sent to your service in the user request. | Yes | 1.0 |
| `parameter.description` | This property describes the parameter’s purposes or example of the value that must be provided. This value appears in the UI. | Yes | 1.0 |
| `parameter.title` | This property is a short user-friendly parameter title or label. | Yes | 1.0 |
| `parameter.inputType` | This property is set to the type of the input required. Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`. Default is set to `text`. | No | 1.4 |

#### Example

Following section is an example of the simple app manifest of the `composeExtensions` object defining a search command:

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}

```

For the complete app manifest, see [App manifest schema](~/resources/schema/manifest-schema.md).

## Universal Actions for search based messaging extensions

>[!NOTE]
> Universal Actions for search based messaging extensions is currently is currently available only in [Developer preview](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

Adaptive Cards in search based messaging extensions now support Universal Actions. To enable Universal Actions for search based messaging extensions, the app must conform to the [Schema for Universal Actions for Adaptive Cards](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) along with the following requirements:

1. The app must have a conversation bot defined in their app manifest.
1. If you already have a conversational bot, the bot must be the same that is used in your messaging extension.
1. If the card is sent in a group, the app must specify `team` or `groupchat` scope on their bot in the manifest.

The following is an example of a JSON schema with `team` and `groupchat`values:

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "scopes": [
                    "team",
                    "personal",
                    "groupchat"
                ]
        }
    ],
    "composeExtensions": [
        {
            "canUpdateConfiguration": true,
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%", // Use the same bot as what is specified in the bots section above
        }
    ]
}
```

### Automatic refresh for Adaptive Cards in search based MEs

Enable automatic refresh for Adaptive Cards in search based messaging extensions to ensure users always see the latest information. To enable, define `userIds` array either in  `29:<ID>` or `8:orgid:<AAD ID>` format in the `refresh` property. For more information, see [Work with Universal Actions for Adaptive Cards](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh).

The following is an example of `userIds` array in the `refresh` property:

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "userIds": [
                "8:orgid:<AADID>",
                "29:<id>"
            ],
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

> [!NOTE]
> Automatic refresh is enabled for all users in the group chat or channel with *less than or equal to* 60 users. For conversations (group chat or channel) with more than 60 users, users can use the refresh button in the message options menu to get the latest result.

The following is an example of `Action.Execute` in the `refresh` property:

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

### Just-in-time install

Just-in-time (JIT) allows you to install a card or messaging extension for multiple users in a group chat or channel. In order to support Universal Actions in search based Message extensions, your bot is added to the conversation where the card (with `Action.Execute`) is sent by the user.

When a user selects a card and sends it in a group chat or channel, a **JIT** installation prompt appears. After the user selects the **send** option, the app is added for all the users in the chat or channel in the background.

> [!NOTE]
> For apps that don’t have `Action.Execute` and `refresh` schema defined, the install prompt is not shown to the users.

The following is an example of a dynamic ME and JIT install user flow:

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="Dynamic ME JIT flow":::

## Code sample

| Sample Name           | Description | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams messaging extension search   |  Describes how to define search commands and respond to searches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## Step-by-step guide

Follow the [step-by-step guide](../../../sbs-messagingextension-searchcommand.yml) to build a search based messaging extension.

## Next step

> [!div class="nextstepaction"]
> [Respond to the search commands](~/messaging-extensions/how-to/search-commands/respond-to-search.md).

## See Also

* [Universal Actions for Adaptive Cards](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
* [Universal Action Model](/adaptive-cards/authoring-cards/universal-action-model)
