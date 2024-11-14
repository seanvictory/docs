---
description: Connect to your users' Quip accounts
---

# Quip

## Setup Guide

You can find your Quip app credentials in your [Quip Developer Account.](https://quip.com/dev/automation/documentation/current)

You'll need the following information to set up your Quip App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Quip app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Quip App page.
* **Client Secret:** Found under Client Secret on your Quip App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Quip app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Quip

Once your users have connected their Quip account, you can use the Paragon SDK to access the Quip API on behalf of connected users.

See the Quip [REST API documentation](https://quip.com/dev/automation/documentation/current) for their full API reference.

Any Quip API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Retrieve Documents, Spreadsheets, or Chat
paragon.request("quip", "/2/threads/<threadIdOrSecretPath>", {
  method: "GET"
});

// Create a Document
paragon.request("quip", "/1/threads/new-document, {
  method: "POST",
  body: {
    title: "My Quip Document"
    content: "<html></html>",
    type: "document"
  }
});
  
```

## Building Quip workflows

Once your Quip account is connected, you use the Quip Request step to access any of Quip's API endpoints without the authentication piece.

When creating or updating records in Quip, you can reference data from previous steps by typing `{{` to invoke the variable menu.
