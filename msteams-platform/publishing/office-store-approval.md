---
title: Microsoft Teams app approval process guidance
description: Describes the approval process for getting your app published to the Microsoft Teams app store
keywords: teams publish store office publishing AppSource
---
# Microsoft Teams app approval process guidance

Teams app approval is a free service provided by AppSource that verifies that your app works as described, contains all appropriate metadata, and provides content that would be valuable to an end user. For rapid approval, follow our [checklist](#checklist-for-rapid-approval).

For your Teams app to be approved:

* It must not contain inadmissible or offensive material.
* It must be stable and functional.
* Any material that you associate with your experience, such as descriptions and support documentation, must be accurate. Use correct spelling, capitalization, punctuation, and grammar in your descriptions and materials.
* It must pass all current [AppSource validation policies](https://dev.office.com/officestore/docs/validation-policies) for Teams tabs and bots. Please note that these policies are subject to change.
* For tabs, it must provide value to users outside of what is possible by simply pinning your website in Teams. This means that, at minimum, it must remove extraneous chrome and disallow navigating outside the configured context. See the [Microsoft Teams Design Guidelines](~/resources/design/overview.md) for more guidance.

When the validation process is complete, you will receive a message to let you know that either your Teams experience is approved or it fails one of the stated policies. You can also follow these steps to check the approval status in the Seller Dashboard:

1. Sign in to the Seller Dashboard.
2. On the **manage** tab, your submission status appears under the submission name.
   * If the status is **pending approval**, your submission is still being verified. When it is in this state, you can't update or resubmit it.
   * If the status is **changes requested**, your submission needs changes before approval. Select your submission; on the summary page, choose **View the add-in report** for details about the required changes.
   * If the status is **approved**, your submission will be listed in the appropriate marketplaces, typically within 24 hours.

Failures are explained, with references to the specific policy violations. All failures must be addressed before resubmission. Be sure to resubmit your app using the tile on the Overview tab. Do not use the *Add a new app* button.

## Checklist for rapid approval

The information below covers some of the most common reasons apps fail validation. It is not intended to be an exhaustive list of all potential issues with you app. However, if you follow this guidance your likelihood of a first-time pass will be greatly increased.

### Sign up, Sign in, and Sign out

Apps must provide a clear, simple sign in/out and (when appropriate) sign-up experience. The experience must be reachable across all capabilities in your app.

* If there is a sign-in option, there must be a sign-out option, even if the app is using SSO/Silent Authentication.
* The sign-out option must sign them out of only the capability, not the Teams client.
* The sign-out behavior has to be consistent with the sign-in behavior.
* Make sure there is always a way to reverse the following (or similar) behaviors:
  * Sign-in => sign-out
  * Link an account/service => un-link an account/service
  * Connect an account/service => disconnect the account/service
  * Authorize an account/service => de/un-authorize the account/service
  * Register an account/service => un-register the account/service
* If your app requires an account or service, you must provide a way to sign-up or request sign-up.

For additional information on authentication see:

* [Authentication documentation](~/concepts/authentication/authentication.md)
* [Bot authentication sample in Node](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Tab authentication sample in Node](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Tab/bot authentication in C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### Test Notes for validation/approval

You must provide at least two login credentials, one admin and one not, so we can validate your app.

* The accounts you provide should have sufficient data pre-populated for verification purposes.
* For enterprise apps, apps where a subscription is required, or where there is an office 365 tenant/domain dependency for testing you must provide an 3rd account in the same domain that is not already configured to use your app so we can validate the first-run user experience.
* If your app has any Premium/Upgraded features, an account with the necessary access must be provided to test that experience.

### Updating your existing Teams app

* Do not use the *Add a new app* button to resubmit your app. Use the tile for your app on the Overview tab instead.
* The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.
* Increment your version number in your manifest.

### App metadata

Make sure your app descriptions and screenshots follow the [AppSource guidance](/office/dev/store/create-effective-office-store-listings).

* Don't use "Teams", "Microsoft", or "app" in your app name.
* The developerName in the App Manifest must be same as the Provider Name defined in Seller Dashboard.
* Make sure the app description, screenshots, text, and promotional images describe only the app and do not contain any additional advertising, promotions or copyrighted brand names.
* If your product requires an account on your service or another service, list that in the description and ensure there are links to sign up, sign in and sign out.
* If your product requires additional purchases to function properly, list that in the description.
* Provide the requisite Terms and Privacy policy links in the manifest and the Seller Dashboard. Verify that the links properly resolve to the correct documentation, ideally Teams specific. For bots, you must provide this same information in the Submission section of the Bot Framework registration page.
* Ensure that metadata in the manifest roughly matches metadata in the Seller Dashboard (and, for bots, in the Bot Framework registration). Note that your Seller Dashboard entry should contain a more detailed and formatted description for use in the AppSource product page.

### Help and configuration pages

It is highly recommended to have help/FAQ link for your Teams app and to provide this link in first-run user experience. For all personal apps we recommend you provide your help page as a personal tab for ease of discovery.

### Privacy policy, terms of use and support URLs

* The Privacy policy can be specific to your app/add-in or can be an overall privacy policy for all the services from a developer. There should be no broken links and no beta or staging URLs. If you use a generic privacy policy, it must reference "Services/Applications/Platforms", and not just "Website".
* Privacy policy should cover how you handle user data storage, data retention, and security controls information.
* Your privacy policy must have your contact information.
* Your support URL should not require authentication before contacting you for any issues with your app.

### Bots and messaging extensions

* Be sure that your bot provides appropriate responses when mentioned (@*botname*) in a channel and in personal conversations as needed. If your bot does not provide meaningful context within the personal or teams scope, disable that scope via the manifest. (See the `bots` block in the [Microsoft Teams manifest schema reference](~/resources/schema/manifest-schema.md#bots).)
* Your bot should respond to invalid commands with help content. For example "I'm sorry, I don't understand. Type "help" for more information."
* Your bot must include a help command that provides your value proposition and valid commands.
* For bots, a response to a user command must occur within two seconds. If longer processing is required, you must use a typing indicator.
* For messaging extensions, a response to a user command must occur within five seconds.

### Tabs

* For your tab configuration page, be sure to provide "About" links and proper guidance. This page is the first thing the user sees, so ensure that a new user understands what to do.
* If a response to an action takes more than three seconds, you must provide a loading message or warning.

### Miscellaneous

* Check your manifest for completeness and accuracy. Then check it again.
* Do not make changes to your app while validation is in progress. This will require a complete re-validation of your app.
* Your app  must not stop responding, end unexpectedly, or contain programming errors. If there is an issue it should fail gracefully with a valid message to user.
* Your app must not automatically download or install or launch other executable code on the user's environment.
