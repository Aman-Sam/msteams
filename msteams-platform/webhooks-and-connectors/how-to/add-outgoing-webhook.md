---
title: Create an Outgoing Webhook
author: laujan
description: describes how to create an Outgoing Webhook
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
keywords: teams tabs outgoing webhook actionable message verify webhook
---

# Create Outgoing Webhook

The Outgoing Webhook acts as a bot and search for messages in channels using **@mention**. It sends notifications to external web services and responds with rich messages, which include cards and images. It helps to skip the process of creating bots through the [Microsoft Bot Framework](https://dev.botframework.com/).

<!--- TBD: Edit this article.
* Admonitions/alerts may be overused in this article. Check once.
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* Some screenshots like teamschannel.png may be redundant. Check once.
* Some headings use title case. We use sentence case for titles.
* Check for markdownlint errors. 
* Try using &nbsp; to add spaces in codeblocks for indentation and remove the hard tabs.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

## Key features of Outgoing Webhook

The following table provides the features and description of Outgoing Webhooks:

| Features | Description |
| ------- | ----------- |
| Scoped configuration| Webhooks are scoped at the team level. Mandatory set up process for each adds an Outgoing Webhook. |
| Reactive messaging| Users must use @mention for the webhook to receive messages. Currently, users can only message an Outgoing Webhook in public channels and not within the personal or private scope. |
|Standard HTTP message exchange|Responses appear in the same chain as the original request message and can include any Bot Framework message content. For example, rich text, images, cards, and emojis. Although Outgoing Webhooks can use cards, they can't use any card actions except for `openURL`.|
| Teams API method support|Outgoing Webhooks sends an HTTP POST to a web service and gets a response. They can't access any other APIs, such as retrieve the roster or list of channels in a team.|

## Create Outgoing Webhooks

Create Outgoing Webhooks and add custom bots to Teams.

To create an Outgoing Webhook, follow these steps:

1. Select **Teams** from the left pane. The **Teams** page appears:

    ![Teams channel](~/assets/images/teamschannel.png)

1. In the **Teams** page, select the required team to create an Outgoing Webhook and select the &#8226;&#8226;&#8226;. In the dropdown menu, select **Manage team**:

    ![Create Outgoing Webhook](~/assets/images/outgoingwebhook1.png)

1. Select the **Apps** tab on the channel page:

    ![Create an Outgoing Webhook](~/assets/images/outgoingwebhook2.png)

1. Select **Create an Outgoing Webhook**:

    ![Create Outgoing Webhooks](~/assets/images/outgoingwebhook3.png)

1. Type the following details in the **Create an Outgoing Webhook** page:

    * **Name**: The webhook title and @mention tab.
    * **Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.
    * **Description**: A detailed string that appears in the profile card and the team-level App dashboard.
    * **Profile Picture**: An app icon for your webhook, which is optional.

1. Select **Create**. The Outgoing Webhook is added to the current team's channel:

    ![create Outgoing Webhook](~/assets/images/outgoingwebhook.png)

A [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) dialogue box appears. It's a security token used to authenticate calls between Teams and the designated outside service. The HMAC security token doesn't expire and is unique for each configuration.

>[!NOTE]
> The Outgoing Webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal. For example, an HMAC handshake.

The following scenario provides the details to add an Outgoing Webhook:

* Scenario: Push change status notifications on a Teams channel database server to your app.
* Example: You have a line of business app that tracks all CRUD (create, read, update, and delete) operations. These operations are made to the employee records by Teams channel HR users across an Office 365 tenancy.

# [URL JSON payload](#tab/urljsonpayload)

**Create a URL on your app's server to accept and process a POST request with a JSON payload**

Your service receives messages in a standard Azure bot service messaging schema. The Bot Framework connector is a RESTful service that empowers to process the interchange of JSON formatted messages through HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Alternatively, you can follow the Microsoft Bot Framework SDK to process and parse messages. For more information, see [overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).

Outgoing Webhooks are scoped to the `team` level and are visible to all the team members. Users need to **\@mention** the name of the Outgoing Webhook to invoke it in the channel.

# [Verify HMAC token](#tab/verifyhmactoken)

**Create a method to verify the Outgoing Webhook HMAC token**

Using example of inbound message and ID: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.

Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.

To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` authorization header. Always include the code in your authentication protocol.

Your code must always validate the HMAC signature included in the request as follows:

* Generate the HMAC token from the request body of the message. There are standard libraries to do this on most platform, such as [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js and [Teams webhook sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#. Microsoft Teams uses standard SHA256 HMAC cryptography. You must convert the body to a byte array in UTF8.
* Compute the hash from the byte array of the security token provided by Teams when you registered the Outgoing Webhook in the Teams client. See [create an Outgoing Webhook](#create-outgoing-webhook).
* Convert the hash to a string using UTF-8 encoding.
* Compare the string value of the generated hash with the value provided in the HTTP request.

# [Method to respond](#tab/methodtorespond)

**Create a method to send a success or failure response**

Responses from your Outgoing Webhooks appear in the same reply chain as the original message. When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.

### Example response

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

---

> [!NOTE]
> * You can send Adaptive Card, Hero card, and text messages as attachment with an Outgoing Webhook.
> * Cards support formatting. For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).

The following codes are examples of an Adaptive Card response:

# [C#/.NET](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# [JavaScript/Node.js](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# [JSON](#tab/json)

```json
{
	"type": "message",
	"attachments": [
		{
			"contentType": "application/vnd.microsoft.card.adaptive",
			"content": {
				"type": "AdaptiveCard",
				"version": "1.4",
				"body": [
					{
						"type": "TextBlock",
						"text": "Request sent by: Megan"
					},
					{
						"type": "Image",
						"url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
					},
					{
						"type": "TextBlock",
						"text": "Sample image for Adaptive Card.."
					}
				]
			}
		}
	]
}
```

---

## Code sample

|**Sample name** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Outgoing Webhooks | Samples to create custom bots to be used in Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## See also

* [Create an Incoming Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Create and send messages](~/webhooks-and-connectors/how-to/connectors-using.md)
