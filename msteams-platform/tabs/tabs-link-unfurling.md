---
title: Tabs link unfurling and Stage View
author: Rajeshwari-v
description: Learn about stage view, a full screen UI component invoked to surface your web content. Link unfurling is used to turn URLs into a tab using Adaptive Cards.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
---

# Tabs link unfurling and Stage View

Stage View is a user interface (UI) component, that allows you to render content in a full screen within Teams or as a new window.

> [!NOTE]
> This article is based on  Microsoft Teams JavaScript client SDK version 2.0.x. If you are using an earlier version, see [TeamsJS client library](how-to/using-teams-client-library.md) for guidance on the differences between the latest TeamsJS and earlier versions.

<!--It allows users to maintain their context within their new window experience while continuing  group chat conversation. <br> Developers have to enable Tab link Unfurling for their app to get Stage View update for free. Users are still able to pin the app content as a tab. It's a new entry point to pinning app content but it will not change the existing functionality of tabs or pinning. 

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]-->

## Stage View

Stage View is a full screen UI component that can be used to render your app content, providing users with a focused experience to engage with your app. Stage View can be invoked from either an adaptive card or a deep link, in both chats and channels.

When Stage View is opened from an adaptive card, it renders your app content in a new Teams window and this collaborative Stage View enables your users to multi-task and collaborate with others easily.

The Collaborative Stage View surfaces the originating chat/thread from where it was opened, giving users the ability to engage with content and conversation side-by-side.

Stage View is a full screen UI component that you can invoke to surface your web content. The existing link unfurling service is updated so that it's used to turn URLs into a tab using an Adaptive Card and Chat services.

* When users invoke Stage View from Adaptive cards within chats, Stage View opens in a new window
* When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card. The user can select **View** in the card, and pin the content as a tab directly from Stage View

:::image type="content" source="~/assets/images/tab-images/stage-view.png" alt-text="Stage View" border="true":::

## Collaborative Stage View

Collaborative Stage View is an enhancement to Stage View, that allows for your app content to exist in multiple Teams windows. From within a group chat or channel, when a user opens Stage View from an Adaptive Card, it will open the app content in a new Teams window instead of a modal.

The Collaborative Stage View also opens an accompanying side-panel chat that shows users the group chat or channel thread from which they invoked the Collaborative Stage View. This gives users the context to continue collaborating directly within their new window. When invoked from the Teams web client or mobile, the Collaborative Stage View experience will fall back to the full screen Stage View modal.

|Feature |Notes |Desktop |Web |Mobile|
|---      |:-----  |:--------   |:----  |:----- |
|Collab Stage View| Invoke from Adaptive Card action. |Chat/Channel: Opens Teams pop-out window with chat pane| Opens Stage View modal. |Opens Stage View modal|
|Stage View |Invoke from Deeplink only. Only recommended when calling from your tab app, and not an Adaptive Card. |Opens Stage View modal| Opens Stage View modal| Opens Stage View modal|

### Advantages of Stage View

* Provides enhanced experience to view content in Teams
* Allows users to do multi-task within Teams in a separate window

## Advantages of Collaborative Stage View

Collaborative Stage View helps provide a more seamless, multi-task experience when working with content in Teams. Users can open and view your app content inside a new Teams window and continue discussion from this window. The ability to engage with content while also having a conversation about that same content, leads to higher user engagement with your app.

The following screenshot is an example of collaborative Stage View opens in a new Teams window with the originating chat in the side panel:

:::image type="content" source="../assets/images/tab-images/collaborative-stage-view.png" alt-text="Screenshot shows the Collaborative stage view in Teams.":::

### Limitations of Stage View

* If a Stage View is already open, and the user selects on another stage link in the same chat, it will replace the existing Stage View window

* If a Stage View with chat is open and a meeting with the same chat gets started, Stage View window will get closed automatically. When the meeting ends, Stage View window will be restored

* If a Stage View link is opened from main window or chat window, it will replace with the Stage View window with side chat pane

### Stage View vs. Task module

| Stage View | Task module|
|:-----------|:-----------|
| Stage View is useful to display rich content to the users, such as a page, a dashboard, a file, and so on. It provides rich features that help to render your content in the new pop-up window. <br><br> It provides rich features that help to render your content in the full-screen canvas. <br><br> After your app content has been opened in Stage View, users can choose to pin the content as a tab. <br><br> For even more collaborative capabilities, opening your content in Collaborative Stage View (via an Adaptive Card) allows users to engage with content and conversation side-by-side, while also enabling multi-window scenarios.| [Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that require user attention, or collect information required to move to the next step.|

### Invoke Stage View

You can invoke Stage View in the following  ways:

* [Invoke Stage View from Adaptive Card](#invoke-stage-view-from-adaptive-card)
* [Invoke Collaborative Stage View from Adaptive Card](#invoke-collaborative-stage-view-from-adaptive-card)
* [Invoke Stage View through deep link](#invoke-stage-view-through-deep-link)

### Invoke Stage View from Adaptive Card

When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage. Now Stage View opens in a new window with chat docked to the side. After a stage is launched and the **tabInfo** is provided, you can pin the stage as a tab.

An Adaptive Card opens a stage in the following images:

:::image type="content" source="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt-text="Open a stage from Adaptive Card" border="true":::

:::image type="content" source="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt-text="Open a stage" border="true":::

Following is the code to open a stage from an Adaptive Card:

```json
    {
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
    } 
```

The `invoke` request type must be `composeExtension/queryLink`.

> [!NOTE]
>
> * `invoke` workflow is similar to the current `appLinking` workflow
> * To maintain consistency, it is recommended to name `Action.Submit` as `View`
> * `websiteUrl` is a required property to be passed in the `TabInfo` object
**To invoke Stage View**:

1. When the user selects **View**, the bot receives an `invoke` request. The request type is `composeExtension/queryLink`.
1. `invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.
1. The bot responds with a `200` code.

> [!NOTE]
> On Teams mobile clients, invoking Stage View for apps distributed through the [Teams store](/platform/concepts/deploy-and-publish/apps-publish-overview.md) and not having a moblie-optimized experience opens the default web browser of the device. The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.

### Invoke Collaborative Stage View from Adaptive Card

When the user enters an app content URL in a chat, the bot is invoked and returns an Adaptive Card with the option to open the URL. Depending on the context and the users’ client (see table in the ‘Collaborative Stage View’ section), this URL is opened in the appropriate Stage View UI . When the Collaborative Stage View is invoked from an Adaptive Card in a chat/channel (and not from a deep link), a new window is opened.

The following images display the Collaborative Stage View opened from an Adaptive Card:

:::image type="content" source="../assets/images/tab-images/collaborative-stage-view-adaptive-card.png" alt-text="Screenshot shows the invoke collaborative Stage View from Adaptive Card.":::

:::image type="content" source="../assets/images/tab-images/collaborative-stage-view.png" alt-text="Screenshot shows the Collaborative stage view in Adaptive Card.":::

Following is the code to create a Collaborative Stage View button open a stage in an Adaptive Card:

```json
{
    type: "Action.Submit",
    name: "Open",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Sales Report",  
                    entityId: "entityId"
                 }
                }
            }
        }
} 

```

The invoke request type must be composeExtension/queryLink.

> [!NOTE]
>
> * Invoke workflow is similar to the current appLinking workflow.
> * To maintain consistency, it is recommended to name Action.Submit as Open.
> * websiteUrl is a required property to be passed in the TabInfo object.
> * Passing a Stage View deep link into an adaptive card won't open the Collaborative Stage View. Stage View deep link always open to the Stage View Modal.
> * For Stage View to open unfurl open properly, ensure the URL of the content is within the list of validDomains in your app manifest
> * Learn more about building Adaptive Cards in Teams.

**To invoke collaborative Stage View**:

1. Adaptive Card Link Unfurling:
   1. The sharer shares a URL in a chat.
   1. This sends an invoke request to the bot.(request type: composeExtension/queryLink)
   1. The bot returns the adaptive card JSON, with tab/tabInfoAction in it.
   1. Adaptive Card JSON is rendered.

1. Opening Stage View
   1. A receiver clicks on an action button on the adaptive card.
   1. Stage View opens based on the content of the Adaptive Card.

> [!NOTE]
>
> * On Teams mobile clients, invoking Stage View for apps distributed through the [Teams store](/platform/concepts/deploy-and-publish/apps-publish-overview.md) and not having a mobile optimized experience opens the default web browser of the device. The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.
> * The multi-window Collaborative Stage View is also not available in the Teams web client or mobile. In these scenarios, the Stage View experience will fall back to showing users the content in an interstitial modal.

### Invoke Stage View through deep link

To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `app.openLink(url)` API. To invoke Stage View from a deep link will always default to the modal experience (and not a Teams window). The deep link can also be passed through an `OpenURL` action in the card,  the Stage View deep link is intended for the tab canvas. For Adaptive Cards, we encourage developers to follow the JSON Adaptive Card example.

The following is an example from deep link Stage View opens as a modal within the main Teams window:

:::image type="content" source="../assets/images/tab-images/invoke-stage-view-deep-link.png" alt-text="Screenshot shows the invoke stage view through deep link.":::

> [!NOTE]
>
> * All deep links must be encoded before pasting the URL. We don't support unencoded URLs.
> * The `name` is optional in deep link. If not included, the app name replaces it.
> * When you launch a Stage from a certain context, ensure that your app works in that context. For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.

#### Syntax

The deep link syntax is as follows:

`<https://teams.microsoft.com/l/stage/{appId}/0?context>={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}`

#### Examples

When a user enters a URL, it's unfurled into an Adaptive card.Following are the deep link examples to invoke Stage View:

<br>

<details>
<summary><b>Example 1</b></summary>
URL with threadId

Unencoded URL:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}`

Encoded URL:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D>`

</details>

<br>

<details>
<summary><b>Example 2</b></summary>
URL without threadId

Unencoded URL:

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous"}`

Encoded URL:

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D>`

</details>

<br>

> [!NOTE]
>
> * All deep links must be encoded before pasting the URL. We don't support unencoded URLs.
> * The `name` is optional in deep link. If not included, the app name replaces it.
> * The deep link can also be passed through an `OpenURL` action.
> * When you launch a Stage from a certain context, ensure that your app works in that context. For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.

## Tab information property

| Property name | Type | Number of characters | Description |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | This property is a  unique identifier for the entity that the tab displays and it's a required field.|
| `name` | String | 128 | This property is the display name of the tab in the channel interface and it's an optional field.|
| `contentUrl` | String | 2048 | This property is the `<https://>` URL that points to the entity UI to be displayed in the Teams canvas and it's a required field.|
| `websiteUrl?` | String | 2048 | This property is the `<https://>` URL to point at, if a user selects to view in a browser and it's a required field.|
| `removeUrl?` | String | 2048 | This property is the `<https://>` URL that points to the UI to be displayed when the user deletes the tab and it's an optional field.|

## Code sample

| Sample name | Description | .NET |Node.js|
|-------------|-------------|------|----|
|Tab in stage view |Microsoft Teams tab sample app for demonstrating tab in stage view.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## Next step

> [!div class="nextstepaction"]
> [Create conversational tabs](~/tabs/how-to/conversational-tabs.md)

## See also

* [Build tabs for Teams](what-are-tabs.md)
* [Add link unfurling](../messaging-extensions/how-to/link-unfurling.md)
* [composeExtensions](../resources/schema/manifest-schema.md#composeextensions)
* [Build tabs with Adaptive Cards](how-to/build-adaptive-card-tabs.md)
* [Create deep links](../concepts/build-and-test/deep-links.md)
