---
description: Connect to your users' Heap accounts.
---

# Heap

## Setup Guide

You can find your Heap app credentials in your [Heap Developer Account.](https://developers.heap.io/reference/)

You'll need the following information to set up your Heap App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Heap app to Paragon

Under **Integrations > Connected Integrations >** **Heap** **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Heap App page.
* **Client Secret:** Found under Client Secret on your Heap App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Heap application to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Heap

Once your users have connected their Heap account, you can use the Paragon SDK to access the Heap API on behalf of connected users.

See the Heap [REST API documentation](https://developers.heap.io/reference/) for their full API reference.

Any Heap API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Add custom properties to users
paragon.request("heap", "/add_account_properties", {
  method: "POST",
  body: {
    "app_id": "123456789", 
    "account_id": "Fake Company",
    "properties": {
      "is_in_good_standing": "true",
      "revenue_potential": "123456",
      "account_hq": "United Kingdom",
      "subscription": "Monthly"
    }
  }
});

// Send a custom event in Heap
paragon.request("heap", "/track", {
  method: "POST",
  body: {
    "app_id": "11",
    "identity": "alice@example.com",
    "event": "Send Transactional Email",
    "timestamp": "2017-03-10T22:21:56+00:00", 
    "properties": {
      "subject": "Welcome to My App!",
      "variation": "A"
    }
  }
});
```

## Building Heap workflows

Once your Heap account is connected, you use the Heap Request step to access any of Heap's API endpoints without the authentication piece.

When creating or updating records in Heap, you can reference data from previous steps by typing `{{` to invoke the variable menu.
