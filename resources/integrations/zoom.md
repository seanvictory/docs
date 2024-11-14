---
description: Connect your Zoom app for OAuth in Paragon.
---

# Zoom

## Setup Guide

You can find your Zoom application credentials by visiting your [Zoom developer dashboard](https://marketplace.zoom.us/user/build).

You'll need the following information to set up your Zoom App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* Zoom Developer Account. You can create one [here](https://developers.zoom.us/).
* Zoom OAuth application. Learn more about creating a Zoom OAuth application [here](https://marketplace.zoom.us/docs/guides/build/oauth-app).&#x20;

### Add the Redirect URL to your Zoom app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Zoom app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your [Zoom developer dashboard](https://marketplace.zoom.us/user/build), select your application.

3\. Navigate to **App Credentials > Redirect URL for OAuth**, then paste-in Paragon Connect's redirect URL found in [Step 1](zoom.md#add-the-redirect-url-to-your-zoom-app).

4\. Under **App Credentials > OAuth allow list > Add Whitelist URL**, paste-in Paragon Connect's redirect URL found in [Step 1](zoom.md#add-the-redirect-url-to-your-zoom-app).

![](<../../.gitbook/assets/Adding the Redirect URL to your Zoom app.png>)

### Add your Zoom app to Paragon

1\. Select **Zoom** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations >** **Zoom** **>** **Settings**, fill out your credentials from the end of [Step 1](zoom.md#add-the-redirect-url-to-your-zoom-app) in their respective sections:

* **Client ID:** Found under App Credentials > Client ID on your Zoom App page.
* **Client Secret:** Found under App Credentials > Client secret on your Zoom App page.
* **Permissions:** Select the scopes you've requested for your application. You must add `users:read` in your Zoom and Paragon dashboard.

Press the blue "**Save Changes**" button to save your credentials.

{% hint style="info" %}
**Note:** You should only indicate the scopes you have requested in your Zoom application registration to Paragon. They should match exactly.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Zoom app to Paragon Connect.png>)

## Connecting to Zoom

Once your users have connected their Zoom account, you can use the Paragon SDK to access the Zoom API on behalf of connected users.

See the Zoom [REST API documentation](https://marketplace.zoom.us/docs/api-reference/zoom-api) for their full API reference.

Any Zoom API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Create a Meeting
paragon.request("zoom", "users/me/meetings", {
    method: "POST",
    body: { "topic": "Product Demo Webinar" }
});


//Get Meetings
paragon.request("zoom", "users/me/meetings", {
    method: "GET",
});
```

## Building Zoom workflows

Once your Zoom account is connected, you can add steps to perform the following actions:

* Create Meeting
* Update Meeting
* Get Meeting
* Get Meeting by Meeting ID
* Delete Meeting
* Add Meeting Registrant
* Get Meeting Registrants
* Delete Meeting Registrant

When creating or updating meetings in Zoom, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Generating a Zoom meeting from Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Zoom account. Paragon provides a webhook URL to listen for updates from Zoom to send information to your app. To add the webhook URL to your Zoom app registration and complete its verification, perform the following:

2\. Start in your [Zoom developer dashboard](https://marketplace.zoom.us/user/build), and select your application.

3\. Navigate to **Feature > Add Feature** and turn on **Event subscriptions**.

4\. Copy the **Secret Token** value provided by Zoom.

5\. Navigate back to your integration settings in Paragon. Add the **Secret Token** value to the **Webhook Client Secret**.

6\. Copy the link under "**Webhook URL**" in your integration settings in Paragon. The webhook URL takes the form:

```javascript
https://hermes.useparagon.com/webhook/triggers/connect/zoom/<Integration_ID>
```

4\. Return to Zoom's **Event subscriptions** page and press the `+ Add new event subscription` button.

5\. Under "**Event notification endpoint URL**", paste-in the webhook URL from your integration's `Settings` in Paragon Connect.

6\. Choose the event types that you look to support in **Event types**. These are listed below.

7\. Validate the URL with Zoom by pressing the "Validate" button. There is no need to change the Authentication Header option.

7\. Press `Save` to save your changes once verified.

<figure><img src="../../.gitbook/assets/CleanShot 2024-02-22 at 12.35.54@2x.png" alt=""><figcaption></figcaption></figure>

Once you've added the Event Notification Endpoint URL to your Zoom app, you can access the following triggers in Paragon:

* New Meeting
* Meeting Updated
* Meeting Ended
* New Meeting Registrant
* Meeting Participant Joined
* Meeting Participant Left
* New Recording
* Complete Recording
* Recording Transcript Completed
