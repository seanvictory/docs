---
description: Connect to your users' Apollo.io accounts
---

# Apollo.io

## Setup Guide

You can find your Apollo.io app credentials in your [Apollo.io Developer Account.](https://apolloio.github.io/apollo-api-docs/?shell#introduction)

You'll need the following information to set up your Apollo.io App with Paragon Connect:

* Apollo.io API Key

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Apollo.io

Once your users have connected their Apollo.io account, you can use the Paragon SDK to access the Apollo.io API on behalf of connected users.

See the Apollo.io [REST API documentation](https://apolloio.github.io/apollo-api-docs/?shell#introduction) for their full API reference.

Any Apollo.io API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Create a Contact            
await paragon.request('apolloio', '/contacts', {
  method: 'POST',
  body: { 
   "first_name": "Jonny",
   "last_name": "Snow",
   "title": "Lord Commander",
   "organization_name": "Apollo"
  },
});

// Search Users
await paragon.request('apolloio', '/users/search', {
  method: 'GET',
});
  
```

## Building Apollo.io workflows

Once your Apollo.io account is connected, you use the Apollo.io Request step to access any of Apollo.io's API endpoints without the authentication piece.

When creating or updating records in Apollo.io, you can reference data from previous steps by typing `{{` to invoke the variable menu.
