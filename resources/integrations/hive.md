---
description: Connect to your users' Hive accounts
---

# Hive

## Setup Guide

You can find your Hive API credentials in your [Hive Account](https://hive.com/).

You'll need the following information to set up your Hive App with Paragon Connect:

* API Key
* User ID

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Hive

Once your users have connected their Hive account, you can use the Paragon SDK to access the Hive API on behalf of connected users.

See the Hive [REST API documentation](https://developers.hive.com/reference/introduction) for their full API reference.

Any Hive API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get all actions in the provided Workspace
paragon.request("hive", "workspaces/<workspaceId>/actions", {
  method: "GET"
});

// Get an action by ID
paragon.request("hive", "actions/<actionId>", {
  method: "GET"
});
  
```

## Building Hive workflows

Once your Hive account is connected, you use the Hive Request step to access any of Hive's API endpoints without the authentication piece.

When creating or updating records in Hive, you can reference data from previous steps by typing `{{` to invoke the variable menu.
