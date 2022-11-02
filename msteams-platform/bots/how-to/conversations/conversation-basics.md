---
title: Conversation basics
description: In this module, learn about bot conversation type in a channel, personal chat, and a group chat scopes in Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
---

# Conversation basics

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

A conversation is a series of messages sent between your Microsoft Teams bot and one or more users. The following table provides the three types of conversations, also called scopes in Teams:

| Conversation type | Description |
| ------- | ----------- |
| `channel` | This conversation type is visible to all members of the channel. |
| `personal` | This conversation type includes conversations between bots and a single user. |
| `groupChat` | This conversation type includes chat between a bot and two or more users. It also enables your bot in meeting chats. |

A bot behaves differently depending on the conversation it's involved in:

* Bots in channel and group chat conversations require the user to @mention the bot to invoke it in a channel.

* Bots in a one-to-one conversation don't require an @mention. All messages sent by the user routes to your bot.

> [!NOTE]
> Bots can be enabled to receive all channel messages in a team without being @mentioned using resource-specific consent (RSC) permissions. This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only. For more information, see [receive all channel messages with RSC](channel-messages-with-rsc.md).

For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).

Each message in a bot conversation is an `Activity` object of type `messageType: message`. When a user sends a message, Teams posts the message to your bot and the bot handles the message. In addition, to define core commands that your bot responds to, you can add a command menu with a drop-down list of commands for your bot. Bots in a group or channel only receive messages when they're mentioned @botname. Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active. You can capture these events in your code and take action on them.

A bot can also send proactive messages to users. A proactive message is any message sent by a bot that isn't in response to a request from a user. You can format your bot messages to include rich cards that include interactive elements, such as buttons, text, images, audio, video, and so on. Bot can dynamically update messages after sending them, instead of having your messages as static snapshots of data. Messages can also be deleted using the Bot Framework's `DeleteActivity` method.

## Add SSO authentication to your conversation bots

You can add single sign-on authentication to your conversation bot using the following steps:

* [Create Teams conversation bot](../../../sbs-teams-conversation-bot.yml)
* [Configure your bot app in Azure AD](/bots/how-to/authentication/bot-sso-register-aad)

## Next step

> [!div class="nextstepaction"]
> [Messages in bot conversations](~/bots/how-to/conversations/conversation-messages.md)
