---
description: Connect to your users' Gusto accounts
---

# Gusto

## Setup Guide

You can find your Gusto app credentials in your [Gusto Developer Account.](https://docs.gusto.com/app-integrations/reference)

You'll need the following information to set up your Gusto App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Gusto app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Gusto App page.
* **Client Secret:** Found under Client Secret on your Gusto App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Gusto app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Gusto

Once your users have connected their Gusto account, you can use the Paragon SDK to access the Gusto API on behalf of connected users.

See the Gusto [REST API documentation](https://docs.gusto.com/app-integrations/reference) for their full API reference.

Any Gusto API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get a company
await paragon.request("gusto", "/companies/<company_id>", {
  method: "GET"
});

// Create a Company bank account
await paragon.request("gusto", "/companies/<company_id>/bank_accounts", {
  method: "POST",
  body: {
    "routing_number": "115092013",
    "account_type": "Checking",
    "account_number": "9775014007"
  }
});

// Get a Location
await paragon.request("gusto", "/locations/<location_id>", {
  method: "GET"
});
  
```

## Building Gusto workflows

Once your Gusto account is connected, you use the Gusto Request step to access any of Gusto's API endpoints without the authentication piece.

When creating or updating records in Gusto, you can reference data from previous steps by typing `{{` to invoke the variable menu.
