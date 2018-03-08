---
title: Introducing cards
description: Describes cards and how they are used in bots, connectors and messaging extensions
keywords: connectors bots cards messaging
ms.date: 03/06/18
---
# Cards

A *card* is a user-interface (UI) container for short or related pieces of information. Cards can have multiple properties and attachments. Cards can include buttons which can trigger [Card actions](~/concepts/cards/cards-actions).

## Cards in Connectors

Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors. Like many Office 365 applications, Teams supports Connectors. You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/concepts/connectors), and find the specification for cards in connectors in [Actionable message card reference](https://docs.microsoft.com/en-us/outlook/actionable-messages/card-reference).

Any card used by any O365 Connector will work in Teams as part of a Connector in Teams.

## Cards in Bots

The Microsoft Bot Framework extends the cards specification by adding a set of predefined cards that bots can use as part of bot messages. Teams supports bots using the Bot Framework and supports a slightly different set of these cards. General information on cards in Bot Framework can be found in [Add rich card attachments to messages](https://docs.microsoft.com/en-us/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).

The cards that are supported by bots are detailed in [Teams Card Reference](~/concepts/cards/cards-reference). These cards can not be used in connectors.  Connector cards can be used in bots however using the *O365 Connector Card* which encapsulates any card used in Office 365 Connectors.

## Cards in Messaging Extensions

[Messaging Extensions](~/concepts/messaging-extensions) can also return a card. These can be a Hero, Thumbnail or O365ConnectorCard. These cards can be found in the [Teams Card Reference](~/concepts/cards/cards-reference).

## Card reference

All cards used by Teams are listed in the [Teams Card Reference](~/concepts/cards/cards-reference). This reference also describes differences between Bot Framework cards and cards in Teams.
