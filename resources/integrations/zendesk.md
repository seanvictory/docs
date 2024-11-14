# Zendesk

## Setup Guide

You can find your Zendesk app credentials by visiting your [Zendesk Developer App Console](https://www.zendesk.com/).

You'll need the following information to set up your Zendesk app with Paragon:

* Client ID
* Client Secret

### Add the Redirect URL to your Zendesk app

Paragon provides a redirect URL to send information to your Zendesk app. To add the redirect URL to your Zendesk app:



1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your Zendesk dashboard, click the gear icon on the left.

3\. Under **Channels > API > OAuth Clients**, click the "Add OAuth Client" button.

![](<../../.gitbook/assets/Accessing Zendesk OAuth Clients.gif>)

4\. Fill out your **Client Name** and **Description**.

5\. Under "**Redirect URLs**", paste the Redirect URL from Paragon.&#x20;

6\. Set the "**Client Kind"** to **Confidential**

7\. Press the **Save** button.

8\. Scroll down to the bottom of the page to copy your **Secret**. We'll use this in the next step.

{% hint style="warning" %}
Your OAuth app created with the steps above will _only_ work in your own test Zendesk account sandbox until steps to [“globalize”](zendesk.md#publishing-your-zendesk-application) the app are followed. Refer to the [instructions](zendesk.md#publishing-your-zendesk-application) for enabling the _global_ app.
{% endhint %}

### Add your Zendesk app to Paragon

1\. Select Zendesk from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from the end of [Step 1](zendesk.md#add-the-redirect-url-to-your-zendesk-app) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

## Using the Paragon SDK for Zendesk

Once your users have connected their Zendesk account, you can use the Paragon SDK to access the Zendesk API on behalf of connected users.

See the Zendesk [REST API documentation](https://developer.zendesk.com/rest\_api/docs/support/introduction) for their full API reference.

Any Zendesk API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// List tickets
await paragon.request("zendesk", "v2/tickets", {
    method: "GET",
});
```

## Building Zendesk workflows

Once your Zendesk account is connected, you can add steps to perform the following actions:

* Create Ticket
* Update Ticket
* Add Comment to Ticket
* Search Tickets
* Get Ticket by ID
* Get Users

When creating or updating tickets in Zendesk, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Zendesk account. For example, you might want to trigger a workflow whenever new tickets are created Zendesk to sync your users' Zendesk tickets to your application in real-time.

![](<../../.gitbook/assets/Zendesk Webhook Triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Zendesk below:‌

* **New Ticket**
* **Ticket Updated**

## Publishing your Zendesk Application

A _global_ OAuth application registration is required with Zendesk in order to allow connections from Zendesk users outside of your Zendesk organization. Follow the steps provided by Zendesk's developer documentation for [publishing your Zendesk Application](https://developer.zendesk.com/documentation/marketplace/building-a-marketplace-app/set-up-a-global-oauth-client/).
