---
description: Connect to your users' Zoho CRM accounts.
---

# Zoho CRM

## Setup Guide

You can find your Zoho CRM app credentials in your [Zoho CRM Developer Account](https://accounts.zoho.com/developerconsole).

You'll need the following information to set up your Zoho CRM App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Creating a Zoho CRM app

To get started, you'll need to create an app in the [Zoho API Console](https://api-console.zoho.com/).

1. Sign in with your Zoho CRM Developer Account.
2.  Click "**Add Client**" in the top right:\


    <figure><img src="../../.gitbook/assets/Screen Shot 2022-11-03 at 9.10.23 PM.png" alt=""><figcaption></figcaption></figure>
3.  Select "**Server-based Applications**" as the Client Type:\


    <figure><img src="../../.gitbook/assets/Screen Shot 2022-11-03 at 9.11.18 PM.png" alt=""><figcaption></figcaption></figure>
4. Add your website as the Homepage URL.
5. Add [https://passport.useparagon.com/oauth](https://passport.useparagon.com/oauth) as an **Authorized Redirect URI**.

### Add the Redirect URL to your Zoho CRM app

Paragon provides a redirect URL to send information to your Zoho CRM app. To add the redirect URL to your Zoho CRM app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your [Zoho CRM Developer Account](https://accounts.zoho.com/developerconsole), select your application.

3\. Under **Authorized Redirect URIs**, paste-in the Paragon Connect redirect URL found in Step 1.

4\. Copy the Client ID and Client Secret provided by Zoho CRM.

### Add your Zoho CRM app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found at the end of [Step 1](zohocrm.md#add-the-redirect-url-to-your-zoho-crm-app) on your Zoho CRM App page.
* **Client Secret:** Found at the end of [Step 1](zohocrm.md#add-the-redirect-url-to-your-zoho-crm-app) on your Zoho CRM App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting to your Zoho CRM app  to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Zoho CRM

Once your users have connected their Zoho CRM account, you can use the Paragon SDK to access the Zoho CRM API on behalf of connected users.

See the Zoho CRM [REST API documentation](https://www.zoho.com/crm/developer/docs/api/v3/modules-api.html) for their full API reference.

Any Zoho CRM API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Retrieve the user's data
await paragon.request("zohocrm", "users", {
  method: "GET",
});
            
// Add a user to your organization
await paragon.request("zohocrm", "users", {
  method: "POST",
  body: {
    "users": [
      {
        "role": "554023000000015969",
        "first_name": "Patricia",
        "email": "Patricia@abcl.com",
        "profile": "554023000000015975",
        "last_name": "Boyle"
      }
    ]
  }
});

```

## Building Zoho CRM workflows

Once your Zoho CRM account is connected, you can add steps to perform the following actions:

* Create Record
* Update Record
* Get Record by ID
* Search Records
* Delete Record
* Search Records by COQL Query

When creating or updating records in Zoho CRM, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Zoho CRM account. For example, you might want to trigger a workflow whenever new Accounts are created in Zoho CRM to sync your users' Zoho CRM Accounts to your application in real-time.

You can find the full list of Webhook Triggers for Zoho CRM below:

* **New Record**
* **Record Updated**
