---
description: Connect to your users' Sailthru accounts.
---

# Sailthru

## Setup Guide

You can find your Sailthru API credentials in your [Sailthru account](https://my.sailthru.com/settings/api\_postbacks).

You'll need the following information to set up your Sailthru App with Paragon Connect:

* Company Key
* Company Secret

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Sailthru

Once your users have connected their Sailthru account, you can use the Paragon SDK to access the Sailthru API on behalf of connected users.

See the Sailthru [REST API documentation](https://getstarted.sailthru.com/developers/api/) for their full API reference.

Any Sailthru API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a list
paragon.request("sailthru", "[relative URL]", {
  method: "POST",
  body: {
   "list":"My Email List",
   "primary":1,
   "vars":{"color":"blue"},
   "public_name":"My Email List's public name",
   "type":"natural"
  }
});

// List all campaigns
paragon.request("sailthru", "[relative URL]", {
  method: "GET"
});
  
```

## Building Sailthru workflows

Once your Sailthru account is connected, you use the Sailthru Request step to access any of Sailthru's API endpoints without the authentication piece.

When creating or updating records in Sailthru, you can reference data from previous steps by typing `{{` to invoke the variable menu.
