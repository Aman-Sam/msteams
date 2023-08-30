---
title: Tab margin changes
author: surbhigupta
description: Learn how to remove margins around tabs in Microsoft Teams with UI kit. Know extra padding effect, margin size for left, right, top, and bottom.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.date: 07/21/2022
---

# Tab margin changes

This document describes how the removal of margins around all tabs in Microsoft Teams enhances your app building experience. It's an enhancement introduced in Teams in 2021.
You can build apps that look more native to Teams by removing the margins around all tabs. Tabs with removed margins align with Microsoft Teams' [UI kit designs](~/tabs/design/tabs.md). Most apps experience enhanced look without margins.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Tab wit and without margins":::

> [!NOTE]
> This feature is not applicable to mobile clients, as the tabs viewed in the mobile clients don't have margins.

## Guidelines

Tab margins removal affects your Teams apps that use tabs. In such cases, you can add margins around your tab designs where it's required. App designs in production have an extra padding effect, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and goes away in a few weeks, leaving only the app's provided padding.

## FAQ

<details>
<summary>Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?</summary>

Yes, it's allowed and Teams encourages such designs that help the app to feel native.

</details>

</details>

<details>
<summary>Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?</summary>

No, you must provide your own padding or margins of all app content to ensure that it doesn't touch the left and right edges of your UI. You can also add margins at the top of your tab, if necessary.

</details>

<details>
<summary>What's the size of the tab margins that Teams applied previously?</summary>

* Left and right: 20 pixels
* Top: 16 pixels
* Bottom: 0 pixels

</details>

> [!IMPORTANT]
>
> * All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.
> * The tab margin removal change applies to all tabs. There is no way to opt-in or opt-out of the change.
> * Tab margins' change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.

## See also

* [Build tabs for Teams](../tabs/what-are-tabs.md)
* [Create a personal tab](../tabs/how-to/create-personal-tab.md)
* [Create a channel tab or group tab](../tabs/how-to/create-channel-group-tab.md)
