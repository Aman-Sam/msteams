> [!NOTE]
> SSO handlers except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the `TeamsMessagingExtensionsSearchAuthConfigBot.cs` file aren't supported.

This section covers:

1. [Update development environment variables](#update-development-environment-variables)
1. [Add code to request a token](#add-code-to-request-a-token)
1. [Add code to receive the token](#add-code-to-receive-the-token)
1. [Add token to Bot Framework Token Store](#add-token-to-bot-framework-token-store)
1. [Handle app user log out](#handle-app-user-log-out)

## Update development environment variables

You've configured client secret and OAuth connection setting for the app in Azure AD. You must configure your app code with these variables.

To update the development environment variables:

1. Open the bot app project.
1. Open the `./env` file for your project.
1. 1. Update the following variables:

    - For `MicrosoftAppId`, update the Bot registration ID from Azure AD.
    - For `MicrosoftAppPassword`, update the Bot registration client secret.
    - For `ConnectionName`, update the name of the OAuth connection you configured in Azure AD.
    - For `MicrosoftAppTenantId`, update the tenant ID.

1. Save the file.

You've now configured the required environment variables for your bot app and for SSO. Next, add the code for handling bot tokens.

## Add code to request a token

The request to get the token is a POST message request using the existing message schema. It's included in the attachments of an OAuthCard. The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true). Teams refreshes the token if the `TokenExchangeResource` property is populated on the card. For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.

>[!NOTE]
> The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.

To update your app's code:

1. Add code snippet for `TeamsSSOTokenExchangeMiddleware`.

    # [csharp](#tab/cs1)

    Add the following code snippet to `AdapterWithErrorHandler.cs` (or the equivalent class in your app's code):

    ```csharp
    base.Use(new TeamsSSOTokenExchangeMiddleware(storage, configuration["ConnectionName"]));
    ```

    # [JavaScript](#tab/js1)
    
    Add the following code snippet to `index.js` (or the equivalent class in your app's code):
    
    ```JavaScript
    const {TeamsSSOTokenExchangeMiddleware} = require('botbuilder');
    const tokenExchangeMiddleware = new TeamsSSOTokenExchangeMiddleware(memoryStorage, env.connectionName);
    adapter.use(tokenExchangeMiddleware);
    ```
    
    ---

1. Use the following code snippet for requesting a token.

    # [csharp](#tab/cs2)

    After you add the `AdapterWithErrorHandler.cs`, your code should be as shown below:
    
    ```csharp
        ```csharp
    public class AdapterWithErrorHandler : CloudAdapter
    {
        public AdapterWithErrorHandler(
            IConfiguration configuration,
            IHttpClientFactory httpClientFactory,
            ILogger<IBotFrameworkHttpAdapter> logger,
            IStorage storage,
            ConversationState conversationState)
            : base(configuration, httpClientFactory, logger)
        {
            base.Use(new TeamsSSOTokenExchangeMiddleware(storage, configuration["ConnectionName"]));

            OnTurnError = async (turnContext, exception) =>
            {
                // Log any leaked exception from the application.
                // NOTE: In production environment, you should consider logging this to
                // Azure Application Insights. Visit https://aka.ms/bottelemetry to see how
                // to add telemetry capture to your bot.
                logger.LogError(exception, $"[OnTurnError] unhandled error : {exception.Message}");

                // Send a message to the user
                await turnContext.SendActivityAsync("The bot encountered an error or bug.");
                await turnContext.SendActivityAsync("To continue to run this bot, please fix the bot source code.");

                if (conversationState != null)
                {
                    try
                    {
                        // Delete the conversationState for the current conversation to prevent the
                        // bot from getting stuck in a error-loop caused by being in a bad state.
                        // ConversationState should be thought of as similar to "cookie-state" in a Web pages.
                        await conversationState.DeleteAsync(turnContext);
                    }
                    catch (Exception e)
                    {
                        logger.LogError(e, $"Exception caught on attempting to Delete ConversationState : {e.Message}");
                    }
                }

                // Send a trace activity, which will be displayed in the Bot Framework Emulator
                await turnContext.TraceActivityAsync(
                    "OnTurnError Trace",
                    exception.Message,
                    "https://www.botframework.com/schemas/error",
                    "TurnError");
            };
        }
    }
    ```

    # [JavaScript](#tab/js2)
    
    After you add the code to `index.js`, your code should be as shown below:

    ```JavaScript
    adapter.onTurnError = async (context, error) => {
        // This check writes out errors to console log .vs. app insights.
        // NOTE: In production environment, you should consider logging this to Azure
        //       application insights. See https://aka.ms/bottelemetry for telemetry
        //       configuration instructions.
        console.error(`\n [onTurnError] unhandled error: ${ error }`);
    
        // Send a trace activity, which will be displayed in Bot Framework Emulator
        await context.sendTraceActivity(
            'OnTurnError Trace',
            `${ error }`,
            'https://www.botframework.com/schemas/error',
            'TurnError'
        );
    
        // Send a message to the user
        await context.sendActivity('The bot encountered an error or bug.');
        await context.sendActivity('To continue to run this bot, please fix the bot source code.');
        // Clear out state
        await conversationState.delete(context);
    };
    
    // Define the state store for your bot.
    // See https://aka.ms/about-bot-state to learn more about using MemoryStorage.
    // A bot requires a state storage system to persist the dialog and user state between messages.
    //const memoryStorage = new MemoryStorage();
    
    // Create conversation and user state with in-memory storage provider.
    const conversationState = new ConversationState(memoryStorage);
    const userState = new UserState(memoryStorage);
    
    // Create the main dialog.
    const dialog = new MainDialog();
    // Create the bot that will handle incoming messages.
    const bot = new TeamsBot(conversationState, userState, dialog);
    
    // Create HTTP server.
    const server = restify.createServer();
    server.use(restify.plugins.bodyParser());
    
    server.listen(process.env.port || process.env.PORT || 3978, function() {
        console.log(`\n${ server.name } listening to ${ server.url }`);
        console.log('\nGet Bot Framework Emulator: https://aka.ms/botframework-emulator');
        console.log('\nTo talk to your bot, open the emulator select "Open Bot"');
    });
    
    // Listen for incoming requests.
    server.post('/api/messages', async (req, res) => {
        // Route received a request to adapter for processing
        await adapter.process(req, res, (context) => bot.run(context));
    });
    ```

---

### Consent dialog for getting access token

If the app user is using the application for the first time, consent is required for SSO authentication.

:::image type="content" source="~/assets/images/authentication/teams-sso-mex/me-sso-profile-select.png" alt-text="SSO authentication for message extension app":::

When the app user selects the user name, validation is done using the Teams identity.

:::image type="content" source="~/assets/images/authentication/teams-sso-mex/me-sso-completed.png" alt-text="SSO authentication completed for message extension app":::

The consent dialog that appears is for open-id scopes defined in Azure AD. The app user must give consent only once. After consenting, the app user can access and use your message extension app for the granted permissions and scopes.

> [!IMPORTANT]
> Scenarios where consent dialogs are not needed:
>
> - If the tenant administrator has granted consent on behalf of the tenant, app users don't need to be prompted for consent at all. This means that the app users don't see the consent dialogs, and can access the app seamlessly.
> - If your Azure AD app is registered in the same tenant from which you're requesting an authentication in Teams, the app user can't be asked to consent, and is granted an access token right away. App users consent to these permissions only if the Azure AD app is registered in a different tenant.

If you encounter any errors, see [Troubleshoot SSO authentication in Teams](~/tabs/how-to/authentication/tab-sso-troubleshooting.md).

## Add code to receive the token

The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today. The only difference is the invoke name,
**sign in/tokenExchange**, and the **value** field. The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.

>[!NOTE]
> You might receive multiple responses for a given request if the user has multiple active endpoints. You must eliminate all duplicate or redundant responses with the token. For more information about **signin/tokenExchange**, see [TeamsSSOTokenExchangeMiddleware Class](/python/api/botbuilder-core/botbuilder.core.teams.teams_sso_token_exchange_middleware.teamsssotokenexchangemiddleware?view=botbuilder-py-latest#remarks&preserve-view=true).

Use the following code snippet example to invoke response:

# [csharp](#tab/cs3)

```csharp
private async Task<DialogTurnResult> PromptStepAsync(WaterfallStepContext stepContext, CancellationToken cancellationToken)
        {
            return await stepContext.BeginDialogAsync(nameof(OAuthPrompt), null, cancellationToken);
        }

private async Task<DialogTurnResult> LoginStepAsync(WaterfallStepContext stepContext, CancellationToken cancellationToken)
        {
            
            var tokenResponse = (TokenResponse)stepContext.Result;
            if (tokenResponse?.Token != null)
            {
                var token = tokenResponse.Token;

                 // On successful login, the token contains sign in token.
            }
            await stepContext.Context.SendActivityAsync(
            MessageFactory.Text("Login was not successful please try again."), cancellationToken);

            return await stepContext.EndDialogAsync(cancellationToken: cancellationToken);
        }
```

# [JavaScript](#tab/js3)

```JavaScript
async loginStep(stepContext) {
        // Get the token from the previous step. Note that we could also have gotten the
        // token directly from the prompt itself. There is an example of this in the next method.
        const tokenResponse = stepContext.result;
        if (!tokenResponse || !tokenResponse.token) {
            await stepContext.context.sendActivity('Login was not successful please try again.');
        } else {
            const token = new SimpleGraphClient(tokenResponse.token);
        }
        return await stepContext.endDialog();
    }
```
---

> [!NOTE]
> The code snippets use the Waterfall Dialog bot. For more information about Waterfall Dialog, see [About component and waterfall dialogs](/azure/bot-service/bot-builder-concept-waterfall-dialogs?view=azure-bot-service-4.0&preserve-view=true).

<!--The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot. You must store the tokens for performance reasons and refresh them.-->

You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you're enabling the SSO for:

```json
JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
if(valueObject["authentication"] !=null)
 {
    JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
    if(authenticationObject["token"] !=null)
 }
```

### Validate the access token

Web APIs on your server must decode the access token, and verify if it's sent from the client. 

> [!NOTE]
> If you use Bot Framework, it handles the access token validation. If you don't use Bot Framework, follow the guidelines in this section.

For more information about validating access token, see [Validate tokens](/azure/active-directory/develop/access-tokens.md#validate-tokens)

<!--The token is a JSON Web Token (JWT), which means that validation works just like token validation in most standard OAuth flows. The web APIs must decode access token. Optionally, you can copy and paste access token manually into a tool, such as jwt.ms.-->

There are a number of libraries available that can handle JWT validation. Basic validation includes:

- Checking that the token is well-formed
- Checking that the token was issued by the intended authority
- Checking that the token is targeted to the web API

Keep in mind the following guidelines when validating the token:

- Valid SSO tokens are issued by Azure AD. The `iss` claim in the token should start with this value.
- The token's `aud1` parameter will be set to the app ID generated during Azure AD app registration.
- The token's `scp` parameter will be set to `access_as_user`.

#### Example access token

The following is a typical decoded payload of an access token.

```javascript
{
    aud: "2c3caa80-93f9-425e-8b85-0745f50c0d24",
    iss: "https://login.microsoftonline.com/fec4f964-8bc9-4fac-b972-1c1da35adbcd/v2.0",
    iat: 1521143967,
    nbf: 1521143967,
    exp: 1521147867,
    aio: "ATQAy/8GAAAA0agfnU4DTJUlEqGLisMtBk5q6z+6DB+sgiRjB/Ni73q83y0B86yBHU/WFJnlMQJ8",
    azp: "e4590ed6-62b3-5102-beff-bad2292ab01c",
    azpacr: "0",
    e_exp: 262800,
    name: "Mila Nikolova",
    oid: "6467882c-fdfd-4354-a1ed-4e13f064be25",
    preferred_username: "milan@contoso.com",
    scp: "access_as_user",
    sub: "XkjgWjdmaZ-_xDmhgN1BMP2vL2YOfeVxfPT_o8GRWaw",
    tid: "fec4f964-8bc9-4fac-b972-1c1da35adbcd",
    uti: "MICAQyhrH02ov54bCtIDAA",
    ver: "2.0"
}
```

## Add token to Bot Framework Token Store

If you're using the OAuth connection, you must update or add the token in the Bot Framework Token store. Use the following code snippet example to add to the `TeamsMessagingExtensionsSearchAuthConfigBot.cs` file for updating or adding the token in the store:

```c#
protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
     {
         JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
         if (valueObject["authentication"] != null)
         {
             JObject authenticationObject = JObject.FromObject(valueObject["authentication"]);
             if (authenticationObject["token"] != null)
             {
                 //If the token is NOT exchangeable, then return 412 to require user consent
                 if (await TokenIsExchangeable(turnContext, cancellationToken))
                 {
                     return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
                 }
                 else
                 {
                     var response = new InvokeResponse();
                     response.Status = 412;
                     return response;
                 }
             }
         }
         return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
     }
     private async Task<bool> TokenIsExchangeable(ITurnContext turnContext, CancellationToken cancellationToken)
     {
         TokenResponse tokenExchangeResponse = null;
         try
         {
             JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
             var tokenExchangeRequest =
             ((JObject)valueObject["authentication"])?.ToObject<TokenExchangeInvokeRequest>();
             var userTokenClient = turnContext.TurnState.Get<UserTokenClient>();
             tokenExchangeResponse = await userTokenClient.ExchangeTokenAsync(
                             turnContext.Activity.From.Id,
                              _connectionName,
                              turnContext.Activity.ChannelId,
                              new TokenExchangeRequest
              {
                  Token = tokenExchangeRequest.Token,
              },
               cancellationToken).ConfigureAwait(false);
         }
 #pragma warning disable CA1031 //Do not catch general exception types (ignoring, see comment below)
         catch
 #pragma warning restore CA1031 //Do not catch general exception types
         {
             //ignore exceptions
             //if token exchange failed for any reason, tokenExchangeResponse above remains null, and a failure invoke response is sent to the caller.
             //This ensures the caller knows that the invoke has failed.
         }
         if (tokenExchangeResponse == null || string.IsNullOrEmpty(tokenExchangeResponse.Token))
         {
             return false;
         }
         return true;
     }
```

## Handle app user log out

Use the following code snippet to handle the access token in case the app user logs out:

# [csharp](#tab/cs4)

```csharp
    private async Task<DialogTurnResult> InterruptAsync(DialogContext innerDc, 
    CancellationToken cancellationToken = default(CancellationToken))
        {
            if (innerDc.Context.Activity.Type == ActivityTypes.Message)
            {
                var text = innerDc.Context.Activity.Text.ToLowerInvariant();

                // Allow logout anywhere in the command
                if (text.IndexOf("logout") >= 0)
                {
                    // The UserTokenClient encapsulates the authentication processes.
                    var userTokenClient = innerDc.Context.TurnState.Get<UserTokenClient>();
                    await userTokenClient.SignOutUserAsync(
    innerDc.Context.Activity.From.Id, 
    ConnectionName, 
    innerDc.Context.Activity.ChannelId, 
    cancellationToken
    ).ConfigureAwait(false);

                    await innerDc.Context.SendActivityAsync(MessageFactory.Text("You have been signed out."), cancellationToken);
                    return await innerDc.CancelAllDialogsAsync(cancellationToken);
                }
            }

            return null;
        }
```

# [JavaScript](#tab/js4)

```JavaScript
    async interrupt(innerDc) {
        if (innerDc.context.activity.type === ActivityTypes.Message) {
            const text = innerDc.context.activity.text.toLowerCase();
            if (text === 'logout') {
                const userTokenClient = innerDc.context.turnState.get(innerDc.context.adapter.UserTokenClientKey);

                const { activity } = innerDc.context;
                await userTokenClient.signOutUser(activity.from.id, this.connectionName, activity.channelId);

                await innerDc.context.sendActivity('You have been signed out.');
                return await innerDc.cancelAllDialogs();
            }
        }
    }
```

---

## Code sample

This section provides Bot authentication v3 SDK sample.

| **Sample name** | **Description** | **C#** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Bot authentication | This sample shows how to get started with authentication in a bot for Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Tab, Bot and Message Extension (ME) SSO | This sample shows SSO for Tab, Bot and ME - search, action, link unfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | NA |
|Tab, Bot, and Message extension| This sample shows how to check authentication in Bot,Tab, and Message extension with SSO | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-auth/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-auth/nodejs) | NA |
