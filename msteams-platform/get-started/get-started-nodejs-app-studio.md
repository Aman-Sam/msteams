---
title: Tutorial - Create your first app using Node.js
description: Learn how to get started building Microsoft Teams apps with Node.js.
keywords: getting started node.js nodejs App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
---

# Build your first Microsoft Teams app using Node.js

In this tutorial, you will learn how to build your very first Microsoft Teams app using Node.js. It also walks you through the steps to: 

1. [Prepare your environment](#prepare-environment)
1. [Get prerequisites](#GetPrerequisites)
1. [Download the sample](#DownloadSample)
1. [Build and run the sample](#BuildRun)
1. [Host the sample app](#HostSample)
1. [Update the credentials for your hosted app](#updatecredentials)
1. [Configure the app tab](#ConfigureTheAppTab)

<a name="prepare-environment"></a>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

### Download and host your app

Follow these steps to download and host a simple "hello world" app in Teams.

<a name="GetPrerequisites"></a>

## Get prerequisites

To complete this tutorial, you need the following tools. If you don't already have them you can install them from these links.

- [Git](https://git-scm.com/downloads)
- [Node.js and NPM](https://nodejs.org/)
- Get any text editor or IDE. You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.

If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, select the options. 

Verify that the tools are available by running the following in a terminal window:

> [!NOTE]
> Use the terminal window that you are most comfortable with on your platform. These examples use Bash (which is included in Git), but these scripts will run on most platforms.

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

You may have a different version of these applications. This should not be a problem, except for gulp. For gulp you'll need to use version 4.0.0 or later.

If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.

If you have installed Visual Studio Code, you can verify the installation by running:

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

You can continue to use this terminal window to run the commands that follow in this tutorial.

<a name="DownloadSample"></a>

## Download the sample

We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) sample to get you started. In a terminal window, run the following command to clone the sample repository to your local machine:

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.

<a name="BuildRun"></a>

## Build and run the sample

After the repository is cloned, run the change directory command in terminal to change the directory to the sample:

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

In order to build the sample, you need to install all its dependencies. Run the following command to do this:

```bash
npm install
```

You should see a bunch of dependencies getting installed. After installation you can run the app with the following command:

```bash
npm start
```

When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.

> [!NOTE]
> If you see a different port number displayed in the message above, it is because you have a PORT environment variable set. You can continue to use that port or
> change your environment variable to 3333.

At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

## Deploy your sample app

Remember that apps in Microsoft Teams are web applications exposing one or more capabilities. For the Teams platform to load your app, your app must be reachable from the internet. To make your app reachable from the internet, you need to *host* your app.

For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint. [ngrok](https://ngrok.com) is a free tool that lets you do just that. With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example). You can [download and install](https://ngrok.com/download) *ngrok* for your environment. Make sure you add it to a location in your `PATH`.

After you install it, you can open a new terminal window and run the following command to create a tunnel. The sample uses port 3333, so be sure to specify it here:

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333. You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page. Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.

> [!NOTE]
> If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.
> [!TIP]
> It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun. The *ngrok* session will return useful debugging information in this window.

There is a paid version of *ngrok* that allows persistent names. If you use the free version your app will only be available during the current session on your development machine. If the machine is shut down or goes to sleep the service will no longer be available. Remember this when sharing the app for testing by other users. If you have to restart the service it will return a new address and you will have to update every place that uses that address.

Make a note of the URL of your app. You will need this later when you register the app with Teams using App studio or Developer Portal.

<a name="DeployToTeams"></a>

## Deploy your app to Microsoft Teams

At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called. To do this you now have to create an app package. This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app. You can manually create this app package, or you can use App Studio or Developer Portal, tools that run in Teams, that will simplify the process of registering the app. App Studio and Developer Portal are the recommended ways of creating and updating the app package.

For either method you will need the following:

- The URL where your app can be found on the internet.
- Icons that Teams will use to brand your app. The sample comes with placeholder icons located in "src\static\images. App Studio also will provide default icons if needed.

**Update the app package**

# [App Studio](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# [Developer Portal](#tab/DP)

**To install Developer Portal (preview) in Teams**

1. Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. Select **Developer Portal** and select **Open**.

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. Select the Apps tab and select **Import an existing app**.

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. Select **Hello World** and select **Import**. The **Hello World** app is imported in Developer Portal. 

    You can configure your app using the Teams Developer Portal. The Manifest is found under Distribute. You can use the Manifest to configure capabilities, required resources, and other important attributes for your app. For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>

---
<a name="updatecredentials"></a>

## Update the credentials for your hosted app

The sample app requires the following environment variables to be set to the values you made a note of earlier:

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

How you do that differs depending on how you hosted your app. The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.

If you are running the app using ngrok you'll need to set up some local environment variables. There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

Where:

MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.
NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.
NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).

> [!Note]
> If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.

<a name="ConfigureTheAppTab"></a>

## Configure the app tab

After you install the app into a team, you will need to configure it to show content. Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list. You will then be presented with a configuration dialog. This dialog will let you choose which tab to display in this channel. After you select the tab and click **Save** you can see the `Hello World` tab loaded with the tab you chose:

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### Test your bot in Teams

You can now interact with the bot in Teams. Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message. This is called an **\@mention**. Whatever message you send to the bot will be sent back to you as a reply:

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### Test your messaging extension

**To test your messaging extension**
1. Select the three dots below the input box in your conversation view. A menu with the **'Hello World'** app is displayed.
1. Select the menu. A set of random texts is displayed. You can select one of the random text and that is inserted into your conversation.

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Select one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom:

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

 ## See also

* [Tutorials Overview](code-samples.md)
* [Create a conversational bot app](first-app-bot.md)
* [Create a messaging extension](first-message-extension.md)
* [Code Samples](https://github.com/OfficeDev/Microsoft-Teams-Samples)