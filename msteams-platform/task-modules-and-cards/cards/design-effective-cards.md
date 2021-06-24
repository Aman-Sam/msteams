---
title: Designing Adaptive Cards for your app
description: Learn how to design Adaptive Cards for Teams and get the Microsoft Teams UI Kit.
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
---
# Designing Adaptive Cards for your Microsoft Teams app

An Adaptive Card contains a freeform body of card elements and optional set of actions. Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension. Using text, graphics, and buttons, these cards provide rich communication to your audience.

The Adaptive Card framework is used across many Microsoft products, including Teams. You can send cards inside messages to users via bots or messaging extensions. Users can also take actions on cards when present.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Overview example of an Adaptive Card." border="false":::

## Microsoft Teams UI Kit

You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit. The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.

> [!div class="nextstepaction"]
> [Get the Microsoft Teams UI Kit (Figma)](https://www.figma.com/community/file/916836509871353159)

## Adaptive Cards designer

You also can start designing your Adaptive Cards directly in the browser.

> [!div class="nextstepaction"]
> [Try the Adaptive Cards designer](https://adaptivecards.io/designer/)

## Types of Adaptive Cards

### Hero

Our largest card. Use for sharing articles or scenarios where an image tells most of the story.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Example shows an Adaptive Card hero card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="Example shows an Adaptive Card hero card on mobile." border="false":::

---

### Thumbnail

Use for sending a simple actionable message.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Example shows an Adaptive Card thumbnail card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="Example shows an Adaptive Card thumbnail card on mobile." border="false":::

---

### List

Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Example shows an Adaptive Card list card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="Example shows an Adaptive Card list card on mobile." border="false":::

---

### Digest

Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false":::

---

### Media

Use when you want to combine text and media, like audio or video.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Example shows an Adaptive Card media card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="Example shows an Adaptive Card media card on mobile." border="false":::

---

### People

Best used when you to efficiently convey who's involved with a task.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Example shows an Adaptive Card people card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="Example shows an Adaptive Card people card on mobile." border="false":::

---

### Request ticket

Use to get quick inputs from a user to automatically create a task or ticket.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Example shows an Adaptive Card request ticket card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="Example shows an Adaptive Card request ticket card on mobile." border="false":::

---

### Image set

Use to send multiple image thumbnails.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Example shows an Adaptive Card image set card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="Example shows an Adaptive Card image set card on mobile." border="false":::

---

### Action set

Use when you want to the user to select a button, then gather addition user input from the same card.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Example shows an Adaptive Card action set card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="Example shows an Adaptive Card action set card on mobile." border="false":::

---

### Choice set

Use to gather multiple inputs from the user.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Example shows an Adaptive Card choice set card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="Example shows an Adaptive Card choice set card on mobile." border="false":::

---

## Anatomy

Adaptive Cards have a lot of flexibility. But at minimum, we strongly suggest including the following components in every card.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample shows Adaptive Card anatomy." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="Example shows Adaptive Card anatomy on mobile." border="false":::

---

|Counter|Description|
|----------|-----------|
|A|**Header**: Make your headers clear and concise.|
|B|**Body copy**: Convey details that are either too long or not important enough to include in the header.|
|C|**Primary actions**: As a best practice, include 1-3 primary actions. You can have up to six.|

## Best practices

Use these recommendations to create a quality app experience.

### Primary and secondary actions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Best practice about how you should include only a small set of actions on an Adaptive Card." border="false":::

#### Do: Use up to six primary actions

While Adaptive Cards can support six primary actions, most cards don’t need that. Actions should be clear, concise, and straight forward. Less is more.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Best practice about how not to overwhelm users with too many actions on an Adaptive Card." border="false":::

#### Don't: Use more than six primary actions

Adaptive Cards should present quick, actionable content. Too many actions can overwhelm a user.

   :::column-end:::
:::row-end:::

### Frequency

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Best practice about Adaptive Card frequency." border="false":::

#### Do: Be concise

It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful. Try to limit yourself to the essentials. This is especially true in a channel where users have less tolerance for what they perceive as "noise".
