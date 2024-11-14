---
description: Connect your Intercom app for OAuth in Paragon.
---

# Intercom

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new Intercom app if you don't already have one. To access your customer's Intercom data by using OAuth, you'll need to [submit your app for a review](https://developers.intercom.com/building-apps/docs/review-publish-your-app#changing-your-review-or-listing).
{% endhint %}

You can find your Intercom app credentials by visiting your [Intercom Developer Hub](https://developers.intercom.com/).

You'll need the following information to set up your Intercom App with Paragon Connect:

* Client ID
* Client Secret

### Add the Redirect URL to your Intercom app

Paragon provides a redirect URL to send information to your Intercom app. To add the redirect URL to your Intercom app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your [Intercom developer dashboard](https://developers.intercom.com/), select your application.

3\. Under **Configure > Authentication**, click the **Edit** button.

4\. Tick the **Use OAuth** option.

5\. Under **Redirect URLs**, paste-in Paragon Connect's redirect URL found in Step 1. Click the **Save** button to save your changes.

![](<../../.gitbook/assets/Connect - Authorizing Intercom OAuth for Paragon Connect.gif>)

### Add your Intercom app to Paragon

1\. Select Intercom from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](intercom.md#1-add-the-redirect-url-to-your-intercom-app) in their respective sections:

* **Client ID:** Found under Configure > Basic Information > Client ID on your Intercom app page.
* **Client Secret:** Found under Configure > Basic Information > Client Secret on your Intercom app page.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Intercom app to Paragon Connect.png>)

## Connecting to Intercom

Once your users have connected their Intercom account, you can use the Paragon SDK to access the Intercom API on behalf of connected users.

See the Intercom [REST API documentation](https://developers.intercom.com/building-apps/docs/rest-apis) for their full API reference.

Any Intercom API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create Contact
await paragon.request("intercom", "/contacts", { 
  method: "POST",
  body: {
    "role": "user",
	  "external_id": "25",
	  "email": "wash@serenity.io",
    "phone": "+1123456789",
    "name": "Hoban Washburn",
    "avatar": "https://example.org/128Wash.jpg",
    "last_seen_at": 1571069751,
    "signed_up_at": 1571069751,
    "owner_id": 127,
    "unsubscribed_from_emails": false,
    "custom_attributes": {
      "paid_subscriber": true,
      "monthly_spend": 155.5,
      "team_mates": 1
    }
  }
});

// Query Contacts
await paragon.request("intercom", "/contacts", { 
  method: "GET"
});
  
```

## Building Intercom workflows

Once your Intercom account is connected, you can add steps to perform the following actions:

* Create contact
* Update contact
* Get contact by ID
* Search contacts
* Send message

When creating or updating contacts in Intercom, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating a lead in Intercom with Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Intercom account. For example, you might want to trigger a workflow whenever new companies are created in Intercom to sync your users' Intercom companies to your application in real-time.

<figure><img src="../../.gitbook/assets/Intercom Webhook Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Intercom below:

* **Company Created**
* **Company Updated**
* **Contact Created**
* **Contact Updated**
