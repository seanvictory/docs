---
description: Connect to your users' Emarsys accounts.
---

# Emarsys

## Setup Guide

You can find your Emarsys app credentials in your [Emarsys account.](https://dev.emarsys.com/docs/core-api-reference/64bjdnkvt328t-overview-of-endpoint-batches)

You'll need the following information to set up your Emarsys account with Paragon Connect:

* API Username
* API Secret

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Emarsys

Once your users have connected their Emarsys account, you can use the Paragon SDK to access the Emarsys API on behalf of connected users.

See the Emarsys [REST API documentation](https://dev.emarsys.com/docs/core-api-reference/64bjdnkvt328t-overview-of-endpoint-batches) for their full API reference.

Any Emarsys API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// List Contacts
await paragon.request("emarsys", "v2/contact/query/?return=<field identifier ID>", {
  method: "GET"
});

// Update a Contact
await paragon.request("emarsys", "v2/contact", {
  method: "PUT",
  body: {
  "key_id": "3",
  "contacts": [
    {
      "1": "sample text",
      "2": "sample text",
      "3": "xyz@example.com"
    }
  ]
}
});

// Get Segments
paragon.request("emarsys", "v2/filter/<Segment ID>", {
  method: "GET"
});

// Get Campaigns
paragon.request("emarsys", "v2/email", {
  method: "GET"
});
  
```

## Building Emarsys workflows

Once your Emarsys account is connected, you use the Emarsys Request step to access any of Emarsys's API endpoints without the authentication piece.

When creating or updating records in Emarsys, you can reference data from previous steps by typing `{{` to invoke the variable menu.
