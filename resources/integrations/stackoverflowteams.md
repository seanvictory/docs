---
description: Connect to your users' Stack Overflow for Teams accounts.
---

# Stack Overflow for Teams

## Setup Guide

You'll need the following information to set up your Stack Overflow for Teams App with Paragon Connect:

* Personal Access Token
* Team Name

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Stack Overflow for Teams

Once your users have connected their Stack Overflow for Teams account, you can use the Paragon SDK to access the Stack Overflow for Teams API on behalf of connected users.

See the Stack Overflow for Teams [REST API documentation](https://api.stackoverflowteams.com/docs) for their full API reference.

Any Stack Overflow for Teams API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get all Posts for the associated user(s)
paragon.request("stackoverflowteams", "/users/<ids>/posts", {
  method: "GET"
});

// Get a Post by ID
paragon.request("stackoverflowteams", "/questions/<ids>", {
  method: "GET"
});
  
```

## Building Stack Overflow for Teams workflows

Once your Stack Overflow for Teams account is connected, you use the Stack Overflow for Teams Request step to access any of Stack Overflow for Teams's API endpoints without the authentication piece.

When creating or updating records in Stack Overflow for Teams, you can reference data from previous steps by typing `{{` to invoke the variable menu.
