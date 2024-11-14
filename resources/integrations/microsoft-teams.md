# Microsoft Teams

## Setup Guide

You can find your Microsoft Teams application credentials by visiting the [Microsoft Developer Portal for Teams](https://dev.teams.microsoft.com/).

You'll need the following information to set up your Microsoft Teams app with Paragon Connect:

* App ID
* Bot ID
* Bot Client Secret
* Scopes Requested

### Prerequisites

* A [Microsoft Azure](https://azure.microsoft.com/) account
* A bot registered in the Microsoft Developer Portal for Teams (_See_ [_Creating a Microsoft Teams bot_](microsoft-teams.md#undefined) _for setup instructions_)

### Creating a Microsoft Teams bot

You will need to create a bot user in the [Microsoft Developer Portal for Teams](https://dev.teams.microsoft.com/) to build your integration.

1. Log in to the Developer Portal for Teams using the same Microsoft account that you use to log in to the Microsoft Azure Portal.
2. Navigate to **Tools** in the sidebar.
3. Select **Bot Management**.
4. Click **New Bot** and provide a name for your bot. _This is not the name that appears to your users_; we recommend appending "(Bot)" to the name for clarity.

Next, you will need to associate this new bot with your Teams application.

1. In the Developer Portal for Teams, navigate to **Apps** in the sidebar.
2. If you do not have a Teams app yet, click **New app** and provide a name. This name will be the one displayed in the Microsoft Teams store and to your users.
   1. In **Basic information**, you will need to minimally provide a short description and URLs for your application's website, Privacy Policy, and Terms of Use.
   2. Click **Save** below.
3. In your Teams app settings, navigate to **App features** (under the **Configure** section).
4. Select **Bot**.
5. Select the bot user you created above.
6. Check any applicable capabilities for your bot user.
7. Click **Save** below.
8. Optionally, upload an icon for your app in **Branding**.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

#### Testing your Microsoft Teams bot

If your application is not yet published to the Microsoft Teams store, you can test your app by uploading your app's package directly into your Teams account.

1. In the [Developer Portal for Teams](https://dev.teams.microsoft.com/), navigate to your list of Apps.
2. Click the triple-dot menu in your app's row and click **Download app package**. Your app's package will be downloaded as a .zip file.\
   ![](<../../.gitbook/assets/image (73).png>)
3. Log in to Microsoft Teams with the account you would like to test your bot in.
4. Click **Apps** in the left sidebar (one of the last options):\
   ![](<../../.gitbook/assets/image (14).png>)
5. Click **Manage your apps** (at the bottom of the App categories sidebar).
6. Click **Upload an app** and **Upload your app to your org's app catalog**.&#x20;
7. Select the .zip file with your app's package. After a successful upload, you will be navigated to the "Built for your org" page.
8. Select the name of your app in the list.
9. Click **Add** and **Add to a team**. \
   ![](<../../.gitbook/assets/image (74).png>)
10. Select a team and channel to add your bot.

### Add the Redirect URL to your Microsoft Teams app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Microsoft Teams app:

1. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is `https://passport.useparagon.com/oauth`
2. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/) using your Microsoft account.
3. Navigate to **All Services > App Registrations** and select the app registration _representing your bot, not your Microsoft Teams app_. You can check to make sure that the ID matches the one you selected for your associated bot:\
   \
   _In Developer Portal for Teams > \[Your App] > App Features:_\
   ![](<../../.gitbook/assets/image (67).png>)\
   _In Azure Portal > App Registrations:_\
   ![](<../../.gitbook/assets/image (23).png>)\
   &#x20;
4. Select **Authentication** from the sidebar.
5. Under **Platform configurations**, press the  **"Add a platform"** button.
6. Select the **Web** platform.
7. Paste the Redirect URL from Step 1 under Redirect URIs.
8. Press the **Save** button at the top of the page.

### Generate a Bot Client Secret

Since Microsoft Teams does not automatically provide you with a Bot Client Secret for your application, we'll need to make one. To get your Bot Client Secret:

1. Navigate to **All Services > App Registrations** and select the app registration _representing your bot, not your Microsoft Teams app_. You can check to make sure that the ID matches the one you selected for your associated bot:\
   \
   _In Developer Portal for Teams > \[Your App] > App Features:_\
   ![](<../../.gitbook/assets/image (67).png>)\
   _In Azure Portal > App Registrations:_\
   ![](<../../.gitbook/assets/image (23).png>)
2. Navigate to **Manage > Certificates & secrets** in the sidebar.
3. Under **Client Secrets**, click the **+ New client secret** button.&#x20;
4. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.
5. Copy the displayed Bot Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Bot Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Add your Microsoft Teams app to Paragon

1\. Select **Microsoft Teams** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](microsoft-teams.md#add-the-redirect-url-to-your-microsoft-teams-app) and [Step 2](microsoft-teams.md#generate-a-client-id-and-client-secret) in their respective sections:

* **App/Manifest ID:**  Found in the [Microsoft Developer Portal for Teams](https://dev.teams.microsoft.com/), as the **App ID:**\
  ![](<../../.gitbook/assets/image (47).png>)
* **Bot ID:** Found in the Microsoft Azure Portal, under App registrations > Application (client) ID. This should be the Client ID of the app registration _representing your bot, not your Microsoft Teams app._
* **Bot Client Secret:** See [Generate a Bot Client Secret](microsoft-teams.md#generate-a-bot-client-secret).
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** You should only add the scopes you've requested in your application page to Paragon.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Microsoft Teams applications to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Microsoft Teams

Once your users have connected their Microsoft Teams account, you can use the Paragon SDK to access the Microsoft Teams API on behalf of connected users.

See the Microsoft Teams [REST API documentation](https://docs.microsoft.com/en-us/graph/api/resources/teams-api-overview?view=graph-rest-1.0) for their full API reference.

Any Microsoft Teams API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// List Channels
paragon.request("microsoftTeams", "channels", {
  method: "GET",
});


// Send message in a channel
paragon.request("microsoftTeams", "channels/<channel-id>/messages", {
  method: "POST",
  body: { "content": "Hello World!" }
});
```

## Building Microsoft Teams workflows

Once your Microsoft Teams account is connected, you can add steps to perform the following actions:

* Send message in channel
* Send message in chat

When creating messages in Microsoft Teams, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Sending messages to Microsoft Teams using Paragon Connect (1).png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Microsoft Teams account. For example, you might want to trigger a workflow whenever new chats are created in Microsoft Teams to sync your users' Microsoft Teams chats to your application in real-time.

<figure><img src="../../.gitbook/assets/Microsoft Teams triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Microsoft Teams below:

* **Channel Created**
* **Chat Created**
* **Chat Updated**
