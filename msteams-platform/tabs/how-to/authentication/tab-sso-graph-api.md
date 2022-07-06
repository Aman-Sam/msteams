---
title: Extend tab app with Microsoft Graph permissions
description: Describes configuring API permissions with Microsoft Graph
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams authentication tabs Microsoft Azure Active Directory (Azure AD) Graph API Delegated permission access token scope
---
# Extend tab app with Microsoft Graph permissions and scope

You can extend your tab app by using Microsoft Graph to allow users additional permissions, such as to view app user profile, to read mail, and more. Your app must ask for specific permission scopes to obtain the access tokens on app user's consent.

Graph scopes, such as `User.Read` or `Mail.Read`, lets you specify how your app accesses a Teams user's account. You need to specify your scopes in the authorization request.

In this section, you'll learn to:

- [Configure API permissions in Azure AD](#configure-api-permissions-in-azure-ad)
- [Configure authentication for different platforms](#configure-authentication-for-different-platforms)
- [Acquire access token for MS Graph](#acquire-access-token-for-ms-graph)

## Configure API permissions in Azure AD

You can configure additional Graph scopes in Azure AD for your app. These are delegated permissions, which are used by apps that require signed-in access. A signed-in app user or administrator must consent to them. Your tab app can consent on behalf of the signed-in user when it calls Microsoft Graph.

### To configure API permissions

1. Open the app you registered in the [Azure portal](https://ms.portal.azure.com/).

2. Select **Manage** > **API permission** from the left pane.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="App permissions menu option.":::

    The **API permissions** page appears.

3. Select **+ Add permissions** to add Microsoft Graph API permissions.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="App permissions page.":::

    The **Request API permissions** page appears.

4. Select **Microsoft Graph**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text="Request API permissions page.":::

    The options for Graph permissions display.

5. Select **Delegated permissions** to view the list of permissions.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="Delegated permissions.":::

6. Select relevant permissions for your app, and then select **Add permissions**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="Select permissions.":::

    You can also enter the permission name in the search box to find it.

    A message pops up on the browser stating that the permissions were updated.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="Permissions updated message.":::

    The added permissions are displayed in the **API permissions** page.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="API permissions are configured.":::

    You've configured your app with Microsoft Graph permissions.

## Configure authentication for different platforms

Depending on the platform or device where you want to target your app, additional configuration may be required such as redirect URIs, specific authentication settings, or details specific to the platform.

> [!NOTE]
>
> - If your tab app hasn't been granted IT admin consent, app users have to provide consent the first time they use your app on a different platform.
> - Implicit grant is not required if SSO is enabled on a tab app.

You can configure authentication for multiple platforms as long as the URL is unique.

### To configure authentication for a platform

1. Open the app you registered in the the [Azure portal](https://ms.portal.azure.com/).

1. Select **Manage** > **Authentication** from the left pane.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="Authenticate for platforms":::

    The **Platform configurations** page appears.

1. Select **+ Add a platform**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="Add a platforms":::

    The **Configure platforms** page appears.

1. Select the platform that you want to configure for your tab app. You can choose the platform type from web or SPA.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="Select web platform":::

    You can configure multiple platforms for a particular platform type. Ensure that the redirect URI is unique for every platform you configure.

    The Configure Web page appears.

    > [!NOTE]
    > The configurations will be different based on the platform you select.

1. Enter the configuration details for the platform.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="Configure web platform":::

    1. Enter the redirect URI. The URI should be unique.
    2. Enter the front-channel logout URL.
    3. Select the tokens you want Azure AD to send for your app.

1. Select **Configure**.

    The platform is configured and displayed in the **Platform configurations** page.

## Acquire access token for MS Graph

You'll need to acquire access token for Microsoft Graph. You can do so by using Azure AD OBO flow.

The current implementation for SSO grants consent for only user-level permissions that are not usable for making Graph calls. To get the permissions (scopes) needed to make a Graph call, SSO apps must implement a custom web service to exchange the token received from the Teams JavaScript SDK for a token that includes the needed scopes. You can use Microsoft Authentication Library (MSAL) for fetching the token from the client side.

After you've configured Graph permissions in Azure AD:

- [Configure your client-side code to fetch access token using MSAL](#configure-code-to-fetch-access-token-using-msal)
- [Pass the access token to server-side code](#pass-the-access-token-to-server-side-code)

### Configure code to fetch access token using MSAL

The following code provides an example of OBO flow to fetch access token from the Teams client using MSAL.

### [C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### [Node.js](#tab/nodejs)

```Node.js

// Exchange client Id side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenant id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```

---

### Pass the access token to server-side code

If you need to access Microsoft Graph data, configure your server-side code to:

1. Validate the access token. For more information, see [Validate the access token](tab-sso-code.md#validate-the-access-token).
1. Initiate the OAuth 2.0 OBO flow with a call to the Microsoft identity platform that includes the access token, some metadata about the user, and the credentials of the tab app (its app ID and client secret). The Microsoft identity platform will return a new access token that can be used to access Microsoft Graph.
1. Get data from Microsoft Graph by using the new token.
1. Use token cache serialization in MSAL.NET to cache the new access token for multiple, if required.

> [!IMPORTANT]
> As a best practice for security, always use the server-side code to make Microsoft Graph calls, or other calls that require passing an access token. Never return the OBO token to the client to enable the client to make direct calls to Microsoft Graph. This helps protect the token from being intercepted or leaked.

## Known limitations

Tenant admin consent: A simple way of [consenting on behalf of an organization as a tenant admin](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent) is by getting [consent from admin](/azure/active-directory/manage-apps/grant-admin-consent).

You can ask for consent using the Auth API. Another approach for getting Graph scopes is to present a consent dialog using our existing [third party OAuth provider authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page). This approach involves popping up an Azure AD consent dialog box.

<details>
<summary>To ask for additional consent using the Auth API, follow these steps:</summary>

1. The token retrieved using `getAuthToken()` must be exchanged on the server-side using Azure AD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) to get access to those other Graph APIs. Ensure you use the v2 Graph endpoint for this exchange.
2. If the exchange fails, Azure AD returns an invalid grant exception. It usually responds with one of the two error messages, `invalid_grant` or `interaction_required`.
3. When the exchange fails, you must ask for consent. Use the user interface (UI) to ask the app user to grant other consent. This UI must include a button that triggers an Azure AD consent dialog using [Silent authentication](~/concepts/authentication/auth-silent-aad.md).
4. When asking for more consent from Azure AD, you must include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to Azure AD, otherwise Azure AD wouldn't ask for other scopes.
    - Instead of `?scope={scopes}`, use `?prompt=consent&scope={scopes}`
    - Ensure that `{scopes}` includes all the scopes you're prompting the user for, for example, `Mail.Read` or `User.Read`.
5. After the app user has granted more permissions, retry the OBO flow to get access to these other APIs.

    </details>

## See also

- [OAuth 2.0 On-Behalf-Of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [Get access for MS Graph](/graph/auth-v2-user)
- [Token cache serialization in MSAL.NET](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)
- [Microsoft Teams MSAL2 provider](/graph/toolkit/providers/teams-msal2)
