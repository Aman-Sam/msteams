---
title: Messaging extensions
author: surbhigupta
description: An overview of messaging extensions on the Microsoft Teams platform
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
---
# Messaging extensions

Messaging extensions allow the users to interact with your web service through buttons and forms in the Microsoft Teams client. They can search or initiate actions in an external system from the compose message area, the command box, or directly from a message. You can send back the results of that interaction to the Microsoft Teams client in the form of a richly formatted card. This document gives an overview of the messaging extension, tasks performed under different scenarios, working of messaging extension, action and search commands, and link unfurling.

The following image displays the locations from where messaging extensions are invoked:

![messaging extension invoke locations](~/assets/images/messaging-extension-invoke-locations.png)

> [!NOTE]
> @mentioning message extensions is no longer supported in the compose box.

## Scenarios where messaging extensions are used

| Scenario | Example |
|:-----------------|:-----------------|
|You want some external system to do an action  and the result of the action to be sent back to your conversation.|Reserve a resource and allow the channel to know the reserved time slot.|
|You want to find something in an external system, and share the results with the conversation.|Search for a work item in Azure DevOps, and share it with the group as an Adaptive Card.|
|You want to complete a complex task involving multiple steps or lots of information in an external system, and share the results with a conversation.|Create a bug in your tracking system based on a Teams message, assign that bug to Bob, and send a card to the conversation thread with the bug's details.|

## Understand how messaging extensions work

A messaging extension consists of a web service that you host and an app manifest, which defines where your web service is invoked from in the Microsoft Teams client. The web service takes advantage of the Bot Framework's messaging schema and secure communication protocol, so you must register your web service as a bot in the Bot Framework. 

> [!NOTE]
> Though you can create the web service manually, use [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) to work with the protocol.

In the app manifest for Microsoft Teams app, a single messaging extension is defined with up to ten different commands. Each command defines a type, such as action or search and the locations in the client from where it is invoked. The invoke locations are compose message area, command bar, and message. On invoke, the web service receives an HTTPS message with a JSON payload including all the relevant information. Respond with a JSON payload, allowing the Teams client to know the next interaction to enable. 

## Types of messaging extension commands

There are two types of messaging extension commands, action command and search command. The messaging extension command type defines the UI elements and interaction flows available to your web service. Some interactions, such as authentication and configuration are available for both types of commands.

### Action commands

Action commands are used to present the users with a modal popup to collect or display information. When the user submits the form, your web service responds by inserting a message into the conversation directly or by inserting a message into the compose message area. After that the user can submit the message. You can chain multiple forms together for more complex workflows.

The action commands are triggered from the compose message area, the command box, or from a message. When the command is invoked from a message, the initial JSON payload sent to your bot includes the entire message it was invoked from. The following image displays the messaging extension action command task module:
![messaging extension action command task module](~/assets/images/task-module.png)

### Search commands

Search commands allow the users to search an external system for information either manually through a search box, or by pasting a link to a monitored domain into the compose message area, and insert the results of the search into a message. In the most basic search command flow, the initial invoke message includes the search string that the user submitted. You respond with a list of cards and card previews. The Teams client renders a list of card previews for the user. When the user selects a card from the list, the full-size card is inserted into the compose message area.

The cards are triggered from the compose message area or the command box and not triggered from a message. They can not be triggered from a message.
The following image displays the messaging extension search command task module:

![messaging extension search command](~/assets/images/search-extension.png)

> [!NOTE]
> For more information on cards, see [what are cards](../task-modules-and-cards/what-are-cards.md).

## Link unfurling

A web service is invoked when a URL is pasted in the compose message area. This functionality is known as link unfurling. You can subscribe to receive an invoke when URLs containing a particular domain are pasted into the compose message area. Your web service can "unfurl" the URL into a detailed card, providing more information than the standard website preview card. You can add buttons to allow the users to immediately take action without leaving the Microsoft Teams client.
The following images display link unfurling feature when a link is pasted in messaging extension:
 
![unfurl link](../assets/images/messaging-extension/unfurl-link.png)

![link unfurling](../assets/images/messaging-extension/link-unfurl.gif)

## Code sample

| **Sample name** | **Description** | **.NET** | **Node.js** | **Python** |
|------------|-------------|----------------|------------|
| Messaging extension with action-based commands | This sample illustrates how to build an action-based messaging extension. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Messaging extension with search-based commands | This sample illustrates how to build a Search-based Messaging Extension. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## See also

[Create a messaging extension](../build-your-first-app/build-messaging-extension.md)


## Next step

> [!div class="nextstepaction"]
> [Define action messaging extension command](~/messaging-extensions/how-to/action-commands/define-action-command.md)

> [!div class="nextstepaction"]
> [Define search messaging extension command](~/messaging-extensions/how-to/search-commands/define-search-command.md)
