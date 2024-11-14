---
description: Connect to your users' Typeform accounts
---

# Typeform

## Setup Guide

You can find your Typeform app credentials in your [Typeform Developer Account.](https://www.typeform.com/developers/get-started/)

You'll need the following information to set up your Typeform App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Typeform app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Typeform App page.
* **Client Secret:** Found under Client Secret on your Typeform App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Typeform app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Typeform

Once your users have connected their Typeform account, you can use the Paragon SDK to access the Typeform API on behalf of connected users.

See the Typeform [REST API documentation](https://www.typeform.com/developers/get-started/) for their full API reference.

Any Typeform API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Retrieve all Forms
paragon.request("typeform", "forms", {
  method: "GET"
});

// Retrieve Responses for a specific form
paragon.request("typeform", "/forms/<form_id>/responses", {
  method: "GET"
});
  
```

## Building Typeform workflows

Once your Typeform account is connected, you use the Typeform Request step to access any of Typeform's API endpoints without the authentication piece.

When creating or updating records in Typeform, you can reference data from previous steps by typing `{{` to invoke the variable menu.
