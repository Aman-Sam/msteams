---
title: Share to Teams from personal app or tab
description: Learn how to enable the Share to Teams button on your personal app or tab, limitations and end user experience.
ms.topic: reference
ms.localizationpriority: medium
---
# Share to Teams from personal app or tab

Share to Teams allows users to share the content from personal app or tab to other user or group or channel within Teams. Users can select Share to Teams to launch the Share to Teams experience in a pop-up window. The pop-up window allows users to add other user or group or channel to share the content.

The following image shows the Share to Teams pop-up window:

:::image type="content" source="../../assets/images/share-to-teams/share-to-teams.PNG" alt-text="The screenshot shows the Share to Teams pop-up window.":::

## Enable Share to Teams button

> [!NOTE]
> Ensure that you have [Microsoft Teams JavaScript Client SDK](../../tabs/how-to/using-teams-client-sdk.md) or [Microsoft Teams JavaScript Client SDK v2 Preview](../../tabs/how-to/using-teams-client-sdk.md) (`@microsoft/teams-js@1.11.0-beta.7` or later) to enable Share to Teams for your personal app or tab.

To enable Share to Teams:

1. Create a personal app or tab with **Teams Javascript Client SDK**.

2. Create a **Share to Teams** button.

3. On Share to Teams button, call `microsoftTeams.sharing.shareWebContent` with a content payload.

The following example explains how to create a content payload:

```json
microsoftTeams.sharing.shareWebContent({
        content: [
          {
            type: 'URL',
            url: '<URL to be shared>',
            message: 'Default message to be loaded in the compose box',
            preview: true
          }
        ]
      });
```

The payload contains the following parameters:

| Property name | Purpose |
|---|---|
| `type` | The type must be `URL` |
| `url` | `URL` to be shared |
|`message`| Default message to be loaded in the compose box |
| `preview` | Set to `true` to enable URL preview |

The following image shows the Share to Teams option:

:::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="The screenshot shows the Share to Teams button.":::

## Response codes

The following table provides the response codes:

|Response code|Description|
|---|---|
| **100** | API not supported in the current platform. |
| **404** | The file specified wasn't found on the given location. |
| **500** | Internal error encountered while performing the required operation. |
| **501** | API isn't supported in current context. |
| **1000** | Permissions denied by user. |
| **2000** | Network issue. |
| **3000** | Underlying hardware doesn't support the capability. |
| **4000** | One or more arguments are invalid. |
| **5000** | User isn't authorized for this operation. |
| **6000** | Couldn't complete the operation due to insufficient resources. |
| **7000** | Platform throttled the request because of API was invoked too frequently. |
| **8000** | User aborted the operation. |
| **9000** | Platform code is old and doesn't implement this API. |
| **10000** | The return value is too big and has exceeded our size boundaries. |

## Limitations

The limitations to add Share to Teams button:

* The Share to Teams button can be hosted or embedded in an app running inside Teams.
* You can add Share to Teams button to the app created by using **Teams Javascript Client SDK**.

## End user Share to Teams experience

After you enable share to teams button on personal app or tab, you can share the content. To access, follow the steps:

1. Open a personal app or tab and select **Share to Teams**.

    :::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="The screenshot shows the Share to Teams button.":::

2. Add other user or group or channel to share the content.

    :::image type="content" source="../../assets/images/share-to-teams/add-recepient.PNG" alt-text="The screenshot shows the steps to add recipient.":::

3. Select **Share**.

   :::image type="content" source="../../assets/images/share-to-teams/add-notes.PNG" alt-text="The screenshot shows the steps to add note.":::

4. Select **View** to reach the conversation where the link was shared.

   :::image type="content" source="../../assets/images/share-to-teams/link-shared.PNG" alt-text="The screenshot shows the steps to select the view button.":::

## See also

* [Share to Teams from web apps](share-to-teams-from-web-apps.md)
* [Create a personal tab](../../tabs/how-to/create-personal-tab.md)
