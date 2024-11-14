---
description: Connect to your users' Insightly accounts
---

# Insightly

## Setup Guide

You can find your Insightly app credentials in your [Insightly Developer Account.](https://api.insightly.com/v3.1/Help#!/Overview/Introduction)

You'll need the following information to set up your Insightly App with Paragon Connect:

* API Key
* Instance Pod

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Insightly

Once your users have connected their Insightly account, you can use the Paragon SDK to access the Insightly API on behalf of connected users.

See the Insightly [REST API documentation](https://api.insightly.com/v3.1/Help#!/Overview/Introduction) for their full API reference.

Any Insightly API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a Contact
await paragon.request("insightly", "/Contacts", {
  method: "POST",
  body: {
    "FIRST_NAME": "John",
    "LAST_NAME": "Doe",
    "EMAIL_ADDRESS": "john.doe@useparagon.com"
  }
});

// Get all Leads
await paragon.request("insightly", "/Leads", {
  method: "GET"
});

// Get all Opportunities
await paragon.request("insightly", "/Opportunities", {
  method: "GET"
});
```

## Building Insightly workflows

Once your Insightly account is connected, you use the Insightly Request step to access any of Insightly's API endpoints without the authentication piece.

When creating or updating records in Insightly, you can reference data from previous steps by typing `{{` to invoke the variable menu.
