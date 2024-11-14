---
description: Connect your Xero app for OAuth in Paragon.
---

# Xero

## Setup Guide

You can find your Xero app credentials by visiting your [Xero Developer Portal](https://developer.xero.com/app/manage)

{% hint style="info" %}
**Note:** You'll need to create a new Xero app if you don't already have one.
{% endhint %}

You'll need the following information to set up your Xero App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Xero app

Paragon provides a redirect URL to send information to your Xero app. To add the redirect URL to your Xero app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log in to your [Xero Developer Portal](https://developer.xero.com/app/manage).&#x20;

3\. Select your application from the developer portal.

4\. Under **App details > OAuth 2.0 credentials**, press the `Add another URI` button.

5\. Paste-in the redirect URL from Paragon. The redirect URL can be found in Step 1.

6\. Press the `Save` button to save the Redirect URL.

![](<../../.gitbook/assets/Adding a redirect URL to Xero.png>)

### Add your Xero app to Paragon <a href="#add-your-stripe-app-to-paragon" id="add-your-stripe-app-to-paragon"></a>

1\. Select **Xero** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials in their respective sections:

* **Client ID:**
  1. Log in to your [Xero Developer Portal](https://developer.xero.com/app/manage).
  2. Select your application.
  3. Navigate to **App details > OAuth 2.0 credentials**.
  4. Copy the **Client ID** from "**Client id**".
* **Client Secret:**
  1. Log in to your [Xero Developer Portal](https://developer.xero.com/app/manage).
  2. Select your application.
  3. Navigate to **App details > OAuth 2.0 credentials**.
  4. Press `Generate a secret`.
  5. Copy the **Client Secret** to use in Paragon.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

## Connecting to Xero

Once your users have connected their Xero account, you can use the Paragon SDK to access the Xero API on behalf of connected users.

See the Xero [REST API documentation](https://developer.xero.com/documentation/api/accounting/overview/) for their full API reference.

Any Xero API endpoints can be accessed with the Paragon SDK as shown in this example.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Query Payments
await paragon.request("xero", "payments", {
  method: "GET",
});
```
{% endtab %}
{% endtabs %}

## Building Xero workflows

Once your Xero account is connected, you can add steps to perform the following actions:

* Get Accounts
* Get Contacts
* Create Customer
* Update Customer
* Get Invoices
* Create Invoice
* Update Invoice
* Send Invoice
* Get Payments
* Create Payments

When creating or updating customers and invoices in Xero, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Using Xero in Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Xero account. For example, you might want to trigger a workflow whenever new customers are created in Xero to sync your users' Xero customers to your application in real-time.

![](<../../.gitbook/assets/Xero webhook triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Xero below:‌

* **New Account**
* **New Customer**
* **New Invoice**
