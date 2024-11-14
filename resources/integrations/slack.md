---
description: Connect your Slack app for OAuth in Paragon
---

# Slack

## Setup Guide

You can find your Slack app credentials by visiting your [Slack App dashboard](https://api.slack.com/apps).

{% hint style="info" %}
**Note:** You'll need to create a new Slack app if you don't already have one.
{% endhint %}

You'll need the following information to set up your Slack App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Slack app

Paragon provides a redirect URL to send information to your Slack app. To add the redirect URL to your Slack app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log in to your [Slack App dashboard](https://api.slack.com/apps) and select your Slack app.

3\. In your Slack App page sidebar, navigate to **OAuth & Permissions > Redirect URLs**.

4\. Press "**Add New Redirect URL**".

5\. Paste-in the redirect URL from Paragon. The redirect URL can be found in Step 1.

6\. Press "**Add**", then press "**Save URLs**".

![](<../../.gitbook/assets/Adding Slack redirect URL.gif>)

Slack provides you with the **Client ID** and **Client Secret** needed for the next steps after adding the redirect URL to your application. You can find the credentials under **Basic Information > App Credentials** in the Slack app sidebar.

7\. Enable your Slack app in other workspaces. Under **Settings > Managed Distribution > Share Your App with Other Workspaces**, complete the listed steps to allow your Slack app to be installed by your customers.

<figure><img src="../../.gitbook/assets/Enabling Other Workspaces for your Slack app for Paragon Connect.png" alt=""><figcaption></figcaption></figure>

### Add your Slack app to Paragon

1\. Select **Slack** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](slack.md#add-the-redirect-url-to-your-slack-app) in their respective sections:

* **Client ID:** Found under Basic Information > App Credentials > Client ID on your Slack App page.
* **Client Secret:** Found under Basic Information > App Credentials > Client Secret on your Slack App page.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Slack app to Paragon Connect.png>)

## Connecting to Slack

Once your users have connected their Slack account, you can use the Paragon SDK to access the Slack API on behalf of connected users.

See the Slack [REST API documentation](https://api.slack.com/reference) for their full API reference.

Any Slack API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get All Channels
await paragon.request("slack", "/conversations.list", {
  method: "GET"
});

// Send Message to Channel
await paragon.request("slack", "/chat.postMessage", {
  method: "POST",
  body: {
    "channel": "YOUR_CHANNEL_ID",
    "text": "Hello, world",
    "as_user": true
  }
});
```

## Building Slack workflows

Once your Slack account is connected, you can add steps to perform the following actions.

* Send message in channel
* Send DM
* Get User by Email
* Search Messages

When composing your Slack message, you can reference data from previous steps by typing `{{` to invoke the variable menu.

Additionally, you can choose whether to send a message as a bot or yourself. If you choose to send as a bot, you can choose to give your bot a custom name and icon.

![](<../../.gitbook/assets/Selecting Slack App Authentication in Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Slack account. For example, you might want to trigger a workflow whenever new messages are created in Slack to sync your users' Slack messages to your application in real-time.

<figure><img src="../../.gitbook/assets/Slack Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Slack below:

* **Direct Message Created**
* **Channel Created**
* **Direct Message Sent**
* **File Deleted**
* **Group Message Sent**
* **Channel Message Sent**
* **Direct Message Updated**
* **Group Message Updated**
* **Channel Message Updated**
* **App Mentioned**
* **New Message Reaction**
* **Message Reaction Removed**
* **Message Interaction**

### **Add the Request URL to your Slack app**

Paragon provides a request URL to subscribe your Slack app to events in Slack. To add the request URL to your Slack app:

1.  In the Settings tab of your Slack integration in Paragon, copy the link under "**Webhook URL".**\


    <figure><img src="../../.gitbook/assets/CleanShot 2023-11-17 at 13.34.12@2x.png" alt="" width="563"><figcaption></figcaption></figure>
2. Log in to your [Slack App dashboard](https://api.slack.com/apps) and select your Slack app.
3. In your Slack App page sidebar, navigate to **Event Subscriptions > Enable Events**.
4. Provide the "**Request URL**." Paragon will automatically respond to Slack's `challenge` request and begin listening to events on behalf of your app.&#x20;
5. Click **Save Changes** at the bottom of the Slack App dashboard.

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-17 at 13.38.38@2x.png" alt="" width="563"><figcaption></figcaption></figure>
