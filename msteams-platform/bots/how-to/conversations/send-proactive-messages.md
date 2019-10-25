---
title: Send proactive messages
author: clearab
description: How to send proactive messages with your Microsoft Teams bot.
ms.topic: overview
ms.author: anclear
---
# Send proactive messages

<!-- Update -->

A bot may need to send a message to the user that is not an immediate response to an incoming message. These types of messages are called **proactive messages**.  

Proactive messages can be useful in a variety of scenarios. These are some examples:  

- The user previously asked the bot to monitor the price of a product, the bot can alert the user if the price of the product has changed.
- A bot requires some time to compile a response to the user's question, it may inform the user of the delay and allow the conversation to continue in the meantime.

## Best practices for proactive messaging

Sending proactive messages to users can be a very effective way to communicate with your users. However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app. As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.

Proactive messages generally fall into one of two categories, welcome messages or notifications.

### Welcome messages

When receiving a welcome message a users do not have context. Also this is the first time they have interacted with the bot which is an opportunity to create a good first impression. Well structured messages include:

- **Why the users are receiving the message.** It should be very clear to the users why they are receiving the message. If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed and potentially who installed it.
- **What is the offer.** What can they do with your bot? What value it brings?
- **What should they do next.** Invite them to try out a command, or interact with your bot in some way.

### Notification messages

When sending notifications, assure that the users have a clear path to take common actions, and a clear understanding of why the notification ocurred. Well structured messages include:

- **What happened.** A clear indication of what caused the notification.
- **What it happened to.** What item was updated to cause the notification.
- **Who did it.** Who took the action that caused the notification to be sent.
- **What they can do about it.** Make it easy for the users to take actions based on the notification.
- **How they can opt out.** You need to provide a path for users to opt out of additional notifications.

## Obtain necessary user information

Bots can create new conversations with an individual Microsoft Teams user by obtaining the userâ€™s *unique ID* and *tenant ID.* You can obtain these values using one of the following methods:

<!-- WARNING: Verify. Please, verify these links; they point to topics in the _old folder.-->

- By [fetching the team roster](../../../_old/concepts/bots/bots-context.md#fetching-the-team-roster) from a channel your app is installed in.
- By caching them when a user [interacts with your bot in a channel](../../../_old/concepts/bots/bot-conversations/bots-conv-channel.md).
- When a users is [@mentioned in a channel conversation](../../../_old/concepts/bots/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.
- By caching them when you [receive the conversationUpdate](../../../_old/concepts/bots/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat.



### Proactively install your app using Graph

> [!Note]
> Proactively installing apps using graph is currently in beta.

Occasionally it may be necessary to proactively message users that have not installed or interacted with your bot previously. For example, you want to use the [company communicator](../../../samples/app-templates.md#company-communicator) to send messages to your entire organization. For this scenario you can use the Graph API to proactively install your bot for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.

You can only install apps that are in your organizational app catalogue, or the Teams app store.

See [Install apps for users](https://docs.microsoft.com/graph/teams-proactive-messaging) in the Graph documentation for complete details. There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).


## Example

In essence there are two ways to issue proactive messages, in a standalone fashion or in a conversation.

The simplest way to issue a proactive message is standalone, as shown in the example below. For example, when a user is added to a team a bot can issue a proactive message to the the added member via a `SendActivityAsync`.  
 
```cs 
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> membersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  foreach (var member in membersAdded)
  {
      var replyActivity = MessageFactory.Text($"{member.Id} added to the team");
      replyActivity.ApplyConversationReference(turnContext.Activity.GetConversationReference());

      var channelId = turnContext.Activity.Conversation.Id.Split(";")[0];
      replyActivity.Conversation.Id = channelId;
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
  }
}
```

A bot can post into a channel to create a new conversation as shown in the example below. This scenario applies when it is important for the bot to preserve conversation state information and refer to it at some later time.

```cs
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)

{
    var members = await TeamsInfo.GetMembersAsync(turnContext, cancellationToken);
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.Name}. I'm a Teams conversation bot.");
        var connector = turnContext.TurnState.Get<IConnectorClient>();

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };

        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(teamsChannelId, serviceUrl, credentials, conversationParameters, (t, ct) => {
           conversationReference = t.Activity.GetConversationReference();
           return Task.CompletedTask;}, cancellationToken);

        await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(_appId, conversationReference, async (t, ct) => {
          await t.SendActivityAsync(proactiveMessage, ct);}, cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All members have been messaged"), cancellationToken);
}

```

## Additional resources

- [Send proactive notifications to users](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp) - Bot Framework SDK proactive messages explained
- [How bots work](https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&tabs=csharp) - Inside the bots
- [Have a conversation with a Microsoft Teams bot](../../../_old/concepts/bots/bot-conversations/bots-conversations.md) - Conversations and messages in Teams
