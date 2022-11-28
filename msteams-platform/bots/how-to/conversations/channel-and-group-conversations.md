---
title: Create conversation bots for channel or group chat
author: surbhigupta
description: Learn how to create new conversation threads, work on mentions, and send message on install. Explore Teams file upload sample (.NET, JavaScript, Python).
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
---
# Channel and group chat conversations with a bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

To install the Microsoft Teams bot in a team or group chat, add the `teams` or `groupchat` scope to your bot. This allows all members of the conversation to interact with your bot. After the bot is installed, it has access to metadata about the conversation, such as the list of conversation members. Also, when it's installed in a team, the bot has access to details about that team and the full list of channels.

Bots in a group or channel only receive messages when they're mentioned @botname. They don't receive any other messages sent to the conversation. The bot must be @mentioned directly. Your bot doesn't receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.

> [!NOTE]
> This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.
>
> Using resource-specific consent (RSC), bots can receive all channel messages in teams that it's installed in without being @mentioned. For more information, see [receive all channel messages with RSC](channel-messages-with-rsc.md).
>
> Posting a message or Adaptive Card to a private channel is currently not supported.

See the following video to learn about channel and group chat conversations with a bot:
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4NzEs]
<br>

## Design guidelines

Unlike personal chats, in group chats and channels, your bot must provide a quick introduction. You must follow these and more bot design guidelines. For more information on how to design bots in Teams, see [how to design bot conversations in channels and chats](~/bots/design/bots.md).

Now, you can create new conversation threads and easily manage different conversations in channels.

## Create new conversation threads

When your bot is installed in a team, you must create a new conversation thread rather than reply to an existing one. At times, it's difficult to differentiate between two conversations. If the conversation is threaded, it's easier to organize and manage different conversations in channels. This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).

Next, you can retrieve mentions using the `entities` object and add mentions to your messages using the `Mention` object.

## Work with mentions

Every message to your bot from a group or channel contains an @mention with its name in the message text. Your bot can also retrieve other users mentioned in a message and add mentions to any messages it sends.

You must also strip out the @mentions from the content of the message your bot receives.

### Retrieve mentions

Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and the name of the user mentioned. The text of the message also includes the mention, such as `<at>@John Smith<at>`. However, don't rely on the text in the message to retrieve any information about the user. It's possible for the person sending the message to alter it. Therefore, use the `entities` object.

You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK, which returns an array of `Mention` objects.

The following code shows an example of retrieving mentions:

# [C#](#tab/dotnet)

* [SDK reference](https://learn.microsoft.com/en-us/dotnet/api/microsoft.bot.builder.activityhandler.onmessageactivityasync?view=botbuilder-dotnet-stable)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-token-app/csharp/Bots/TokenBot.cs#L52)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    // Resolves the mentions from the entities activity.
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        // Sends a message activity to the sender of the incoming activity.
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        // Sends a message activity to the sender of the incoming activity.
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# [TypeScript](#tab/typescript)

* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-localization/nodejs/server/bot/botActivityHandler.js#L25)

```typescript
this.onMessage(async (turnContext, next) => {
    // Resolves the mentions from the entities activity.
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        // Sends a message activity to the sender of the incoming activity.
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        // Sends a message activity to the sender of the incoming activity.
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});

```

# [JSON](#tab/json)

* [SDK reference](https://learn.microsoft.com/en-us/microsoftteams/platform/resources/bot-v3/bot-conversations/bots-conv-channel#example-outgoing-message-with-user-mentioned)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# [Python](#tab/python)

```python
@staticmethod
// Resolves the mentions from the entities of this activity.
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### Add mentions to your messages

Your bot can mention other users in messages posted into channels.

The `Mention` object has two properties that you must set using the following:

* Include *@username* in the message text.
* Include the mention object inside the entities collection.

The Bot Framework SDK provides helper methods and objects to create mentions.

The following code shows an example of adding mentions to your messages:

# [C#](#tab/dotnet)

* [SDK reference](https://learn.microsoft.com/en-us/dotnet/api/microsoft.bot.builder.activityhandler.onmessageactivityasync?view=botbuilder-dotnet-stable)
* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/bot-conversation/csharp/Bots/TeamsConversationBot.cs#L38)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };
    // Returns a simple text message.
    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };
    // Sends an activity to the sender of the incoming activity.
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

```

# [TypeScript](#tab/typescript)

* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-localization/nodejs/server/bot/botActivityHandler.js#L25)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;
    // Returns a simple text message.
    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    // Sends a message activity to the sender of the incoming activity.
    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});

```

# [JSON](#tab/json)

The `text` field in the object in the `entities` array must match a portion of the message `text` field. If it doesn't, the mention is ignored.

* [SDK reference](https://learn.microsoft.com/en-us/microsoftteams/platform/resources/bot-v3/bot-conversations/bots-conv-channel#example-outgoing-message-with-user-mentioned)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# [Python](#tab/python)

* [Sample code reference](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/bot-conversation/python/bots/teams_conversation_bot.py#L29)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )
        // Returns a simple text message.
        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        // Sends a message activity to the sender of the incoming activity.
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

Now you can send an introduction message when your bot is first installed or added to a group or team.

## Send a message on installation

When your bot is first added to the group or team, an introduction message must be sent. The message must provide a brief description of the bot's features and how to use them. You must subscribe to the `conversationUpdate` event with the `teamMemberAdded` eventType.  The event is sent when any new team member is added. Check if the new member added is the bot. For more information, see [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).

You can send a personal message to each member of the team when the bot is added. To do this, [fetch the team roster](../../../resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](../../../resources/bot-v3/bot-conversations/bots-conv-proactive.md).

>[!NOTE]
> Ensure that the message sent by the bot is relevant and adds value to the initial message and doesn't spam the users.

Don't send a message in the following cases:

* When the team is large, for example, larger than 100 members. Your bot can be seen as spam and the person who added it can get complaints. You must clearly communicate your bot's value proposition to everyone who sees the welcome message.
* Your bot is first mentioned in a group or channel instead of being first added to a team.
* A group or channel is renamed.
* A team member is added to a group or channel.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## Step-by-step guide

Follow the [step-by-step guide](../../../sbs-teams-conversation-bot.yml), create Teams conversation bot.

## Next step

> [!div class="nextstepaction"]
> [Subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## See also

* [Get Teams context](~/bots/how-to/get-teams-context.md)
* [Create private channel on behalf of user](/graph/api/channel-post#example-2-create-private-channel-on-behalf-of-user)
* [Connect a bot to Web Chat channel](/azure/bot-service/bot-service-channel-connect-webchat)
