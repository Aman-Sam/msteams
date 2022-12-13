---
title: Deep link to a Teams chat
author: v-npaladugu
description:  In this article, learn how to create deep links to a chat and navigate them in your Microsoft Teams.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
---

# Deep link to Teams chat

You can navigate to or create private chats between users with TeamsJS by specifying the set of participants. If a chat doesn’t exist with the specified participants, the user is navigated to an empty new chat. New chats are created in draft state until the user sends the first message. Otherwise, you can specify the name of the chat if it doesn’t already exist, along with text that should be inserted into the user's compose box. You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.

As an example use case, if you’re returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person. The following example demonstrates how to open a chat message to a group of participants with an initial message.

```javascript
if(chat.isSupported()) {
    const chatPromise = chat.openGroupChat({ users: ["joe@contoso.com","bob@contoso.com"], topic: "Prep For Meeting Tomorrow", message: "Hi folks kicking off chat about our meeting tomorrow"});
    chatPromise.
      then((result) => {/*Successful operation*/}).
      catch((error) => {/*Unsuccessful operation*/});
}
else { /* handle case where capability isn't supported */ }
```

While use of the typed APIs is recommended, you can alternatively use the following format for a manually created deep link that you can use in a bot, connector, or message extension card:

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`

The query parameters are:

* `users`: The comma-separated list of user IDs representing the participants of the chat. The user that performs the action is always included as a participant. Currently, the User ID field supports the Microsoft Azure Active Directory (Azure AD) UserPrincipalName, such as an email address only.
* `topicName`: An optional field for chat's display name, if a chat has three or more users. If this field isn't specified, the chat's display name is based on the names of the participants.
* `message`: An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.

To use this deep link with your bot, specify this as the URL target in your card's button or tap action through the `openUrl` action type.

## Generate deep links to channel conversation

Use this deep link format to go to a particular conversation within channel thread:

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

Example: `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

The query parameters are:

* `channelId`: Channel ID of the conversation. For example, `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`.
* `tenantId`: Tenant ID such as `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `groupId`: Group ID of the file. For example, `3606f714-ec2e-41b3-9ad1-6afb331bd35d`.
* `parentMessageId`: Parent message ID of the conversation.
* `teamName`: Name of the team.
* `channelName`: Name of the team's channel.

> [!NOTE]
> You can see `channelId` and `groupId` in the URL from the channel.

## Deep links to navigate chat messages

Use the following deep link format to navigate a user to a message in a personal or group chat in Teams:

`http://teams.microsoft.com/l/message/{chatId}/{messageId}?context={"contextType":"chat"}`

Example: `http://teams.microsoft.com/l/message/19:253f5895-9a62-4362-8d38-43f0205c702c_f1b94dcf-0aa3-4989-bcdf-ef4a5ed00f86@unq.gbl.spaces/1563480968434?context=%7B%22contextType%22:%22chat%22%7D`

The query parameters are:

* `chatId`: ChatId of the conversation. The supported format for `chatId` is 19:xxx. For example, `19:253f5895-9a62-4362-8d38-43f0205c702c_f1b94dcf-0aa3-4989-bcdf-ef4a5ed00f86@unq.gbl.spaces`.

   Apps can read a chat ID through app context in Teams, incoming payload to bot, or through [Microsoft Graph APIs](/graph/api/chat-get?view=graph-rest-1.0&tabs=http&preserve-view=true).

   > [!NOTE]
   > For one-on-one chats with bot, the incoming payload to bot contains the conversation ID in a:xxx format.

* `messageId`: Each message in a chat has a unique ID. When a bot posts a message in chat, the `messageId` is returned. You can also get the `messageId` through [Microsoft Graph APIs](/graph/api/message-get?view=graph-rest-1.0&tabs=http&preserve-view=true). For example, `1563480968434`.

* `context`: Specify the contextType as chat.

### Generate deep links to file in channel

The following deep link format can be used in a bot, connector, or message extension card:

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

The query parameters are:

* `fileId`: Unique file ID from Sharepoint Online, also known as `sourcedoc`. For example,`1FA202A5-3762-4F10-B550-C04F81F6ACBD`.
* `tenantId`: Tenant ID such as `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `fileType`: Supported file type, such as .docx, .pptx, .xlsx, and .pdf.
* `objectUrl`: Object URL of the file. The format is `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`. For example, `https://microsoft.sharepoint.com/teams/(filepath)`.
* `baseUrl`: Base URL of the file. The format is `https://{tenantName}.sharepoint.com/sites/{TeamName}`. For example, `https://microsoft.sharepoint.com/teams`.
* `serviceName`: Name of the service, app ID. For example, `teams`.
* `threadId`: The threadId is the team ID of the team where the file is stored. It's optional and can't be set for files stored in a user's OneDrive folder. threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId`: Group ID of the file. For example, `ae063b79-5315-4ddb-ba70-27328ba6c31e`.

> [!NOTE]
> You can see `threadId` and `groupId` in the URL from the channel.  

The following deep link format is used in a bot, connector, or message extension card:

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

The following example format illustrates the deep link to files:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

#### Serialization of this object

```javascript
{
fileId: "5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80",
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```

### Navigate to a chat

1. Group chat

   Use this deep link format to go to a message in personal and group chats in Teams:

   `http://teams.microsoft.com/l/message/{chatId}/{messageId}?context={"contextType":"chat"}`

   Example: `http://teams.microsoft.com/l/message/19:253f5895-9a62-4362-8d38-43f0205c702c_f1b94dcf-0aa3-4989-bcdf-ef4a5ed00f86@unq.gbl.spaces/1563480968434?context=%7B%22contextType%22:%22chat%22%7D`

   The query parameters are:

   * `chatId`: ChatId of the conversation. You can get the `chatId` from URL of the chat in Teams web client or using the [Microsoft Graph API](/graph/api/chat-get?view=graph-rest-1.0&tabs=http&preserve-view=true). For example, `19:253f5895-9a62-4362-8d38-43f0205c702c_f1b94dcf-0aa3-4989-bcdf-ef4a5ed00f86@unq.gbl.spaces`.

     Apps can read a group chat ID through context using the Microsoft Teams JavaScript library or from the incoming request payload to Bot.

   * `messageId`: Each message in a chat has a unique ID. You can get the `messageId` for a message in the following ways:

   * When a bot posts a message in chat, the bots  receives a notification with the `messageId`.
   * Using graph API, when there is an action in the chat window. For example, `1563480968434`.

   * `contextObject`: Specify the contextType as chat.

2. Channel

   Use this deep link format to navigate to a particular conversation within channel thread:

   `https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

   Example: `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

   The query parameters are:

    * `channelId`: Channel ID of the conversation. For example, `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`.
    * `tenantId`: Tenant ID such as `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
    * `groupId`: Group ID of the file. For example, `3606f714-ec2e-41b3-9ad1-6afb331bd35d`.
    * `parentMessageId`: Parent message ID of the conversation.
    * `teamName`: Name of the team.
    * `channelName`: Name of the team's channel.

       > [!NOTE]
       > You can see `channelId` and `groupId` in the URL from the channel.

## Navigate to a chat message

### Navigate to a chat message

Applications can navigate a user to a specific message.  

For navigating to a specific message in a chat refer to the following deep link format:
<TODO – get the format from feature team, we haven’t documented it>.

Use this deep link format to navigate to a particular conversation within channel thread:

`https://teams.microsoft.com/l/message/<channelId>/<parentMessageId>?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=<parentMessageId>&teamName=<teamName>&channelName=<channelName>&createdTime=<createdTime>`

Example: `https://teams.microsoft.com/l/message/<channelId>/1648741500652?tenantId=<tenantId>&groupId=<groupId>&parentMessageId=1648741500652&teamName=<teamName>&channelName=<channelName>&createdTime=1648741500652`

The query parameters are:

* `channelId`: Channel ID of the conversation. For example, `19:3997a8734ee5432bb9cdedb7c432ae7d@thread.tacv2`.
* `tenantId`: Tenant ID such as `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `groupId`: Group ID of the file. For example, `3606f714-ec2e-41b3-9ad1-6afb331bd35d`.
* `parentMessageId`: Parent message ID of the conversation.
* `teamName`: Name of the team.
* `channelName`: Name of the team's channel.

> [!NOTE]
> You can see `channelId` and `groupId` in the URL from the channel.

### Open a file

Generate deep links to file in channel

The following deep link format can be used in a bot, connector, or message extension card:

`https://teams.microsoft.com/l/file/<fileId>?tenantId=<tenantId>&fileType=<fileType>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadId>&groupId=<groupId>`

The query parameters are:

* `fileId`: Unique file ID from Sharepoint Online, also known as `sourcedoc`. For example,`1FA202A5-3762-4F10-B550-C04F81F6ACBD`.
* `tenantId`: Tenant ID such as `0d9b645f-597b-41f0-a2a3-ef103fbd91bb`.
* `fileType`: Supported file type, such as .docx, .pptx, .xlsx, and .pdf.
* `objectUrl`: Object URL of the file. The format is `https://{tenantName}.sharepoint.com/sites/{TeamName}/SharedDocuments/{ChannelName}/FileName.ext`. For example, `https://microsoft.sharepoint.com/teams/(filepath)`.
* `baseUrl`: Base URL of the file. The format is `https://{tenantName}.sharepoint.com/sites/{TeamName}`. For example, `https://microsoft.sharepoint.com/teams`.
* `serviceName`: Name of the service, app ID. For example, `teams`.
* `threadId`: The threadId is the team ID of the team where the file is stored. It's optional and can't be set for files stored in a user's OneDrive folder. threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype.
* `groupId`: Group ID of the file. For example, `ae063b79-5315-4ddb-ba70-27328ba6c31e`.

> [!NOTE]
> You can see `threadId` and `groupId` in the URL from the channel.

The following example format illustrates the deep link to files:

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`
