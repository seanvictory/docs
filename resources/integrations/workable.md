---
description: Connect to your users' Workable accounts.
---

# Workable

## Setup Guide

You can find your Workable app credentials in your [Workable Developer Account.](https://workable.readme.io/reference/generate-an-access-token)

You'll need the following information to set up your Workable App with Paragon Connect:

* Account Subdomain
* API Access Token

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Workable

Once your users have connected their Workable account, you can use the Paragon SDK to access the Workable API on behalf of connected users.

See the Workable [REST API documentation](https://workable.readme.io/reference/generate-an-access-token) for their full API reference.

Any Workable API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Retrieve the members data
await paragon.request("workable", "/members", {
  method: "GET",
});

// Create a candidate at the specified job
await paragon.request("workable", "/jobs/{shortcode}/candidates", {
  method: "POST",
  body: {
    "candidate": [
      {
        "first_name": "Hashirama",
        "email": "hashirama@senju.com",
        "last_name": "Senju"
      }
    ]
  }
});
  
```

## Building Workable workflows

Once your Workable account is connected, you use the Workable Request step to access any of Workable's API endpoints without the authentication piece.

When creating or updating records in Workable, you can reference data from previous steps by typing `{{` to invoke the variable menu.
