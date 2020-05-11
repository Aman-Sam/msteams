---
title: Tips and frequently failed cases 
description: Describes tips for submission and most failed policies 
author: laujan
ms.author: lajanuar
ms.topic: how to
---
# Tips for a successful app submission

This article addresses common reasons submitted apps fail validation. While it's not intended to be an exhaustive list of all potential issues with your app, following this guide will increase the likelihood that your app submission will pass the first time. *See* [Commercial marketplace certification policies](/legal/marketplace/certification-policies) for an extensive list of validation policies.

>[!NOTE]
>**[Section 1140](/legal/marketplace/certification-policies#1140-teams)** is specific to Microsoft Teams and **[sub-section 1140.4](https://docs.microsoft.com/legal/marketplace/certification-policies#11404-functionality)** addresses functionality requirements for Teams apps.

## Validation guidelines

### &#9989; General considerations

*See also* [Section 100 — General](/legal/marketplace/certification-policies#100-general)

* Ensure you are using version 1.4.1 or later of the [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js).
* Don't make changes to your app while the validation process is in progress. Doing so will require a complete revalidation of your app.
* Your app  must not stop responding, end unexpectedly, or contain programming errors. If an issue is encountered, your app should fail gracefully and provide a valid-way-forward message to the user.
* Your app must not automatically download, install, or launch any executable code in the user environment. All downloads should seek explicit permission from the user.
* Any material that you associate with your experience, such as descriptions and support documentation, must be accurate. Use correct spelling, capitalization, punctuation, and grammar in your descriptions and materials.
* Provide help and support information. It's highly recommended that your app include a help/FAQ link for the first-run user experience. For all personal apps, we recommend providing your help page as a personal tab for a better user experience.
* Increment your app version number in the manifest if you make any manifest changes to your submission.

### &#9989;  Provide a clear and simple sign in/sign out and sign-up experience

*See also* [Section 1100.5 — Customer control](/legal/marketplace/certification-policies#11005-customer-control)

* If your app or add-in depends on external accounts or services, the sign in/sign out and sign-up experience must be apparent and reachable across all capabilities in your app.
* If there is an explicit sign-in option provided to the user, there must be a corresponding sign-out option (even if the app is using SSO/[silent authentication](~/tabs/how-to/authentication/auth-silent-aad.md)).
* The sign-out option must only sign the user out of your app's capability and not out of the Teams client.
* At a minimum, the sign-out option must sign the user out of the same capabilities accessed with the sign-in option. For example, if the sign-in option includes both a messaging extension and tab, then the sign-out option must include both the messaging extension and tab.

* Make sure there is always a way to reverse the following (or similar) behaviors:
  * Sign-in => sign-out.
  * Link an account/service => unlink an account/service.
  * Connect an account/service => disconnect an account/service.
  * Authorize an account/service => deauthorize/deny an account/service.
  * Register an account/service => unregister/unsubscribe an account/service.
* If your app requires an account or service, you must provide a way for the user to sign up or to create a sign-up request. An exception may be granted if your app is an Enterprise application.
* Sign in/sign out functionality must work on mobile clients. Ensure you're using the [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js) version 1.4.1 or later.

For additional information on authentication see:

* [Authentication documentation](../../../authentication/authentication.md)
* [Bot authentication sample in Node](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Tab authentication sample in Node](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Tab/bot authentication in C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### &#9989; Response times must be reasonable

* **Tabs**. If a response to an action takes more than three seconds, you must provide a loading message or warning.
* **Bots**. A response to a user command must occur within two seconds. If longer processing is required, your app must display a typing indicator.
* **Compose extensions**. A response to a user command must occur within five seconds.

> [!TIP]
> Make sure your app displays a loading indicator or some form of warning when your app is taking longer than expected to respond.

### &#9989; Tab content should not have excessive chrome or layered navigation

* Tabs should provide focused content and avoid needless UI elements. In general, this usually refers to unnecessary nested/layered navigation, an extraneous or irrelevant UI next to the content, or any links that take the user to unrelated content. For example, below is a tab view that omits navigation menus and only showcases the main content:

![SharePoint web view](~/assets/images/faq/web-sp.png)
![SharePoint tab view](~/assets/images/faq/tab-sp.png)

* If there are multiple view options, consider having a tab config menu for the user to choose from. For example, instead of embedding a menu inside the tab, put the menu in the configuration page so the actual tab view is clean and focused.

![Wide idea configuration page](~/assets/images/faq/wideidea.png)

### &#9989; Tab configuration must happen in the configuration screen

* The configuration screen should clearly explain the value of the experience and how to configure the tab.
* The configuration process should not dead-end the user experience and always provide a way for users to continue.
* A user should always be able to finish the configuration experience, even if they can’t immediately find the content they’re looking for.
* The configuration experience should provide options for the user to find their content, pin a URL, or create new content if it doesn’t exist.
* The user shouldn’t have to leave the configuration experience to create content and then come back to Teams to pin it.

![OneNote allows users to paste a OneNote link in case notes can not be found](~/assets/images/faq/tab-onenote-config.png)

![Users can always create new plan on planner in case there no existing ones](~/assets/images/faq/tab-planner-config.png)

![SharePoint also allows user to directly paste a SharePoint link](~/assets/images/faq/tab-sp-config.png)

### &#9989; Bots must always be responsive and fail gracefully

Your bot should be responsive to any command and not dead-end the user. Here are some tips to help your bot intelligently respond to users:

* **Use command lists**. Analyzing user input or predicting user intent is hard. Instead of letting users guess what your bot can do, provide a list of commands your bot understands.

![Flow command list](~/assets/images/faq/flow-bot.png)

* **Include a help command**. Users are likely to type "Help" when they are lost or when your bot doesn't respond as expected. Include a help command that describes how your app's value will be experienced along with all valid commands.

![Flow help command](~/assets/images/faq/flow-help.png)

* **Include help content or guidance when your bot is lost**. When your bot can't understand the user input, it should suggest an alternative action. For example, *"I'm sorry, I don't understand. Type "help" for more information."* Don't respond with an error message or simply, *"I don't understand"*. Use this chance to teach your users.

* **Think through all scopes**. Be sure that your bot provides appropriate responses when mentioned (`@*botname*`) in a channel and in personal conversations. If your bot does not provide meaningful context within the personal or teams scope, disable that scope via the manifest. (See the `bots` block in the [Microsoft Teams manifest schema reference](~/resources/schema/manifest-schema.md#bots).)

### &#9989; Bots must send a welcome message on first launch

Welcome messages are the best way to set your bot's tone. This is the first interaction a user has with the bot. A good welcome message can encourage the user to keep exploring the app. If the welcome or introductory message is confusing or unclear, users won't see the value of the app immediately and lose interests. The welcome message must include the following:

* A help command.
* The value proposition
* All valid commands.

Here are a few considerations when designing your welcome message:

#### Personal Scope

* **Make your message concise and informative**. Most likely, users' experiences with and knowledge of your app will vary. They might have used your app on another platform or know nothing about your app. You want to tailor your message to all audiences and in a couple sentences explain what your bot does and the ways to interact with it. You should also explain the value of the app and how the users will benefit from using it.
![Cafe and Dinning bot](~/assets/images/faq/cafe-bot.png)

* **Make your message actionable**. Think about the first thing you want users to do after installing your app. Is there a cool command they should try? Is there another onboarding experience they should know about? Do they need to sign in? You can add actions on an adaptive card or provide specific examples such as *“Try asking….”*, *“This is what I can do…”*.

#### Team scope

Things are a little bit different when the bot is first added to a channel. Normally, you shouldn't send a 1:1 message to everyone on the team, but the bot can send a welcome message in the channel.

> [!div class="nextstepaction"]
> [Learn more about Teams app approval policies](/legal/marketplace/certification-policies#1140-teams) 
