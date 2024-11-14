---
description: Connect to your users' Keap accounts.
---

# Keap

## Setup Guide

You can find your Keap app credentials in your [Keap Developer Account.](https://developer.infusionsoft.com/docs/rest/)

You'll need the following information to set up your Keap App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Keap app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Keap App page.
* **Client Secret:** Found under Client Secret on your Keap App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Keap app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Keap

Once your users have connected their Keap account, you can use the Paragon SDK to access the Keap API on behalf of connected users.

See the Keap [REST API documentation](https://developer.infusionsoft.com/docs/rest/) for their full API reference.

Any Keap API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create Company
await paragon.request("keap", "/v1/companies", {
  method: "POST",
  body: {
    "company_name": "string",
    "email_address": "string",
    "notes": "string",
    "opt_in_reason": "string",
    "phone_number": {
      "extension": "string",
      "number": "string",
      "type": "string"
    },
    "website": "string"
  }
});

// List Companies
await paragon.request("keap", "/v1/companies", {
  method: "GET"
});
  
```

## Building Keap workflows

Once your Keap account is connected, you use the Keap Request step to access any of Keap's API endpoints without the authentication piece.

When creating or updating records in Keap, you can reference data from previous steps by typing `{{` to invoke the variable menu.
