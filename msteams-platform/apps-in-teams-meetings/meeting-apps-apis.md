---
title: Meeting apps APIs
author: v-sdhakshina
description: Learn meeting apps API references that are available for Teams client and Bot Framework SDKs with examples, code samples, and response codes.
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
---

# Meeting apps APIs

The meeting extensibility provides APIs to enhance meeting experience. You can perform the following with help of the listed APIs:

* Build apps or integrate existing apps within meeting lifecycle.
* Use APIs to make your app aware of meeting.
* Select required APIs to improve the meeting experience.

> [!NOTE]
> Use Teams [Microsoft Teams JavaScript client library (TeamsJS)](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) (*Version*: 1.10 and later) for SSO to work in meeting side panel.

The following table provides a list of APIs available across the Microsoft Teams JavaScript library and Microsoft Bot Framework SDKs:

|Method| Description| Source|
|---|---|----|
|[**Get user context**](#get-user-context-api)| Get contextual information to display relevant content in a Microsoft Teams tab.| [Microsoft Teams JavaScript client library](/microsoftteams/platform/tabs/how-to/access-teams-context#get-context-by-using-the-microsoft-teams-javascript-library) |
|[**Get participant**](#get-participant-api)| Fetch participant information by meeting ID and participant ID. | [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetingparticipantasync?view=botbuilder-dotnet-stable&preserve-view=true)
|[**Send in-meeting notification**](#send-an-in-meeting-notification)| Provide meeting signals using the existing conversation notification API for user-bot chat and allows to notify user action that shows an in-meeting notification. | [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityextensions.teamsnotifyuser?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Get meeting details**](#get-meeting-details-api)| Get a meeting's static metadata. | [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetinginfoasync?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Send real-time captions**](#send-real-time-captions-api)| Send real-time captions to an ongoing meeting. | [Microsoft Teams JavaScript client library](/azure/cognitive-services/speech-service/speech-sdk?tabs=nodejs%2Cubuntu%2Cios-xcode%2Cmac-xcode%2Candroid-studio#get-the-speech-sdk&preserve-view=true) |
|[**Share app content to stage**](build-apps-for-teams-meeting-stage.md#share-app-content-to-stage-api)| Share specific parts of the app to meeting stage from the app side panel in a meeting. | [Microsoft Teams JavaScript client library](/javascript/api/@microsoft/teams-js/meeting) |
|[**Get real-time Teams meeting events**](#get-real-time-teams-meeting-events-api)|Fetch real-time meeting events, such as actual start and end time.| [Microsoft Bot Framework SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable&preserve-view=true) |
| [**Get incoming audio state**](#get-incoming-audio-state) | Allows an app to get the incoming audio state setting for the meeting user.| [Microsoft Teams JavaScript client library](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |
| [**Toggle incoming audio**](#toggle-incoming-audio) | Allows an app to toggle the incoming audio state setting for the meeting user from mute to unmute or vice-versa.| [Microsoft Teams JavaScript client library](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |
|[Targeted in-meeting notification API](#targeted-in-meeting-notification-api) | Targeted in-meeting notification allows you to send notification to specific participants during the meeting. | [Microsoft Bot Framework SDK ](Work in progress.) |

## Get user context API

To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab running in the meeting context and is added for the response payload.

## Get participant API

The `GetParticipant` API must have a bot registration and ID to generate auth tokens. For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).

> [!NOTE]
>
> * The user type is not included in the **getParticipantRole** API.
> * Do not cache participant roles since the meeting organizer can change the roles any time.
> * Currently, the `GetParticipant` API is only supported for distributions lists or rosters with less than 350 participants.

### Query parameters

> [!TIP]
> Get participant IDs and tenant IDs from the [tab SSO authentication](../tabs/how-to/authentication/tab-sso-overview.md).

The `Meeting` API must have `meetingId`, `participantId`, and `tenantId` as URL parameters. The parameters are available as part of the Microsoft Teams JavaScript client library (TeamsJS) library and bot activity.

The following table includes the query parameters:

|Value|Type|Required|Description|
|---|---|----|---|
|**meetingId**| String | Yes | The meeting identifier is available through Bot Invoke and TeamsJS library.|
|**participantId**| String | Yes | The participant ID is the user ID. It's available in Tab SSO, Bot Invoke, and TeamsJS library. It's recommended to get a participant ID from the Tab SSO. |
|**tenantId**| String | Yes | The tenant ID is required for the tenant users. It's available in Tab SSO, Bot Invoke, and TeamsJS library. It's recommended to get a tenant ID from the Tab SSO. |

### Example

# [C#](#tab/dotnet)

* [SDK reference](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetingparticipantasync?view=botbuilder-dotnet-stable&preserve-view=true)  
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-context-app/csharp/MeetingContextApp/Bots/MeetingContextBot.cs#L33)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  // Gets the details for the given meeting participant. 
  // This only works in Teams meeting scoped conversations.
  TeamsMeetingParticipant participant = await TeamsInfo.GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourParticipantTenantId").ConfigureAwait(false);
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  // Sends a message activity to the sender of the incoming activity. 
  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}
```

# [JavaScript](#tab/javascript)

* [SDK reference](/javascript/api/botbuilder/teamsinfo?view=botbuilder-ts-latest#botbuilder-teamsinfo-getmeetingparticipant&preserve-view=true)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-token-app/nodejs/server/bot/botActivityHandler.js#L30)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {

            // getMeetingParticipant : Gets the details for the given meeting participant. 
            // This only works in Teams meeting scoped conversations.
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;

            // Sends a message activity to the sender of the incoming activity. 
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# [JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "conversationType": "groupChat", 
      "isGroup":true
   }
}
```

---

| Property name | Description |
|---|---|
| **user.id** | ID of the user. |
| **user.aadObjectId** | Azure Active Directory object ID of the user. |
| **user.name** | Name of the user. |
| **user.givenName** | First Name of the user.|
| **user.surname** | Last Name of the user. |
| **user.email** | Mail ID of the user. |
| **user.userPrincipalName** | UPN of the user. |
| **user.tenantId** | Azure Active Directory tenant ID. |
| **user.userRole** | Role of the user. For example, 'admin' or 'user'. |
| **meeting.role** | The participant's role in the meeting. For example, 'Organizer' or 'Presenter' or 'Attendee'. |
| **meeting.inMeeting** | The value indicating if the participant is in the meeting. |
| **conversation.id** | The meeting chat ID. |
| **conversation.isGroup** | Boolean indicating whether conversation has more than two participants. |

### Response codes

The following table provides the response codes:

|Response code|Description|
|---|---|
| **403** | Get participant information isn't shared with the app. If the app isn't installed in the meeting, it triggers the error response 403. If the tenant admin disables or blocks the app during live site migration, it triggers the error response 403. |
| **200** | The participant information is successfully retrieved.|
| **401** | The app responds with an invalid token.|
| **404** | The meeting has either expired or participants aren't available.|

## Send an in-meeting notification

All users in a meeting receive the notifications sent through in-meeting notification payload. In-meeting notification payload triggers an in-meeting notification and enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat. You can send an in-meeting notification based on user action. The payload is available through Bot Services.

You can also send targeted in-meeting notification to a specific participant in a meeting. For more information, see [Targeted in-meeting notification](in-meeting-notification-for-meeting.md#targeted-in-meeting-notification).

> [!NOTE]
>
> * When an in-meeting notification is invoked, the content is presented as a chat message.
> * You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web view. This is a requirement for app submission. For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * If you want your app to support anonymous users, initial invoke request payload must rely on `from.id` request metadata in `from` object, not `from.aadObjectId` request metadata. `from.id` is the user ID and `from.aadObjectId` is the Microsoft Azure Active Directory (Azure AD) ID of the user. For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### Query parameter

The following table includes the query parameter:

|Value|Type|Required|Description|
|---|---|----|---|
|**conversationId**| String | Yes | The conversation identifier is available as part of Bot Invoke. |

### Examples

`Bot ID` is declared in the manifest and the bot receives a result object.

> [!NOTE]
>
> * The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.
> * The `externalResourceUrl` width and height parameters must be in pixels. For more information, see [design guidelines](design/designing-apps-in-meetings.md).
> * The URL is the page, which loads as `<iframe>` in the in-meeting notification. The domain must be in the apps' `validDomains` array in your app manifest.

# [C#](#tab/dotnet)

* [SDK reference](/dotnet/api/microsoft.bot.builder.teams.teamsactivityextensions.teamsnotifyuser?view=botbuilder-dotnet-stable#microsoft-bot-builder-teams-teamsactivityextensions-teamsnotifyuser(microsoft-bot-schema-iactivity)&preserve-view=true)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/bot-proactive-messaging/csharp/proactive-cmd/Program.cs#L178)

```csharp
// Specifies the type of text data in a message attachment.
Activity activity = MessageFactory.Text("This is a meeting signal test");

// Configures the current activity to generate a notification within Teams.
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");

// Sends a message activity to the sender of the incoming activity. 
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# [JavaScript](#tab/javascript)

* [SDK reference](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#botbuilder-core-turncontext-sendactivity&preserve-view=true)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/bot-conversation/nodejs/bots/teamsConversationBot.js#L74)

```javascript
// MessageFactory.text(): Specifies the type of text data in a message attachment.
const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};

// Sends a message activity to the sender of the incoming activity.
await context.sendActivity(replyActivity);
```

# [JSON](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities
```

```json
// In-meeting notification response
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&<completionBotId>=<BOT_APP_ID>"
        }
    },
    "replyToId": "1493070356924"
}
```

---

| Property name | Description |
|---|---|
| **type** | Type of activity. |
| **text** | The text content of the message. |
| **summary** | The summary text of the message. |
| **channelData.notification.alertInMeeting** | Boolean indicating if a notification is to be shown to the user while in a meeting. |
| **channelData.notification.externalResourceUrl** | The value of the notification's external resource URL.|
| **replyToId** | The ID of the parent or root message of the thread. |
| **APP_ID** | App Id declared in manifest. |
| **completionBotId** | Bot app Id |

### Response codes

The following table includes the response codes:

|Response code|Description|
|---|---|
| **201** | The activity with signal is successfully sent. |
| **401** | The app responds with an invalid token. |
| **403** | The app is unable to send the signal. 403 response code can occur because of various reasons, such as the tenant admin disables and blocks the app during live site migration. In this case, the payload contains a detailed error message. |
| **404** | The meeting chat doesn't exist. |

## Targeted in-meeting notification API

The `targetedMeetingNotification` API allows apps to send notifications to specific participants in a meeting. Apps send targeted in-meeting notifications based on user action. The API is available through bot API.

> [!NOTE]
>
> * The API payload only permits a task module with a URL.
> * The user ID formats **aadObjectid** and **UPN** aren't supported.

Get supported user ID format for targeted in-meeting notification:

* [Get participant API](#get-participant-api)
* [Get members API](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)

### Example

Following is an example of request payload:

```http
GET POST /v1/meetings/{meetingId}/notification
```

```json
{

  "type": "targetedMeetingNotification",
  "value": {
    "recipients": [ 
"29:1I12M_iy2wTa97T6LbjTh4rJCWrtw2PZ3lxpD3yFv8j2YPnweY2lpCPPAn3RI0PP7rghfHauUz48I1t7ANhj4CA"
     ], 
    "surfaces": [ 
      { 
        "surface": "meetingStage", 
        "contentType": "task", 
        "content": { 
          "value": { 
            "height": "300", 
            "width": "400", 
            "title": "Targeted meeting Notification", 
            "url": "https://somevalidurl.com"           
}
        } 
      } 
    ] 
  },
  "channelData": { // optional if a developer doesn't want to support user attributes.
    "onBehalfOf": [ 
      { 
        "itemid": 0, 
        "mentionType": "person", 
        "mri": "29:1mDOCfGM9825lMHlwP8NjIVMJeQAbN-ojYBT5VzQfPpnst1IFQeYB1QXC8Zupn2RhgfLIW27HmynQk-4bdx_YhA", 
        "displayName": "yunny chung"      } 
    ] 
  }
}
```

| Property name | Description |
|---|---|
| `meetingId` | The meeting ID is available through bot invoke and TeamsJS library. |
| `type` |`targetedMeetingNotification` |
| `recipients` | List of user IDs. Get user IDs for meeting participants through [Get participant API](#get-participant-api). Get the entire list of chat roster using [Get members API](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile). Empty or null recipients list will return 400.|
| `surface` | `meetingStage` keyword. |
| `contentType` | `task` keyword. |
| `onBehalfOf.itemid` | Describes identification of the item. Its value must be 0. **Optional**. |
| `onBehalfOf.mentionType` | `person` keyword. Describes the mention of a person. **Optional**.|
| `onBehalfOf.mri` | User MRI shown as sender. **Optional**. |

Following are the optional properties:

| Property name | Description |
|---|---|
| `content.value.title` | Title of the notification. |
| `content.value.width` | Requested width of the notification. |
| `content.value.height` | Requested height of the notification. |
| `content.value.url` | URL to be rendered in the notification. Make sure the URL is part of `validDomains` in app manifest. If empty string or no URL is provided, nothing will be rendered on a meeting notification. |
| `ChannelData.OnBehalfOf` | This is to support [User attributes](../messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md#user-attribution-for-bots-messages). |
| `onBehalfOf.displayName` | Name of the `person`. Used as fallback in case the name resolution is unavailable. |

### Response code

The following table includes the response codes:

| Response code | Description |
|---|---|
| **202** | Notification is successfully sent. |
| **207** | Notifications are sent only to a few participants. |
| **400** | Meeting notification request payload validation failed. |
| **401** | Bot token is invalid. |
| **403** | Bot is not allowed to send the notification. |
| **404** | Meeting chat is not found or none of the participants were found in the roster. |

## Get meeting details API

The Meeting Details API enables your app to get a meeting's static metadata. The metadata provides data points that don't change dynamically. The API is available through Bot Services. Currently, both private scheduled or recurring meetings and channel scheduled or recurring meetings support API with different RSC permissions respectively.

The `Meeting Details` API must have a bot registration and bot ID. It requires Bot SDK to get `TurnContext`. To use the Meeting Details API, you must obtain different RSC permission based on the scope of any meeting, such as private meeting or channel meeting.

### Prerequisite

To use the Meeting Details API, you must obtain different RSC permission based on the scope of any meeting, such as private meeting or channel meeting.

<br>

<details>

<summary><b>For app manifest version 1.12 and later</b></summary>

Use the following example to configure your app manifest's `webApplicationInfo`  and `authorization` properties for any private meeting:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]
    }
}
 ```

Use the following example to configure your app manifest's `webApplicationInfo` and `authorization` properties for any channel meeting:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChannelMeeting.ReadBasic.Group",
                "type": "Application"
            }
        ]
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>For app manifest version 1.11 and earlier</b></summary>

Use the following example to configure your app manifest's `webApplicationInfo` property for any private meeting:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

Use the following example to configure your app manifest's `webApplicationInfo` property for any channel meeting:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "ChannelMeeting.ReadBasic.Group"
    ]
}
 ```

<br>

</details>

> [!NOTE]
>
> * The bot can receive meeting start or end events automatically from all the meetings created in all the channels by adding `ChannelMeeting.ReadBasic.Group` to manifest for RSC permission.
> * For a one-on-one call `organizer` is the initiator of the chat and for group calls `organizer` is the call initiator. For public channel meetings `organizer` is the person who created the channel post.

### Query parameter

The following table lists the query parameter:

|Value|Type|Required|Description|
|---|---|----|---|
|**meetingId**| String | Yes | The meeting identifier is available through Bot Invoke and Microsoft Teams JavaScript client library library. |

### Example

# [C#](#tab/dotnet)

* [SDK reference](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetinginfoasync?view=botbuilder-dotnet-stable#microsoft-bot-builder-teams-teamsinfo-getmeetinginfoasync(microsoft-bot-builder-iturncontext-system-string-system-threading-cancellationtoken)&preserve-view=true)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/graph-meeting-notification/csharp/MeetingNotification/Bots/MeetingNotificationBot.cs#L56)

```csharp
// Gets the information for the given meeting id.
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);

// Sends a message activity to the sender of the incoming activity. 
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# [JavaScript](#tab/javascript)

```javascript

Not available

```

# [JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

The JSON response body for Meeting Details API is as follows:

* **Scheduled meetings:**

    ```json

    {
       "details":  { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "Scheduled" 
         },
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
             }, 
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    } 
    ```

* **Scheduled channel meetings:**

    ```json
    { 
        "details": { 
        "msGraphResourceId": "MSoxNmUwYjdiYi05M2Q1LTQzNTItOTllMC0yM2VlNWYyZmZmZTIqMTY2MDc1ODYwNzc0MCoqMTk6a0RtQkpEWFZsYWl0QWhHcVB2SzBtRExZbHVTWnJub01WX1MxeFNkTjQxNDFAdGhyZWFkLnRhY3Yy", 
        "scheduledStartTime": "2022-08-17T18:00:00Z", 
        "scheduledEndTime": "2022-08-17T18:30:00Z", 
        "type": "ChannelScheduled", 
        "id": "MCMxOTprRG1CSkRYVmxhaXRBaEdxUHZLMG1ETFlsdVNacm5vTVZfUzF4U2RONDE0MUB0aHJlYWQudGFjdjIjMTY2MDc1ODYwNzc0MA==", 
        "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3akDmBJDXVlaitAhGqPvK0mDLYluSZrnoMV_S1xSdN4141%40thread.tacv2/1660758607740?context=%7b%22Tid%22%3a%229f044231-b634-4bdd-b29d-2776e3dbd699%22%2c%22Oid%22%3a%2216e0b7bb-93d5-4352-99e0-23ee5f2fffe2%22%7d", 
        "title": "Test channel meeting"
    }, 
    "conversation": { 
        "isGroup": true, 
        "conversationType": "channel", 
        "id": "19:kDmBJDXVlaitAhGqPvK0mDLYluSZrnoMV_S1xSdN4141@thread.tacv2;messageid=1660758607740"
    }, 
    "organizer": { 
        "tenantId": "9f044231-b634-4bdd-b29d-2776e3dbd699", 
        "objectId": "16e0b7bb-93d5-4352-99e0-23ee5f2fffe2", 
        "id": "29:1q4D6ekLXEAALkrqyLXUIcwtVSdXx31bf6vMdfahmkTb9euYVYSsN9x4133pXLV_I2idpVriFe40e19XEZt57bQ", 
        "aadObjectId": "16e0b7bb-93d5-4352-99e0-23ee5f2fffe2"
    }
    }
    ```

* **One-on-one calls:**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "OneToOneCall"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer  ": {
             "id": "<organizer user ID>",
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Group calls:**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "GroupCall",
             "joinUrl": "https://teams.microsoft.com/l/xx"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer": {
             "id": "<organizer user ID>",
             "objectId": "<organizer object ID>",
             "aadObjectId": "<AAD object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Instant meetings:**

    ```json
    { 
       "details": { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "MeetNow" 
         }, 
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
         },
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>", 
             "tenantId": "<Tenant ID>" ,
             "objectId": "<organizer object ID>"
         }
    }
    
    ```

---

| Property name | Description |
|---|---|
| **details.id** | The meeting's ID, encoded as a BASE64 string. |
| **details.msGraphResourceId** | The MsGraphResourceId, used specifically for MS Graph API calls. |
| **details.scheduledStartTime** | The meeting's scheduled start time, in UTC. |
| **details.scheduledEndTime** | The meeting's scheduled end time, in UTC. |
| **details.joinUrl** | The URL used to join the meeting. |
| **details.title** | The title of the meeting. |
| **details.type** | The meeting's type (OneToOneCall, GroupCall, Scheduled, Recurring, MeetNow, ChannelScheduled, and ChannelRecurring). |
| **conversation.isGroup** | Boolean indicating whether conversation has more than two participants. |
| **conversation.conversationType** | The conversation type. |
| **conversation.id** | The meeting chat ID. |
| **organizer.id** | The Organizer's user ID. |
| **organizer.aadObjectId** | The Organizer's Azure Active Directory object ID. |
| **organizer.tenantId** | The Organizer's Azure Active Directory tenant ID. |

In case of Recurring meeting type,

**startDate**: Specifies the date to start applying the pattern. The value of startDate must correspond to the date value of the start property on the event resource. Note that the first occurrence of the meeting may not occur on this date if it doesn't fit the pattern.

**endDate**: Specifies the date to stop applying the pattern. Note that the last occurrence of the meeting may not occur on this date if it doesn't fit the pattern.

## Send real-time captions API

The send real-time captions API exposes a POST endpoint for Teams communication access real-time translation (CART) captions, human-typed closed captions. Text content sent to this endpoint appears to end users in a Teams meeting when they have captions enabled.

### CART URL

You can get the CART URL for the POST endpoint from the **Meeting options** page in a Teams meeting. For more information, see [CART captions in a Microsoft Teams meeting](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47). You don't need to modify the CART URL to use CART captions.

#### Query Parameter

The CART URL includes the following query parameters:

|Value|Type|Required|Description|
|---|---|----|----|
|**meetingId**| String | Yes |The meeting identifier is available through Bot Invoke and Microsoft Teams JavaScript client library library. <br/>For example, meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**token**| String | Yes |Authorization token.<br/> For example, token=04751eac |

#### Example

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### Method

|Resource|Method|Description|
|----|----|----|
|/cartcaption|POST|Handle captions for meeting, which was started|

> [!NOTE]
> Ensure that the content type for all requests is plain text with UTF-8 encoding. The body of request contains only captions.

#### Example

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!NOTE]  
> Each POST request generates a new line of captions. To ensure that the end user has enough time to read the content, limit each POST request body to 80-120 characters.

### Error codes

The following table provides the error codes:

|Error code|Description|
|---|---|
| **400** | Bad request. The response body has more information. For example, not of all required parameters presented.|
| **401** | Unauthorized. Bad or expired token. If you receive this error, generate a new CART URL in Teams. |
| **404** | Meeting not found or not started. If you receive this error, ensure that you start the meeting and select start captions. After captions are enabled in the meeting, you can begin POSTing captions into the meeting.|
| **500** |Internal server error. For more information, [contact support or provide feedback](../feedback.md).|

## Get real-time Teams meeting events API

> [!NOTE]
> Real-time Teams meeting events are only supported for scheduled meetings.

The user can receive real-time meeting events. As soon as any app is associated with a meeting, the actual meeting start and end time are shared with the bot. The actual start and end time of a meeting are different from scheduled start and end time. The Meeting Details API provides the scheduled start and end time. The event provides the actual start and end time.

You must be familiar with the `TurnContext` object available through the Bot SDK. The `Activity` object in `TurnContext` contains the payload with the actual start and end time. Real-time meeting events require a registered bot ID from the Teams platform. The bot can automatically receive meeting start or end event by adding `ChannelMeeting.ReadBasic.Group` in the manifest.

### Prerequisite

Your app manifest must have the `webApplicationInfo` property to receive the meeting start and end events. Use the following examples to configure your manifest:

<br>

<details>

<summary><b>For app manifest version 1.12 and later</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]    
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>For app manifest version 1.11 and earlier</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

<br>

</details>

### Example of getting `MeetingStartEndEventvalue`

The bot receives event through the `OnEventActivityAsync` handler. To deserialize the JSON payload, a model object is introduced to get the metadata of a meeting. The metadata of a meeting is in the `value` property in the event payload. The `MeetingStartEndEventvalue` model object is created, whose member variables correspond to the keys under the `value` property in the event payload.

> [!NOTE]
>
> * Get meeting ID from `turnContext.ChannelData`.
> * Do not use conversation ID as meeting ID.
> * Do not use meeting ID from meeting events payload `turncontext.activity.value`.

The following code shows how to capture the metadata of a meeting that is `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime`, and `EndTime` from a meeting start/end event:

Meeting Start Event

* [SDK reference](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable#microsoft-bot-builder-teams-teamsactivityhandler-onteamsmeetingstartasync(microsoft-bot-schema-teams-meetingstarteventdetails-microsoft-bot-builder-iturncontext((microsoft-bot-schema-ieventactivity))-system-threading-cancellationtoken)&preserve-view=true)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-events/csharp/MeetingEvents/Bots/ActivityBot.cs#L34)

* [SDK reference](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable#microsoft-bot-builder-teams-teamsactivityhandler-onteamsmeetingstartasync(microsoft-bot-schema-teams-meetingstarteventdetails-microsoft-bot-builder-iturncontext((microsoft-bot-schema-ieventactivity))-system-threading-cancellationtoken)&preserve-view=true)

```csharp
// Invoked when a Teams Meeting Start event activity is received from the connector.
protected override async Task OnTeamsMeetingStartAsync(MeetingStartEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Sends a message activity to the sender of the incoming activity. 
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

Meeting End Event

* [SDK reference](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingendasync?view=botbuilder-dotnet-stable#microsoft-bot-builder-teams-teamsactivityhandler-onteamsmeetingendasync(microsoft-bot-schema-teams-meetingendeventdetails-microsoft-bot-builder-iturncontext((microsoft-bot-schema-ieventactivity))-system-threading-cancellationtoken)&preserve-view=true)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-events/csharp/MeetingEvents/Bots/ActivityBot.cs#L51)

* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-events/csharp/MeetingEvents/Bots/ActivityBot.cs#L51)

* [SDK reference](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingendasync?view=botbuilder-dotnet-stable#microsoft-bot-builder-teams-teamsactivityhandler-onteamsmeetingendasync(microsoft-bot-schema-teams-meetingendeventdetails-microsoft-bot-builder-iturncontext((microsoft-bot-schema-ieventactivity))-system-threading-cancellationtoken)&preserve-view=true)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-events/csharp/MeetingEvents/Bots/ActivityBot.cs#L51)

```csharp
// Invoked when a Teams Meeting End event activity is received from the connector.
protected override async Task OnTeamsMeetingEndAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Sends a message activity to the sender of the incoming activity.
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

### Example of meeting start event payload

The following code provides an example of meeting start event payload:

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id": "meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### Example of meeting end event payload

The following code provides an example of meeting end event payload:

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

| Property name | Description |
|---|---|
| **name** | Name of the user.|
| **type** | Activity type. |
| **timestamp** | Local date and time of the message, expressed in ISO-8601 format. |
| **id** | ID for the activity. |
| **channelId** | Channel this activity is associated with. |
| **serviceUrl** | Service URL where responses to this activity should be sent. |
| **from.id** | ID of the user that sent the request. |
| **from.aadObjectId** | Azure Active Directory object ID of the user that sent the request. |
| **conversation.isGroup** | Boolean indicating whether conversation has more than two participants. |
| **conversation.tenantId** | Azure Active Directory tenant ID of the conversation or meeting. |
| **conversation.id** | The meeting chat ID. |
| **recipient.id** | ID of the user that receive the request. |
| **recipient.name** | Name of the user that receive the request. |
| **entities.locale** | entity which contains metadata about locale. |
| **entities.country** | entity which contains metadata about country. |
| **entities.type** | entity which contains metadata about client. |
| **channelData.tenant.id** | Azure Active Directory tenant ID. |
| **channelData.source** | The source name from where event is fired or invoked. |
| **channelData.meeting.id** | The default ID associated with the meeting. |
| **value.MeetingType** | The type of meeting. |
| **value.Title** | The subject of the meeting. |
| **value.Id** | The default ID associated with the meeting. |
| **value.JoinUrl** | The join URL of the meeting. |
| **value.StartTime** | The meeting start time in UTC. |
| **value.EndTime** | The meeting end time in UTC. |
| **locale**| The locale of the message set by the client. |

## Get incoming audio state

The `getIncomingClientAudioState` API allows an app to get the incoming audio state setting for the meeting user. The API is available through the Microsoft Teams JavaScript client library library.

> [!NOTE]
>
> * The `getIncomingClientAudioState` API for mobile is currently available in [Public Developer Preview](../resources/dev-preview/developer-preview-intro.md).
> * Resource specific consent is available for manifest version 1.12 and later versions, hence this API doesn't work for manifest version 1.11 and earlier versions.

### Manifest

```JSON
"authorization": {
    "permissions": {
      "resourceSpecific": [
        {
          "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
          "type": "Delegated"
        }
      ]
    }
  }
```
  
### Example

```javascript
callback = (errcode, result) => {
        if (errcode) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }
// The getIncomingClientAudioState API shows the current audio state.
microsoftTeams.meeting.getIncomingClientAudioState(this.callback)
```

### Query parameter

The following table includes the query parameter:

|Value|Type|Required|Description|
|---|---|----|---|
|**callback**| String | Yes | Callback contains two parameters `error` and `result`. The *error* can either contain an error type `SdkError` or `null` when the audio fetch is successful. The *result* can either contain true or false value when the audio fetch is successful or null when the audio fetch fails. The incoming audio is muted if the result is true and unmuted if the result is false. |
  
### Response codes

The following table provides the response codes:

|Response code|Description|
|---|---|
| **500** | Internal error. |
| **501** | API isn't supported in the current context.|
| **1000** | App doesn't have proper permissions to allow share to stage.|

## Toggle incoming audio

The `toggleIncomingClientAudio` API allows an app to toggle the incoming audio state setting for the meeting user from mute to unmute or vice-versa. The API is available through the Microsoft Teams JavaScript client library.

> [!NOTE]
>
> * The `toggleIncomingClientAudio` API for mobile is currently available in [Public Developer Preview](../resources/dev-preview/developer-preview-intro.md).
> * Resource specific consent is available for manifest version 1.12 and later versions, hence this API doesn't work for manifest version 1.11 and earlier versions.

### Manifest

```JSON
"authorization": {
 "permissions": {
  "resourceSpecific": [
   {
    "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
    "type": "Delegated"
   }
  ]
 }
}
```

### Example

```javascript
callback = (error, result) => {
        if (error) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }
// The toggleIncomingClientAudio API allows an app to toggle the incoming audio state.
microsoftTeams.meeting.toggleIncomingClientAudio(this.callback)
```
  
### Query parameter

The following table includes the query parameter:

|Value|Type|Required|Description|
|---|---|----|---|
|**callback**| String | Yes | Callback contains two parameters `error` and `result`. The *error* can either contain an error type `SdkError` or `null` when the toggle is successful. The *result* can either contain true or false value, when the toggle is successful or null when the toggle fails. The incoming audio is muted if the result is true and unmuted if the result is false.
  
### Response code

The following table provides the response codes:

|Response code|Description|
|---|---|
| **500** | Internal error. |
| **501** | API isn't supported in the current context.|
| **1000** | App doesn't have proper permissions to allow share to stage.|

## Code sample

|Sample name | Description | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| Meetings extensibility | Teams meeting extensibility sample for passing tokens. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Meeting content bubble bot | Teams meeting extensibility sample for interacting with content bubble bot in a meeting. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Meeting side panel | Teams meeting extensibility sample for interacting with the side panel in-meeting. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Details Tab in Meeting | Teams meeting extensibility sample for interacting with Details Tab in-meeting. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
| Meeting Events Sample | Sample app to show real-time Teams meeting events|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
| Meeting Recruitment Sample |Sample app to show meeting experience for recruitment scenario.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
| App installation using QR code |Sample app that generates the QR code and installs the app using the QR code|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## See also

* [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md)
* [Apps for Teams meetings](teams-apps-in-meetings.md)
* [Live Share SDK](teams-live-share-overview.md)
* [Teams cloud meeting recording](/microsoftteams/cloud-recording)
* [Build in-meeting notification for Teams meeting](in-meeting-notification-for-meeting.md)

## Next step

[Build tabs for meeting](build-tabs-for-meeting.md)

* [Get change notifications for Microsoft Teams meeting call updates](/graph/changenotifications-for-onlinemeeting)
