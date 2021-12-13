---
title: Receive all conversation messages with RSC
author: surbhigupta12
description: Receive all conversation messages with RSC
ms.topic: conceptual
ms.localizationpriority: medium
---

# Receive all conversation messages with RSC

The resource-specific consent (RSC) permissions model, originally developed for Teams Graph APIs, is being extended to bot scenarios.

Using RSC, you can request team owners to consent for a bot to receive user messages across standard channels or chats without being @mentioned. The capability is enabled by specifying the `ChannelMessage.Read.Group` or `ChatMessage.Read.Chat` permissions in the manifest of RSC enabled Teams app. The conversation owners can grant consent during the app installation or upgrade process.
 
For more information about enabling RSC for your app, see [resource-specific consent in Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).

## Enable bots to receive all channel or chat messages

With user consent, the `ChannelMessage.Read.Group` and `ChatMessage.Read.Chat` RSC enables graph applications, which are defined in a Teams app manifest. You can get all messages in channels and chats, and conversations where the app has been installed. If a bot is defined in an app manifest with one or both of these permissions, users will receive all messages without being @mentioned in conversations where permissions apply. The app has to be consented and installed.

> [!NOTE]
> * Services that need access to all Teams message data must use the Graph APIs that provide access to archived data in channels and chats.
> * Bots must use the `ChannelMessage.Read.Group` and `ChatMessage.Read.Chat` RSC permissions appropriately to build and enhance engaging experience for users in the team or they will not pass the store approval. The app description must include how the bot uses the data it reads.
> * The `ChannelMessage.Read.Group` and `ChatMessage.Read.Chat` RSC permissions may not be used by bots to extract large amounts of customer data.

| **RSC Permission** | **Conversation Context** | **Graph App** | **Bot** |
| -------- | --------- | ---------| --------- |
| `ChannelMessage.Read.Group` | Teams & Channels | Get all messages through Graph API in channels within team where Teams app is installed | Receive all messages sent in standard channels without being @mentioned within team where Teams app is installed |
| `ChatMessage.Read.Chat` | Chats (user:user, groups, and meetings) | Get all messages through Graph API in chats  where Teams app is installed | Receive all messages sent in chat without being @mentioned where Teams app is installed |

## Update app manifest

 For a bot to receive messages without @mention, one or both of the RSC permissions must be specified in the Teams app manifest under `webApplicationInfo.applicationPermissions`.

 ![App Manifest](~/assets/images/bots/manifest_image.png)

The following list describes the `webApplicationInfo` object:

* **id**: Your Azure Active Directory (AAD) app ID. The app ID can be the same as your bot ID.
* **resource**: Any string. The resource field has no operation in RSC, but must be added with a value to avoid error response.
* **applicationPermissions**: RSC permissions for your app with `ChannelMessage.Read.Group`and `ChatMessage.Read.Chat` must be specified. For more information, see [resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).

The following code provides an example of the app manifest:

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
"ChatMessage.Read.Chat"
    ]
  }
```

## Sideload in a conversation to test

# [Channel messages](#tab/channel)

The following steps guide you to sideload and validate bot that receives all channel messages in a Team without being @mentioned:

1. Select or create a team.
1. Select the ellipses &#x25CF;&#x25CF;&#x25CF; from the left pane. The drop-down menu appears.
1. Select **Manage team** from the drop-down menu. The details appear:

    ![Managing apps in team](~/bots/how-to/conversations/Media/managingteam.png)

1. Select **Apps**. Multiple apps appear.
1. Select **Upload a custom app** from the lower right corner":

    ![Uploading custom app](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. Select the app package from the **Open** dialog box.
1. Select **Open**:

    ![Selecting app package](~/bots/how-to/conversations/Media/selectapppackage.png)

1. Select **Add** from the app details pop-up, to add the bot to your selected team:

    ![Adding the bot](~/bots/how-to/conversations/Media/addingbot.png)

1. Select a channel and enter a message in the channel for your bot:

    ![Bot receives message](~/bots/how-to/conversations/Media/botreceivingmessage.png)

   The bot receives the message without being @mentioned.

    ![Bot receives message](~/bots/how-to/conversations/Media/botreceivingmessage-noatmention.png)

# [Chat messages](#tab/chat)

The following steps guide you to sideload and validate bot that receives all chat messages without being @ mentioned in a chat:

1. Select or create a group chat.
1. Select the ellipses &#x25CF;&#x25CF;&#x25CF; from the group chat. The drop-down menu appears.
1. Select **Manage apps** from the drop-down menu:

   ![Manage apps in team](~/assets/images/bots/Chats_Manage_Apps_Entry.png)

1. Select **Upload a custom app** from the lower right corner of **Manage apps**:

    ![Uploading custom app](~/assets/images/bots/Chats_Manage_Apps_Page.png)

1. Select the app package from the **Open** dialog box.
1. Select **Open**:

    ![Selecting app package](~/assets/images/bots/Chats_Sideload_App_FilePicker.png)

1. Select **Add** from the app details pop-up, to add the bot to your selected group chat:

    ![Adding the bot](~/assets/images/bots/Chats_Install_Dialog.png)

1. Enter a message in the group chat for your bot:

   ![Bot receives message](~/assets/images/bots/Bot_ReceiveMessage.png)

   The bot receives the message without being @mentioned:

   ![No mention](~/assets/images/bots/Bot_NoMention.png)

---

## Code sample

| Sample name | Description | C# |Node.js|
|-------------|-------------|------|----|
|Channel messages with RSC permissions|Microsoft Teams sample app demonstrating on how a bot can receive all channel messages with RSC without being @mentioned.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## See also

* [Bot conversations](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Resource-specific consent](/microsoftteams/resource-specific-consent)
* [Test resource-specific consent](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Upload custom app in Teams](~/concepts/deploy-and-publish/apps-upload.md)
