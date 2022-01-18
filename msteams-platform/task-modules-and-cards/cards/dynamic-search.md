---
title: Typeahead search in Adaptive Cards 
author: Rajeshwari-v
description: Describes typeahead search with Input.ChoiceSet control in Adaptive Cards 
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
---

# Typeahead search in Adaptive Cards

Typeahead search functionality in Adaptive Cards gives an enhanced search experience on `input.choiceset` component. It provides a list of choices to enter text in the search field. You can incorporate typeahead search with Adaptive Cards to search and select data.

You can use typeahead search for the following searches:

* [Static search](#static-typeahead-search)
* [Dynamic search](#dynamic-typeahead-search)

## Static typeahead search

Static typeahead search allows users to search from values specified within `input.choiceset` in the Adaptive Card payload. Static typeahead search can be used to show multiple choices to the user. The payload size in static search increases with number of choices specified in the payload.
As user starts entering the texts, the choices are filtered, which partially match the input. The dropdown list highlights the input characters that match the search.

The following image demonstrates static typeahead search:

![Static typeahead search](~/assets/images/Cards/static-typeahead-search.gif)

## Dynamic typeahead search

Dynamic typeahead search is useful to search and select data from large data sets. The data sets are loaded dynamically from the dataset specified in the card payload. The type ahead functionality helps to filter out the choices as the user types.

# [Desktop](#tab/desktop)

![Dynamic typeahead search](~/assets/images/Cards/dynamic-typeahead-search-desktop.png)

![Dynamic typeahead search image 2](~/assets/images/Cards/dynamic-typeahead-search-desktop-2.png)

# [Mobile](#tab/mobile)

Android and iOS mobile clients support typeahead search in Adaptive Cards.

**Scenario**

John is a store employee who works at an Xbox retail store. The store uses a bot to take new purchase requests from customers. A customer can search from the thousands of games available. Typeahead search in Adaptive Cards is used to search and select customers' choices.

**To use typeahead search in Adaptive Cards**

1. User A opens the store bot.
1. User A sends a command to the bot for a **New customer request**. The bot responds with the Adaptive Card that has `Input.ChoiceSet` component.
1. User A uses typeahead search to search and select the information based on the customer's choice.

The following image illustrates mobile experience of typeahead search:

![Static typeahead search](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> You can't get rich card experiences with dynamic search, such as query based messaging extensions.

## Implement typeahead search

`Input.ChoiceSet` is one of the important input components in Adaptive Cards. You can add a typeahead search control to `Input.ChoiceSet` component to implement typeahead search. You can search and select the required information with the following selections:

* Dropdown, such as expanded selection.
* Radio button, such as single selection.
* Check boxes, such as multiple selections.

> [!NOTE]
> The `Input.ChoiceSet` control is based on the style and `isMultiSelect` properties.

### Schema properties

The following properties are the new additions to the [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema to enable typeahead search:

| Property| Type | Required | Description |
|-----------|------|----------|-------------|
| style | Compact <br/> Expanded <br/> Filtered | No | Adds filtered style to the list of supported validations for static type-ahead.|
| choices.data | Data.Query | No | Enables dynamic type-ahead as the user types, by fetching a remote set of choices from a backend. |

### Data.Query definition

| Property| Type | Required | Description |
|-----------|------|----------|-------------|
| type | Data.Query	| Yes |	Specifies that it's a Data.Query object.|
| dataset | String | Yes | Specifies the type of data that is fetched dynamically. |
| value	| String | No | Populates for the invoke request to the bot with the input that the user provided to the `ChoiceSet`. |
| count	| Number | No | Populates for the invoke request to the bot to specify the number of elements that must be returned. The bot ignores it, if the users want to send a different amount. | 
| skip | Number | No | Populates for the invoke request to the bot to indicate that users want to paginate and move ahead in the list. |

### Example

The example payload which contains static and dynamic typeahead search with single & multi select options as follows:

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "columns": [
        {
          "width": "1",
          "items": [
            {
              "size": null,
              "url": "https://urlp.asm.skype.com/v1/url/content?url=https%3a%2f%2fi.imgur.com%2fhdOYxT8.png",
              "height": "auto",
              "type": "Image"
            }
          ],
          "type": "Column"
        },
        {
          "width": "2",
          "items": [
            {
              "size": "extraLarge",
              "text": "Game Purchase",
              "weight": "bolder",
              "wrap": true,
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Please fill out the below form to send a game purchase request.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Call of Duty",
                  "value": "call_of_duty"
                },
                {
                  "title": "Death's Door",
                  "value": "deaths_door"
                },
                {
                  "title": "Grand Theft Auto V",
                  "value": "grand_theft"
                },
                {
                  "title": "Minecraft",
                  "value": "minecraft"
                }
              ],
              "style": "filtered",
              "placeholder": "Search for a game",
              "id": "choiceGameSingle",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Multi-Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Static Option 1",
                  "value": "static_option_1"
                },
                {
                  "title": "Static Option 2",
                  "value": "static_option_2"
                },
                {
                  "title": "Static Option 3",
                  "value": "static_option_3"
                }
              ],
              "isMultiSelect": true,
              "style": "filtered",
              "choices.data": {
                "type": "Data.Query",
                "dataset": "xbox"
              },
              "id": "choiceGameMulti",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Needed by: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        },
        {
          "width": "stretch",
          "items": [
            {
              "id": "choiceDate",
              "type": "Input.Date"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Buy and download digital games and content directly from your Xbox console, Windows 10 PC, or at Xbox.com.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "text": "Earn points for what you already do on Xbox, then redeem your points on real rewards. Play more, get rewarded. Start earning today.",
      "wrap": true,
      "type": "TextBlock"
    }
  ],
  "actions": [
    {
      "data": {
        "msteams": {
          "type": "invoke",
          "value": {
            "type": "task/submit"
          }
        }
      },
      "title": "Request Purchase",
      "type": "Action.Submit"
    }
  ],
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.2"
}
```

## Code snippets for invoke request and response

### Invoke Request

```json
{
    "name": "application/search",
    "type": "invoke",
    "value": {
        "queryText": "fluentui",
        "queryOptions": {
            "skip": 0,
            "top": 15
        },
        "dataset": "npm"
    },
    "locale": "en-US",
    "localTimezone": "America/Los_Angeles",
    // …. other fields
}
```

### Response

#### [C#](#tab/csharp)

```csharp
protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Name == "application/search")
    {
	var packages = new[] {
			new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
			new { title = "Fluent UI Library", value = "FluentUI" }};

	var searchResponseData = new
	{
	    type = "application/vnd.microsoft.search.searchResponse",
	    value = new
	    {
		results = packages
	    }
	};
	var jsonString = JsonConvert.SerializeObject(searchResponseData);
	JObject jsonData = JObject.Parse(jsonString);
	return new InvokeResponse()
	{
	    Status = 200,
	    Body = jsonData
	};
    }

    return null;
}
```

#### [Node.js](#tab/nodejs)
 
```nodejs
  async onInvokeActivity(context) {
    if (context._activity.name == 'application/search') {
      // let searchQuery = context._activity.value.queryText;  // This can be used to filter the results
      var successResult = {
        status: 200,
        body: {
          "type": "application/vnd.microsoft.search.searchResponse",
          "value": {
            "results": [
              {
                "value": "FluentAssertions",
                "title": "A very extensive set of extension methods"
              },
              {
                "value": "FluentUI",
                "title": "Fluent UI Library"
              }
            ]
          }
        }
      }

      return successResult;

    }
  }
```

####  [JSON](#tab/json)

```json
{
    "status": 200,
    "body" : {
        "type": "application/vnd.microsoft.search.searchResponse",
        "value": {
           "results": [
                {
                    "value": "FluentAssertions",
                    "title": "A very extensive set of extension methods."
                },
                {
                    "value": "FluentUI",
                    "title": "Fluent UI Library"
                }
            ]
        }
    }
}
```

---

## Code sample

|**Sample name** | **Description** | **C#** | **Node.js** |
|----------------|-----------------|--------------|----------------|
| Typeahead search control on Adaptive Cards | The sample shows the features of static and dynamic typeahead search control in Adaptive Cards. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/nodejs) |


## See also

* [Universal Actions for Adaptive Cards](Universal-actions-for-adaptive-cards/Overview.md)
* [Task modules](../what-are-task-modules.md)
