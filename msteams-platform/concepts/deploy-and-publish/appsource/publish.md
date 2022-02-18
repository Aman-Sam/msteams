---
title: Overview - Teams app store publishing process
description: Describes the process for submitting your app to Partner Center and getting it published to the Microsoft Teams store (and AppSource).
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: high
---
# Publish your app to the Microsoft Teams store

You can distribute your app directly to the store inside Microsoft Teams and reach millions of users around the world. If your app is also featured in the store, you can instantly reach potential customers.

Apps published to the Teams store also automatically list on [Microsoft AppSource](https://appsource.microsoft.com), which is the official marketplace for Microsoft 365 apps and solutions.

## Understand the publishing process

When you feel your app is production ready, you can begin the process of getting it listed on the Teams store.

> [!TIP]
> Following the pre-submission steps closely can increase the possibility that Microsoft approves your app for publishing.

:::row:::
   :::column span="":::
      
   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Teams app store publishing process" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::
      
   :::column-end:::
:::row-end:::

1. [Review the Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) to ensure your app meets Teams app and store standards.

1. [Create a Partner Center developer account](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md).

1. [Prepare your store submission](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md), which includes running automated tests, compiling test notes, creating a store listing, among other important tasks to help expedite the review process.

1. [Submit your app](/office/dev/store/add-in-submission-guide) through Partner Center.

1. If your submission fails, work with Microsoft directly to [resolve the issues and resubmit your app](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md).

## What to expect after you submit your app?

* **Deep functional and experience tests**

  Your app is thoroughly reviewed by a validator to ensure compliance with the [Microsoft Commercial Marketplace certification policies](/legal/marketplace/certification-policies) with a focus on deep functional and user experience testing, usability checks, and metadata checks. App validation is performed across desktop, web, and mobile clients.

* **Guided app publish through concierge service**

  If there are no issues observed with your app, your app will be approved and published to the Teams store. If there are issues, you'll receive an automated validation report from Partner Center with the failure details. To help you successfully publish your app to the Teams store and guide you through this process, the validation team will send you a personalized email from our concierge service [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) that includes the following information:

   * Summary of all issues

   * Details of failures or issues with policy links and categorization: 

     * Mandatory fix: These issues must be fixed prior to app approval.

     * Suggested fix: These issues can be fixed post app approval as these are recommendations to improve your app’s experience.

     * Blocker: These issues prevent the validation team from testing your app functionality further and must be resolved for validation to continue.

     * Query: These queries can be shared to get answers to specific questions related to your app.

   * Steps to recreate issues through written instructions or video format.

   * Recommendations to fix the reported issues with links to guidance docs.
 
  After you've reviewed the list of issues, fix all the reported issues and share the updated app package over email, for the validation team to re-validate your app thoroughly. If you've any queries related to the reported issues, contact the validation team at [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com).

  If there are issues remaining or regression issues observed in your app, the validation team will share an updated validation report with you. If your app had blockers, you might see new issues reported when your app is validated after the blockers are resolved. Sometimes, the validation team has also noticed regression issues in apps post deployment of fixes. It takes a few re-submissions to close all the issues for an app that consists of bugs, and get it approved to publish to the Teams store.

  After all reported issues are closed and final submission is made in the Partner Center, the validation team will approve and publish your app. Allow at least one business day for the app to be available in the Teams store.

## Tips for rapid approval to publish your app

* **During design phase**

  Review the [store validation guidelines](prepare/teams-store-validation-guidelines.md) early in your app's life cycle (design phase) to ensure that you build your app in alignment with the store requirements. If you build your app in line with these guidelines, this will prevent any rework due to non-adherence to store policies.

* **Prior to app submission**

  1. [Create your Partner Center account](prepare/create-partner-center-dev-account.md) well in advance. If you run into any challenges with your [Partner Center account](prepare/create-partner-center-dev-account.md), create a [support ticket](/azure/marketplace/partner-center-portal/support).

  1. Review the [store validation guidelines](prepare/teams-store-validation-guidelines.md) again to ensure that your app is in alignment with the store requirements. This helps reduce the number of issues observed in your app and consequently, the time taken to approve your app.

  1. Test and re-test your app:

     1. Validate your app package using the Teams [Developer Portal](https://dev.teams.microsoft.com/home) to identify and fix any package errors.

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="Teams store app validation in Developer Portal" lightbox="../../../assets/images/submission/teams-validation-developer-portal.png":::
 
     1. Self-test your app thoroughly prior to app submission to ensure it adheres with store policies. Sideload the app in Teams and test the end-to-end user flows for your app. Ensure the functionality works as expected, links aren't broken, user experience isn't blocked, and any limitations are clearly highlighted.

     1. Test your app across desktop, web, and mobile clients. Ensure that the app is responsive across different form factors.

  1. Complete [publisher verification](/azure/active-directory/develop/publisher-verification-overview) before you submit your app. If you run into any issues, you can create a [support ticket](/azure/marketplace/partner-center-portal/support) for resolution.

  1. As you prepare for app submission, [follow the checklist](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist) and include the following details as part of your submission package:

      1. Thoroughly verified app package.

      1. Working admin and non-admin user credentials to test your app functionality (if your app offers a premium subscription model).

      1. Test instructions detailing app functionality and supported scenarios.

      1. Setup instructions if your app requires additional configuration to access app functionality. Alternately, if your app requires complex configuration, you can also provide a [provisioned demo tenant](/office/developer-program/microsoft-365-developer-program-get-started) with admin access so that our validators can skip the configuration steps.

      1. Link to a demo video recording key user flow for your app. This is highly recommended.

* **Post app submission**

  * After you’ve reviewed the validation report, reply to the email thread with any queries related to the validation report or if you need any additional support to resolve the reported issues.

  * Ensure that you've adequate developer bandwidth to resolve any reported issues till the app is approved.

  * Ensure that you've [resolved all issues](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues) reported to you by the concierge service [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) before sharing your app package for further testing. This helps reduce the number of iterations required to validate your app and consequently, the time taken to approve your app.
  
  * Avoid changing app functionality during the validation process. This might lead to discovery of new issues and increase the time it takes to approve your app.

## See also

* [Publishing to Microsoft 365 App Stores](/office/dev/store/)
* [Upload your Teams app](~/concepts/deploy-and-publish/apps-upload.md)
* [Publish your Teams app to your org](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [Plan onboarding experience for users](../../design/understand-use-cases.md#plan-the-onboarding-experience)
* [Distributing tab apps on mobile](../../../tabs/design/tabs-mobile.md#distribution)
* [Test preview for monetized apps](prepare/Test-preview-for-monetized-apps.md)
