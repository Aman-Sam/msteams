---
title: Enable and configure your apps for Teams meetings
author: surbhigupta
description: Learn how to enable and configure your apps for Teams meetings and different meeting scenarios, update app manifest, configure features and more.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
---

# Enable and configure apps for meetings

Every team has a different way of communicating and collaborating tasks. To achieve these different tasks, customize Teams with apps for meetings. Enable your apps for Teams meetings and configure the apps to be available in meeting scope within their app manifest.

## Prerequisites

With apps for Teams meetings, you can expand the capabilities of your apps across the meeting lifecycle. Before you work with apps for Teams meetings, you must fulfill the following prerequisites:

* Know how to develop Teams apps. For more information on how to develop Teams app, see [Teams app development](../overview.md).

* Use your app that supports configurable tabs in the groupchat and/or team scope. For more information, see [scopes](../resources/schema/manifest-schema.md#configurabletabs) and [build your first tab app](../build-your-first-app/build-channel-tab.md).

* Adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios. For experiences during meetings, refer to the [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).

* For your app to update in real time, it must be up-to-date based on event activities in the meeting. These events can be within the in-meeting dialog and other stages across the meeting lifecycle. For the in-meeting dialog, see `completionBotId` parameter in [in-meeting notification payload](API-references.md#send-an-in-meeting-notification).

## Enable your app for Teams meetings

To enable your app for Teams meetings, update your app manifest and use the context properties to determine where your app must appear.

### Update your app manifest

The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays. The scope defines who can access and the context defines where your app is available.

> [!NOTE]
>
> * Apps in meetings require `groupchat` or `team` scope. The `team` scope works for tabs in channels or channel meetings.
> * To support adding tabs in scheduled channel meetings, specify **team** scope in **scopes** section in your app manifest. Without **team** scope the app would not appear in the flyout for channel meetings.
> * Apps in meetings can use the following contexts: `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` and `meetingStage`.
> * The delegated RSC permissions `MeetingStage.Write.Chat` and `ChannelMeetingStage.Write.Group` are required in the manifest to enable meeting stage sharing.

The following code snippet is an example of a configurable tab used in an app for Teams meetings:

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

### Context property

The `context` property determines what must be shown when a user invokes an app in a meeting depending on where the user invokes the app. The tab `context` and `scopes` properties enable you to determine where your app must appear. The tabs in the `team` or `groupchat` scope can have more than one context.

Support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats. With the pre-meeting app experience, you can find and add meeting apps and do the pre-meeting tasks. With the post-meeting app experience, you can view the results of the meeting, such as poll survey results or fee.

 Following are the values for the `context` property from which you can use all or some of the values:

|Value|Description|
|---|---|
| **channelTab** | A tab in the header of a team channel. |
| **privateChatTab** | A tab in the header of a group chat between a set of users, not in the context of a team or meeting. |
| **meetingChatTab** | A tab in the header of a group chat between a set of users for a scheduled meeting. You can specify either **meetingChatTab** or **meetingDetailsTab** to ensure the apps work in mobile. |
| **meetingDetailsTab** | A tab in the header of the meeting details view of the calendar. You can specify either **meetingChatTab** or **meetingDetailsTab** to ensure the apps work in mobile. |
| **meetingSidePanel** | An in-meeting panel opened through the unified bar (U-bar). |
| **meetingStage** | An app from the `meetingSidePanel` can be shared to the meeting stage. You can't use this app either on mobile or Teams room clients. |

After you enable your app for Teams meetings, you must configure your app before a meeting, during a meeting, and after a meeting.

## Configure your app for meeting scenarios

Teams meetings provide a collaborative experience for your organization. Configure your app for different meeting scenarios and to enhance the meeting experience. Now you can identify what actions can be taken in the following meeting scenarios:

* [Before a meeting](#before-a-meeting)
* [During a meeting](#during-a-meeting)
* [After a meeting](#after-a-meeting)

### Before a meeting

Before a meeting, users can add tabs, bots, and message extensions. Users with organizer and presenter roles can add tabs to a meeting.

To add a tab to a meeting:

1. In your calendar, select a meeting to which you want to add a tab.
1. Select the **Details** tab and select :::image type="icon" source="../assets/images/apps-in-meetings/plusbutton.png":::

   :::image type="content" source="../assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="Screenshot showing the navigation to + option in the UI.":::

1. In the tab gallery that appears, select the app that you want to add and follow the steps as required. The app is installed as a tab.

To add a message extension to a meeting:

1. Select the ellipses &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.
1. Select the app that you want to add and follow the steps as required. The app is installed as a message extension.

To add a bot to a meeting:

In a meeting chat, enter the **@** key and select **Get bots**.

> [!NOTE]
>
> * The in-meeting dialog displays a dialog in a meeting and simultaneously posts an Adaptive Card in the meeting chat that users can access. The Adaptive Card in the meeting chat helps users while attending the meeting or if the Teams app is minimized.
> * The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/tab-sso-overview.md). After authentication, the app can retrieve the user role using the `GetParticipant` API.
> * Based on the user role, the app has the capability to provide role specific experiences. For example, a polling app allows only organizers and presenters to create a new poll.
> * Role assignments can be changed while a meeting is in progress. For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### During a meeting

During a meeting, you can use the `meetingSidePanel` or in-meeting notification to build unique experiences for your apps.

#### Meeting SidePanel

The `meetingSidePanel` enables you to customize experiences in a meeting that allow organizers and presenters to have different set of views and actions. In your app manifest, you must add `meetingSidePanel` to the context array. In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width. For more information, see [FrameInfo interface](/javascript/api/@microsoft/teams-js/frameinfo) (known as `FrameContext` prior to TeamsJS v.2.0.0).

You can [use the user's context to route requests](../tabs/how-to/access-teams-context.md#user-context). For more information, see [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md). Authentication flow for tabs is similar to the authentication flow for websites. Tabs can use OAuth 2.0 directly. For more information, see [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

Message extension works as expected when a user is in an in-meeting view. The user can post compose message extension cards. AppName in-meeting is a tooltip that states the app name in-meeting U-bar.

> [!NOTE]
> Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.

#### In-meeting notification

The in-meeting notification is used to engage participants during the meeting and collect information or feedback during the meeting. Use an [in-meeting notification payload](API-references.md#send-an-in-meeting-notification) to trigger an in-meeting notification. As part of the notification request payload, include the URL where the content to be shown is hosted.

In-meeting notification must not use task module. Task module isn't invoked in a meeting chat. An external resource URL is used to display in-meeting notification. You can use the `submitTask` method to submit data in a meeting chat.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="Example shows how you can use an in-meeting dialog.":::

You can also add the Teams display picture and people card of the user to in-meeting notification based on `onBehalfOf` token with user MRI and display name passed in payload. Following is an example payload:

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="Example shows how Teams display picture and people card is used with in-meeting dialog." border="true":::

#### Shared meeting stage

Shared meeting stage allows meeting participants to interact with and collaborate on app content in real time. You can share your apps to the collaborative meeting stage in the following ways:

* [Share entire app to stage](#share-entire-app-to-stage) using the share to stage button in the meeting side panel of Teams client or through[[deep links](#generate-a-deep-link-to-share-content-to-stage-in-meetings).
* [Share specific parts of the app to stage](#share-specific-parts-of-the-app-to-stage) using APIs in the Teams client SDK.

##### Share entire app to stage

Participants can share the entire app to the collaborative meeting stage using the share to stage button from the app side panel.

:::image type="content" source="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt-text="Screenshot is an example of showing the meeting stage using the share to stage button from the app side panel.":::

To share the entire app to stage, in the app manifest you must configure `meetingStage` and `meetingSidePanel` as frame contexts. For example:

```json
"configurableTabs": [
   {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
         "groupchat"
        ],
      "context":[
         "meetingSidePanel",
         "meetingStage"
        ]
    }
]
```

For more information, see [app manifest](../resources/schema/manifest-schema-dev-preview.md#configurabletabs).

##### Share specific parts of the app to stage

Participants can share specific parts of the app to the collaborative meeting stage by using the share to stage APIs. The APIs are available within the Teams client SDK and are invoked from the app side panel.

:::image type="content" source="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt-text="The screenshot describes how to share specific part of the app to meeting stage in Teams meeting.":::

To share specific parts of the app to stage, you must invoke the related APIs in the Teams client SDK library. For more information, see [API reference](API-references.md).

> [!NOTE]
>
> * To share specific parts of the app to stage, use Teams manifest version 1.12 or later.
> * You can share specific parts of the app to meeting stage only on Teams desktop clients. Mobile users can share specific parts of the app to stage using the [share to stage API](API-references.md#share-app-content-to-stage-api).

### After a meeting

The configurations of after and [before meetings](#before-a-meeting) are the same.

## Generate a deep link to share content to stage in meetings

You can also generate a deep link to [share the app to stage](#share-entire-app-to-stage) and start or join a meeting.

> [!NOTE]
>
> * Currently, the deep link to share content to stage in meetings is undergoing UX improvements and is available only in [public developer preview](~/resources/dev-preview/developer-preview-intro.md).
> * Deep link to share content to stage in meeting is supported in Teams desktop client only.

When a deep link is selected in an app by a user who is part of an ongoing meeting, then the app is shared to the stage and a permission pop-up window appears. Users can grant access to the participants to collaborate with an app.

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="The screenshot is an example that shows a permission pop-up window.":::

When a user isn't in a meeting then the user is redirected to the Teams calendar where they can join a meeting or initiate instant meeting (Meet now).

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="The screenshot is an example that shows a pop-up window when there's no ongoing meeting.":::

Once the user initiates an instant meeting (Meet now), they can add participants and interact with the app.

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="The screenshot is an example that shows an option to add participants and how to interact with the app.":::

To add a deep link to share content on stage, you need to have an app context. The app context allows the Teams client to fetch the app manifest and check if the sharing on stage is possible. The following is an example of an app context.

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

The query parameters for the app context are:

* `appID`: This is the ID that can be obtained from the app manifest.
* `appSharingUrl`: The URL which needs to be shared on stage should be a valid domain defined in the app manifest. If the URL is not a valid domain, an error dialog will pop-up to provide the user with a description of the error.
* `useMeetNow`: This includes a boolean parameter that can be either true or false.
  * **True**: When the `UseMeetNow` value is true and if there's no ongoing meeting, a new Meet now meeting will be initiated. When there's an ongoing meeting, this value will be ignored.

  * **False**: The default value of `UseMeetNow` is false, which means that when a deep link is shared to stage and there's no ongoing meeting, a calendar pop-up will appear. However, you can share directly during a meeting.

Ensure that all the query parameters are properly URI encoded and the app context has to be encoded twice in the final URL. Following is an example.

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

A deep link can be launched either from the Teams web or from the Teams desktop client.

* **Teams web**: Use the following format to launch a deep link from the Teams web to share content on stage.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Example: `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Deep link|Format|Example|
    |---------|---------|---------|
    |To share the app and open Teams calendar, when UseMeeetNow is **false**, default.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |To share the app and initiate instant meeting, when UseMeeetNow is **true**.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Team desktop client**: Use the following format to launch a deep link from the Teams desktop client to share content on stage.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Example: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Deep link|Format|Example|
    |---------|---------|---------|
    |To share the app and open Teams calendar, when UseMeeetNow is **false**, default.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |To share the app and initiate instant meeting, when UseMeeetNow is **true**.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

The query parameters are:

* `deepLinkId`: Any identifier used for telemetry correlation.
* `fqdn`: `fqdn` is an optional parameter, which can be used to switch to an appropriate environment of a meeting to share an app on stage. It supports scenarios where a specific app share happens in a particular environment. The default value of `fqdn` is enterprise URL and possible values are `Teams.live.com` for Teams for Life, `teams.microsoft.com`, or `teams.microsoft.us`.

To share the entire app to stage, in the app manifest, you must configure `meetingStage` and `meetingSidePanel` as frame contexts, see [app manifest](../resources/schema/manifest-schema.md). Otherwise, meeting attendees may not be able to see the content on stage.

> [!NOTE]
> For your app to pass validation, when you create a deep link from your website, web app, or Adaptive Card, use **Share in meeting** as the string or copy.

## Code sample

|Sample name | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Meeting app | Demonstrates how to use the Meeting Token Generator app to request a token. The token is generated sequentially so that each participant has a fair opportunity to contribute in a meeting. The token is useful in situations like scrum meetings and Q&A sessions. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|Meeting stage sample | Sample app to show a tab in meeting stage for collaboration | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|Meeting side panel | Sample app to show how to add agenda in a meeting side panel | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## Step-by-step guides

* Follow the [step-by-step guide](../sbs-meeting-token-generator.yml) to generate meeting token in your Teams meeting.
* Follow the [step-by-step guide](../sbs-meetings-sidepanel.yml) to generate meeting sidepanel in your Teams meeting.
* Follow the [step-by-step guide](../sbs-meetings-stage-view.yml) to share meeting stage view in your Teams meeting.
* Follow the [step-by-step guide](../sbs-meeting-content-bubble.yml) to generate meeting content bubble in your Teams meeting.

## Next step

> [!div class="nextstepaction"]
> [Meeting apps API references](API-references.md)

## See also

* [In-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md)
* [Shared meeting stage experience design guidelines](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Add apps to meetings via Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
