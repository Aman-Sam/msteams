---
title: Apps for Teams meetings
author: surbhigupta
description: In this article, learn how apps works in Microsoft Teams meetings based on participant and user role and app extensibility.
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
---

# Apps for Teams meetings and calls

Meetings enable collaboration, partnership, informed communication, and shared feedback. The meeting space can deliver a user experience for each stage of the meeting lifecycle. The following illustration gives you an idea of the meeting app extensibility features:

<!--
:::image type="content" source="../assets/images/apps-in-meetings/meetingappextensibility.png" alt-text="The screenshot shows you how meeting app extensibility works.":::
-->

[Get participant API](meeting-apps-apis.md#get-participant-api)

:::row:::
    :::column span="":::
           &nbsp; :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/space.png" border="false":::
    :::column-end:::
    :::column span="2":::
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/1-cust-apps.png" border="false" link="build-apps-for-teams-meeting-stage.md":::  :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/2-enable-app.png" border="false":::
    :::column-end:::
        :::column span="":::
           &nbsp; :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/space.png" border="false":::
        :::column-end:::
:::row-end:::
:::row:::
    :::column span="":::

        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/3-create-scene.png" border="false" link="teams-together-mode.md":::
        <br><br><br>
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/5-notification-user.png" border="false" link="in-meeting-notification-for-meeting.md":::
        <br><br><br>
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/7-fetch-participant.png" border="false" link="meeting-apps-apis.md#get-participant-api":::
    :::column-end:::
    :::column span="2":::
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/0-app-extensibility.png" border="false":::
    :::column-end:::
    :::column span="":::
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/4-meeting-lifecycle.png" border="false" link="#meeting-lifecycle":::
        <br><br><br>
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/6-integrate.png" border="false" link="../concepts/build-and-test/share-in-meeting.md":::
        <br><br><br>
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/8-optimize-meeting.png" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="":::
        &nbsp; :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/space.png" border="false":::
    :::column-end:::
    :::column span="2":::
        :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/9-in-meeting.png" border="false"::: :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/10-get-meeting.png" border="false" link="meeting-apps-apis.md#get-real-time-teams-meeting-events-api":::
    :::column-end:::
        :::column span="":::
        &nbsp; :::image type="icon" source="../assets/images/apps-in-meetings/app-extensibility/space.png" border="false":::
    :::column-end:::
:::row-end:::



You must be familiar with the following product concepts to create custom meeting experiences with apps in Microsoft Teams.

## Supported meeting types in Teams

Teams supports access to apps during meeting for the following meeting types:

* [**Scheduled meetings**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): Meetings scheduled through Teams calendar.
* [**Scheduled channel meetings**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop): Meetings scheduled through Teams public channels.
* [**One-on-one calls**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): Calls initiated in one-on-one chat.
* [**Group calls**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798): Calls initiated in group chat.
* [**Instant meetings**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5): Meetings initiated through **Meet now** button in Teams calendar.
* [**Webinar**](https://support.microsoft.com/office/get-started-with-teams-webinars-42f3f874-22dc-4289-b53f-bbc1a69013e3): Webinar initiated through **Webinar** button under **New Meeting** dropdown.

Learn more about [Teams meetings, expiration and policies](/MicrosoftTeams/meeting-expiration) and [meetings, webinars, and live events](/microsoftteams/quick-start-meetings-live-events).
> [!NOTE]
>
> * Apps for scheduled public channel meetings are currently available only in [public developer preview](../resources/dev-preview/developer-preview-intro.md).
> * Apps aren't supported in the following:
>   * [Public Switched Telephone Network (PSTN) Teams calls](/microsoftteams/cloud-voice-landing-page#public-switched-telephone-network-connectivity-options)
>   * [End-to-end encrypted Teams calls](https://support.microsoft.com/office/use-end-to-end-encryption-for-teams-calls-1274b4d2-b5c5-4b24-a376-606fa6728a90)
>   * [Instant channel meetings](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)
>   * Meetings in [shared channel](https://support.microsoft.com/office/what-is-a-shared-channel-in-teams-e70a8c22-fee4-4d6e-986f-9e0781d7d11d)

## Meeting lifecycle

A meeting lifecycle includes pre-meeting, in-meeting, and post-meeting app experience, depending on the user type and user's role in a Teams meeting.

## User types in Teams

Teams supports user types, such as in-tenant, guest, federated or external user in a Teams meeting. Each user type can have one of the [user roles in Teams meeting](#user-roles-in-teams-meeting).

> [!NOTE]
>
> Currently when a third person is added to a one-on-one call, the call is elevated to a group call that means a new session starts. Apps added to the one-on-one call are not available in the group call. However, they can be added again.

The following list details the various user types along with their accessibility:

* **In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant. They're full-time, onsite, or remote employees. An in-tenant user can be an organizer, presenter, or attendee.
* **Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant. Guests are added to the organization’s Azure AD and have same Teams capabilities as a native team member. They have access to team chats, meetings, and files. A guest can be an organizer, presenter, or attendee. For more information, see [guest access in Teams](/microsoftteams/guest-access).
* **Federated or external**: A federated or an external user is a Teams user from another organization who has been invited to join a meeting. Federated users have valid credentials with federated partners and are authorized by Teams. They don't have access to your Teams or other shared resources from your organization. Guest access is a better option for external users to have access to Teams and channels. For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).

    > [!NOTE]
    > Teams users can add apps when they host meetings or chats with other organizations. When an external users share apps to the meeting, all the user can access the app. The host organization's data policies and data sharing practices of the third-party apps shared by that user's organization, will be in effect.

* **Anonymous**: Anonymous users don't have an Azure AD identity and aren't federated with a tenant. The anonymous participants are like external users, but their identity isn't shown in the meeting. Anonymous users can't access apps in a meeting window. An anonymous user can't view the bot logo in the meeting chat. An anonymous user can be a presenter or an attendee, but can't be an organizer.

    > [!NOTE]
    > Anonymous users inherit the global default user-level app permission policy. For more information, see [manage apps](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).

## User roles in Teams meeting

The following are the user roles in a Teams meeting:

* **Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, controls attendee permissions, and starts the meeting. Only users with a Microsoft 365 account and Teams license can be the organizer. A meeting organizer can change the settings for a specific meeting from the [**meeting options**](https://support.microsoft.com/en-us/office/change-participant-settings-for-a-teams-meeting-53261366-dbd5-45f9-aae9-a70e6354f88e).

* **Presenter**: Presenters in a meeting have similar capabilities as the organizer, with the exception of removing an organizer from the session and modifying meeting options for the session.

* **Attendee**: An attendee is a user who is invited to attend the meeting. Attendees have limited capabilities during the meeting.

> [!NOTE]
> Only an organizer or presenter can add, remove, or uninstall apps.

For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

> [!TIP]
>
> * The [default participant settings](/microsoftteams/meeting-policies-participants-and-guests) are determined by an organization's IT administrator. As per default settings, participants joining a meeting have the presenter role.
> * Presenter role isn't available in one-on-one calls.
> * A user who starts the group call from a chat is considered as organizer.

> [!IMPORTANT]
>
> * Currently, third-party apps are available in Government Community Cloud (GCC) but are not available for GCC-High and Department of Defense (DOD) tenants.
> * Third-party apps are turned off by default for GCC. To turn on third-party apps for GCC, see [manage app permission policies](/microsoftteams/teams-app-permission-policies) and [manage apps](/microsoftteams/manage-apps).

## See also

* [Designing your Microsoft Teams meeting extension](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Build tabs for meeting](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Build apps for Teams meeting stage](build-apps-for-teams-meeting-stage.md)
* [Build in-meeting notification for Teams meeting](in-meeting-notification-for-meeting.md)
* [Build extensible conversation for meeting chat](build-extensible-conversation-for-meeting-chat.md)
* [Build apps for anonymous users](build-apps-for-anonymous-user.md)
* [Meeting apps APIs](meeting-apps-apis.md)
* [Enhanced collaboration with Live Share SDK](teams-live-share-overview.md)
* [Custom Together Mode scenes](~/apps-in-teams-meetings/teams-together-mode.md)
* [Get meeting transcripts using Graph APIs](../graph-api/meeting-transcripts/overview-transcripts.md)
* [Instrumenting for Teams app specific analytics](../concepts/design/overview-analytics.md#instrumenting-for-teams-app-specific-analytics)

