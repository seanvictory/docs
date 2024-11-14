---
description: Manage campaigns and contacts in Mailchimp
---

# Mailchimp

## Setup Guide

You can find your Mailchimp app credentials by visiting your [Mailchimp Account Settings.](https://mailchimp.com/)

{% hint style="info" %}
**Note:** You'll need to create a new Mailchimp app if you don't already have one.
{% endhint %}

You'll need the following information to set up your Mailchimp App with Paragon Connect:

* Client ID
* Client Secret

### Add the Redirect URL to your Mailchimp app

Paragon provides a redirect URL to send information to your Mailchimp app. To add the redirect URL to your Mailchimp app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Click your account by selecting the account icon.

3\. Select **Account** from the dropdown list.

4\. Under **Extras > Registered apps**, select your application or create a new one if you don't already have one.

5\. Under **Redirect URI**, paste-in the redirect URL from Paragon. The redirect URL can be found in Step 1.

6\. Press the green  `Update` button to confirm your changes.

### Add your Mailchimp app to Paragon

1\. Select **Mailchimp** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials in their respective sections:

* **Client ID:**
  1. Log in to your [Mailchimp dashboard](https://mailchimp.com/).
  2. Select "**Account"** from the Account dropdown.
  3. Under **Extras > Registered apps**, select your application.
  4. Copy the **Client ID** to use in Paragon Conncet.
* **Client Secret:**
  1. Log in to your [Mailchimp dashboard](https://mailchimp.com/).
  2. Click on "**Account**" in the Account dropdown.
  3. Under **Extras > Registered apps**, select your application.
  4. Copy your **Client ID** to use in Paragon Connect.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting Mailchimp to Paragon Connect.png>)

## Connecting to Mailchimp

Once your users have connected their Mailchimp account, you can use the Paragon SDK to access the Mailchimp API on behalf of connected users.

See the Mailchimp [REST API documentation](https://mailchimp.com/developer/marketing/api/lists) for their full API reference.

Any Mailchimp API endpoints can be accessed with the Paragon SDK as shown in this example.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration.

// Authenticate the user
paragon.authenticate(<ProjectID>, <Paragon User Token>);

// Create a List
await paragon.request("mailchimp", "/lists/<List ID>", {
  method: "POST",
  body: {
    "members": [{ email_address: "test@gmail.com" }],
    "update_existing": true
  }
});

// List all Campaigns
await paragon.request("mailchimp", "/campaigns",
  method: “GET”
});

```
{% endtab %}
{% endtabs %}

## Building Mailchimp workflows

Once your Mailchimp account is connected, you can add steps to perform the following actions:

* Create Campaign
* Update Campaign
* Send Campaign
* Search Campaigns
* Get Campaign by ID
* Delete Campaign by ID
* Create List
* Get List by ID
* Search Lists
* Add Contact to List
* Update Contact in List
* Get Contacts from List

When using Mailchimp, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Mailchimp account. For example, you might want to trigger a workflow whenever new contacts are added to a Mailchimp list to sync your users' Mailchimp contacts to your application in real-time.

You can find the full list of Webhook Triggers for Mailchimp below:

* **Mailchimp Lists**
