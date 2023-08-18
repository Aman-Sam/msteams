---
title: Microsoft Teams updates
description: Learn about the latest updates to Microsoft Teams.
author: v-ypalikila
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: reference
---
# Microsoft Teams update

[The new Microsoft Teams client](https://www.microsoft.com/en-us/microsoft-365/blog/2023/03/27/welcome-to-the-new-era-of-microsoft-teams/) is reimagined from the ground up with performance in mind. It's faster, simpler, smarter, and flexible to provide better experience for your apps and users. The new Teams client supports all the existing Teams app capabilities except Adaptive Card tabs. If you have an app that runs inside the Classic Teams, the app will most likely run in the new Teams client without any issues.

The following are the advantages of the new Teams client:  

* The new Teams client uses the Evergreen version of Microsoft Edge WebView2 to ensure Teams client is always up to date with the latest fixes and improvements available in Microsoft Edge and Chromium.

* The new Teams client has been rebuilt from the ground up with performance in mind and includes all the platform infrastructure responsible for bootstrapping your app and powering the SDK APIs that it uses.  

You can use the following property to identify your app usage in the new Teams or Classic Teams client:

* For TeamsJS v1.x: [`hostName`](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest#@microsoft-teams-js-context-hostname&preserve-view=true)
* For TeamsJS v2.x: [`AppHostInfo`](/javascript/api/@microsoft/teams-js/app.appinfo?view=msteams-client-js-latest&preserve-view=true#@microsoft-teams-js-app-appinfo-host)

> [!NOTE]
> If hostName isn't defined, then assume that your app is running in the Classic Teams client.

The new Teams or Classic Teams client are represented using the `teams` and `teamsModern` fields, respectively.

## Timelines and rollout

To ensure a smooth transition, a phased rollout of the new platform is planned as follows:

* **Developer Preview**: The new Teams client is available in Public Developer Preview starting June 2023. You can access the new platform and test your apps. We encourage you to adopt the feature early and provide feedback to help refine the platform.

* **Availability of all platform features from Classic Teams**: All the platform features from Teams classic will be available in the new Teams client by August 2023.

## Known issues

> [!NOTE]
>
> * We recommend to test apps, tabs, messaging extensions, bots, and link unfurling after switching from the Classic Teams client to the new Teams client.
> * Adaptive Card tabs aren't supported in the new Teams client. If your app is using Adaptive Card tabs, we recommend to rebuild the tab as a web-based tab. For more information, see [Build tabs for Teams](../tabs/how-to/build-adaptive-card-tabs.md).

**Teams features that will be supported soon**

* [Share in Teams](../concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md).

* [Sideloading of apps](../concepts/deploy-and-publish/apps-upload.md) isn't supported in the new Teams client. You can sideload an app in the Classic Teams client and use it in new Teams client.

For more information on known issues and gaps in the new Teams client, see [new Microsoft Teams](/microsoftteams/new-teams-desktop-admin?tabs=teams-admin-center#known-issues).

If your app is working fine in the Classic Teams client but has issues in the new Teams, then raise an issue on [this page](https://github.com/MicrosoftDocs/msteams-docs/issues/new?title=&body=%0A%0A%5BEnter%20feedback%20here%5D%0A%0A%0A---%0A%23%23%23%23%20Document%20Details%0A%0A%E2%9A%A0%20*Do%20not%20edit%20this%20section.%20It%20is%20required%20for%20learn.microsoft.com%20%E2%9E%9F%20GitHub%20issue%20linking.*%0A%0A*%20ID%3A%2019ddf42e-0a47-7717-52d4-e549155480a2%0A*%20Version%20Independent%20ID%3A%204bbe9beb-233f-cfd5-097b-f280aab5fde8%0A*%20Content%3A%20%5BMicrosoft%20Teams%20developer%20community%20support%20and%20feedback%20-%20Teams%5D(https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fmicrosoftteams%2Fplatform%2Ffeedback)%0A*%20Content%20Source%3A%20%5Bmsteams-platform%2Ffeedback.md%5D(https%3A%2F%2Fgithub.com%2FMicrosoftDocs%2Fmsteams-docs%2Fblob%2Fmain%2Fmsteams-platform%2Ffeedback.md)%0A*%20Service%3A%20**msteams**%0A*%20GitHub%20Login%3A%20%40surbhigupta%0A*%20Microsoft%20Alias%3A%20**lajanuar**). For any other issues, request you to raise an issue on [support and feedback](../feedback.md#developer-community-forums).

## See also

[Teams app that fits](../overview.md)
