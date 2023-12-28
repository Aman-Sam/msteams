---
title: Bot configuration experience
author: surbhigupta
description: Learn about bot configuration experience.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
---

# Bot configuration experience

> [!NOTE]
>
> * Bot configuration experience is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md).
> * Bot configuration experience is supported in channel or group chat scopes only.

You can create a bot to enable the bot configuration settings for the user during the bot installation and also from the channel or group chat scope after the bot is installed.

In the following graphic, the bot is installed in a group chat. When the user hovers over the bot, an Adaptive Card appears. The user can select the settings icon in the Adaptive Card to update or change the bot's configuration settings:

:::image type="content" source="../../assets/images/bots/configurationbot.gif" alt-text="Screenshot shows the configuration option for the bot in a Teams group chat.":::

## Enable bot configuration experience

To enable the bot configuration settings from a channel or group chat scope, follow these steps:

1. [Update app manifest](#update-app-manifest)
1. [Configure your bot](#configure-your-bot)

### Update app manifest

You must configure the `fetchTask` property under `bots.configuration` object in the app manifest (previously called Teams app manifest) file as follows:

```json
"bots": [
    {
      "botId": "${{AAD_APP_CLIENT_ID}}",
     "needsChannelSelector": false,
      "scopes": [
        "personal",
        "team",
        "groupChat"
      ],
      "configuration":{
        "groupChat":{
          "fetchTask": true
        },
        "team":{
          "fetchTask": true
        }
      },
      "isNotificationOnly": false
    }
  ],
```

For more information, see [public developer preview app manifest schema](../../resources/schema/manifest-schema-dev-preview.md#botsconfiguration).

### Configure your bot

You can enable the configuration settings for your bot using `onInvokeActivity` or `OnTeamsConfigFetchAsync` and `OnTeamsConfigSubmitAsync` or `handleTeamsConfigFetch` and `handleTeamsConfigSubmit` methods.

The following table summarizes the methods that are used to enable the bot configuration experience in Teams:

| Method | SDK |
| --- | --- |
| `onInvokeActivity`| Bot Framework SDK for .NET and TypeScript.|
| `OnTeamsConfigFetchAsync` and `OnTeamsConfigSubmitAsync`| Teams Bot SDK for .NET. |
| `handleTeamsConfigFetch` and `handleTeamsConfigSubmit`. | Teams Bot SDK for Node.js and TypeScript. |

When a user installs the bot in a team or group chat scope, the `fetchTask` property in the app manifest file initiates `config/fetch`, `handleTeamsConfigFetch` or `OnTeamsConfigFetchAsync` methods defined in the teamsBot.js file. The bot responds with an Adaptive Card and the user provides relevant information in the Adaptive Card and selects Submit. After the user selects Submit, a `config/submit`, `handleTeamsConfigSubmit`, or `OnTeamsConfigSubmitAsync` is returned to the bot and the bot configuration is complete.

# [Bot Framework JS](#tab/bot-framework-js)

```javascript
if (context._activity.name == "config/submit") {
 
  const choice = context._activity.value.data.choiceselect.split(" ")[0];
  chosenFlow = choice;
  if (choice === "static_option_2") {
      const adaptiveCard = CardFactory.adaptiveCard(this.adaptiveCardForStaticSearch());
 
      return {
          status: 200,
          body: {
              config: {
                  type: 'continue',
                  value: {
                      card: adaptiveCard,
                      height: 400,
                      title: 'Task module submit response',
                      width: 300                  }              }          }      }  }
  else {
 
      try {
          return {
              status: 200,
              body: {
                  config: {
                      type: 'continue',
                      value: {
                          card: adaptiveCard,
                          height: 400,
                          title: 'Dialog fetch response',
                          width: 300
                      }
                  }
              }
          }
      }
 
 
if (context._activity.name == "config/fetch") {
  const adaptiveCard = CardFactory.adaptiveCard(this.adaptiveCardForDynamicSearch());
  try {
      return {
          status: 200,
          body: {
              config: {
                  type: 'continue',
                  value: {
                      card: adaptiveCard,
                      height: 400,
                      title: 'Task module fetch response',
                      width: 300
                  }
              }
          }
      }
  } catch (e) {
      console.log(e);
  }
}
```

# [Teams bot SDK JS](#tab/teams-bot-sdk-js)

The handleTeamsConfigFetch and handleTeamsConfigSubmit handle the fetching and submission of Teams configuration data.

* `handleTeamsConfigFetch`: If the command is 'card', the function sets the response.config object to contain suggested actions and a type of 'auth'. If the command is 'message', the function creates an AdaptiveCard with the text 'Bot Config Fetch' and sets the response.config object to contain the card and a type of 'continue'. The function returns the response object.

* `handleTeamsConfigSubmit`: if the command is 'card', the function creates an AdaptiveCard with the text 'Bot Config Submit' and sets the response.config object to contain the card and a type of 'continue'. If the command is 'message', the function sets the response.config object to contain a value of 'config submit text' and a type of 'message'. The function returns the response object.

```javascript
// extending both handlers
 
    async handleTeamsConfigFetch(_context, configData) {
        let response = {};
        switch (configData.command) {
            case 'card':
                {
                    response.config = {
                        suggestedActions: {
                            actions: [
                                {
                                    type: 'bot config auth',
                                    title: 'bot config title',
                                    image:
                                        'https://static-asm.secure.skypeassets.com/pes/v1/emoticons/win10/views/default_40',
                                    value: 'bot config auth value',
                                },
                            ],
                        },
                        type: 'auth',
                    };
                }
                break;
            case 'message':
                {
                    const cardJson = {
                        type: 'AdaptiveCard',
                        version: '1.4',
 
                        body: [
                            {
                                type: 'TextBlock',
                                text: 'Bot Config Fetch',
                            },
                        ],
                    };
                    const card = CardFactory.adaptiveCard(cardJson);
 
                    response = {
                        config: {
                            value: {
                                height: 200,
                                width: 200,
                                title: 'test card fetch',
                                card,
                            },
                            type: 'continue',
                        },
                    };
                }
                break;
            default:
                console.log('no default');
        }
 
        return response;
    }
 
    async handleTeamsConfigSubmit(_context, configData) {
        let response = {};
        switch (configData.command) {
            case 'card':
                {
                    const cardJson = {
                        type: 'AdaptiveCard',
                        version: '1.4',
 
                        body: [
                            {
                                type: 'TextBlock',
                                text: 'Bot Config Submit',
                            },
                        ],
                    };
                    const card = CardFactory.adaptiveCard(cardJson);
 
                    response = {
                        config: {
                            value: {
                                height: 200,
                                width: 200,
                                title: 'test card submit',
                                card,
                            },
                            type: 'continue',
                        },
                    };
                }
                break;
            case 'message':
                {
                    response = {
                        config: {
                            value: 'config submit text',
                            type: 'message',
                        },
                    };
                }
                break;
            default:
                console.log('no default');
                break;
        }
 
        return response;
    }
```

# [Teams bot SDK C#](#tab/teams-bot-sdk)

When a user installs the bot in a team or group chat scope, the `OnTeamsConfigFetchAsync` method is called. The `OnTeamsConfigSubmitAsync` method is called when the user submits the bot configuration. The methods  return `ConfigResponseBase` object that contain the bot configuration, and can be used to create suggested actions, display messages, and configure the bot’s dialog.

```csharp
 
protected override Task<ConfigResponseBase> OnTeamsConfigFetchAsync(ITurnContext<IInvokeActivity> turnContext, JObject configData, CancellationToken cancellationToken)
{
 
    ConfigResponseBase response = new ConfigResponse<BotConfigAuth>
    {
        Config = new BotConfigAuth
        {
            SuggestedActions = new SuggestedActions
            {
                Actions = new List<CardAction>
                {
                    new CardAction
                    {
                        Type = "bot config type",
                        Title = "bot config title",
                        Image = "https://static-asm.secure.skypeassets.com/pes/v1/emoticons/win10/views/default_40",
                        Value = "bot config value"
                    }
                }
            },
            Type = "auth"
        }
    };
 
    return Task.FromResult(response);
}
 
protected override Task<ConfigResponseBase> OnTeamsConfigSubmitAsync(ITurnContext<IInvokeActivity> turnContext, JObject configData, CancellationToken cancellationToken)
{
    ConfigResponseBase response = new ConfigResponse<TaskModuleResponseBase>
    {
        Config = new TaskModuleMessageResponse
        {
            Value = "test message"
        }
    };
 
    return Task.FromResult(response);
}
 
 
protected override Task<ConfigResponseBase> OnTeamsConfigFetchAsync(ITurnContext<IInvokeActivity> turnContext, JObject configData, CancellationToken cancellationToken)
{
    ConfigResponseBase response = createConfigContinueResponse();
    return Task.FromResult(response);
}
 
protected override Task<ConfigResponseBase> OnTeamsConfigSubmitAsync(ITurnContext<IInvokeActivity> turnContext, JObject configData, CancellationToken cancellationToken)
{
    ConfigResponseBase response = createConfigContinueResponse();
    return Task.FromResult(response);
}
 
private ConfigResponseBase createConfigContinueResponse()
{
    AdaptiveCard card = new AdaptiveCard("1.2")
    {
        Body = new List<AdaptiveElement>()
    };
 
    card.Body.Add(
        new AdaptiveContainer
        {
            Items = new List<AdaptiveElement>
            {
                new AdaptiveTextBlock
                {
                    Size = AdaptiveTextSize.Large,
                    Text = "bot config test",
                    Type = "TextBlock"
                }
            }
        });
 
    ConfigResponseBase response = new ConfigResponse<TaskModuleResponseBase>
    {
        Config = new TaskModuleContinueResponse
        {
            Value = new TaskModuleTaskInfo
            {
                Height = 123,
                Width = 456,
                Title = "test title",
                Card = new Attachment
                {
                    ContentType = AdaptiveCard.ContentType,
                    Content = card
                }
            },
            Type = "continue"
        }
    };
 
    return response;
}
 
```

---

## Bot configuration experience in Teams

After you've created a bot to enable the bot configuration settings from a team or group chat scope, the user can configure and reconfigure the bot in Teams.

To configure the bot, follow these steps:

1. Go to **Microsoft Teams**.

1. Select **Apps**.

1. From the Teams store, select a bot app you want to install.

1. From the dropdown next to **Add**, select **Add to a team** or **Add to a chat**.

   :::image type="content" source="../../assets/images/bots/group-chat-add-Bot.png" alt-text="Screenshot shows add your bot to chat.":::

1. Enter the name of a chat in the search field.

   :::image type="content" source="../../assets/images/bots/add-bot-to-chat.png" alt-text="Screenshot shows bot added to a chat.":::

1. Select **Set up a bot**.

   :::image type="content" source="../../assets/images/bots/set-up-a-bot.png" alt-text="Screenshot shows set up a bot in chat.":::

   The bot is installed in the chat.

### Reconfigure the bot

To reconfigure the bot, follow these steps:

1. Go to the chat and **@mention** the bot in the message compose area and select **Send**.

   :::image type="content" source="../../assets/images/bots/mention-bot.png" alt-text="Screenshot shows the interaction of bot.":::

1. When you hover over the bot from the conversation, an Adaptive Card appears. Select the **Settings** icon in the Adaptive Card.

   :::image type="content" source="../../assets/images/bots/bot-adaptive-card-interaction.png" alt-text="Screenshot shows the Adaptive Card with settings icon.":::

   A bot configuration Adaptive Card appears.

1. Reconfigure the bot settings and select **Submit**.

   :::image type="content" source="../../assets/images/bots/reconfigure-bot-settings.png" alt-text="Screenshot shows the Adaptive Card with settings icon to reconfigure.":::

   The bot sends a response message.

## Code sample

| **Sample name** | **Description** |**Node.js** |
|-----------------|-----------------|----------------|
| Bot configuration experience | This sample code describes the configuration and reconfiguration for bots in team and group chat. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-configuration-app/nodejs)|

## Step-by-step guide

Follow the [step-by-step guide](../../qsg-bot-configuration-experience.yml) to configure your bot during installation or after installation from the team or group chat where the bot is installed.

## See also

* [Build bots for Teams](../what-are-bots.md)
* [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
