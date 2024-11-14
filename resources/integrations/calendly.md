---
description: Connect to your users' Calendly accounts.
---

# Calendly

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new Calendly app if you don't already have one.
{% endhint %}

You can find your Calendly app credentials in your [Calendly Developer Account.](https://developer.calendly.com/api-docs/4b402d5ab3edd-calendly-developer)

You'll need the following information to set up your Calendly App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Calendly app

Paragon provides a redirect URL to send information to your Calendly app. To add the redirect URL to your Calendly app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log into your [Calendly Developer Portal](https://developer.calendly.com/).

3\. Select your app from the list of apps.

5\. Under **Redirect URLs**, paste-in the redirect URL from Paragon. The redirect URL can be found in Step 1.

6\. Press the `Save` button to confirm your changes.

### Add your Calendly app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Calendly App page.
* **Client Secret:** Found under Client Secret on your Calendly App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Calendly app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Calendly

Once your users have connected their Calendly account, you can use the Paragon SDK to access the Calendly API on behalf of connected users.

See the Calendly [REST API documentation](https://developer.calendly.com/api-docs/4b402d5ab3edd-calendly-developer) for their full API reference.

Any Calendly API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Fetch an organization's events
paragon.request("calendly", "/scheduled_events", {
  method: "GET"
});

// List an organization's or user's event types
paragon.request("calendly", "event_types?organization=<Organization>", {
  method: "GET"
});
  
```

## Building Calendly workflows

Once your Calendly account is connected, you can add steps to perform the following actions:

* Get Event Type Details
* Get Available Times for Event Type
* Search Events
* Get Event by ID
* Get Event Invitees
* Cancel Event

You can also use the Calendly Request step to access any of Calendly's API endpoints without the authentication piece.

When creating or updating records in Calendly, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Calendly account. For example, you might want to trigger a workflow whenever new invitees are created in Calendly to sync your users' Calendly events to your application in real-time.

You can find the full list of Webhook Triggers for ClickUp below:

* **Invitee Created**
* **Invitee Canceled**
