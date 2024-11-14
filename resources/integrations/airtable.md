---
description: Connect to your users' Airtable accounts
---

# Airtable

## Setup Guide

You can find your Airtable API Key in your [Airtable Account.](https://airtable.com/)

You'll need the following information to set up your Airtable App with Paragon Connect:

* Airtable API Key

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Airtable

Once your users have connected their Airtable account, you can use the Paragon SDK to access the Airtable API on behalf of connected users.

See the Airtable [REST API documentation](https://airtable.com/api) for their full API reference.

Any Airtable API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// List records
paragon.request("airtable", "/<BASE ID>/<TABLE NAME>?maxRecords=3&view=Grid%20view", {
  method: "GET"
});

// Create a record
paragon.request("airtable", "/<BASE ID>/<TABLE NAME>", {
  method: "POST",
  body: {
  "records": [
      "fields": {
        "<AIRTABLE COLUMN NAME>": <VALUE>
      }
    ]
  }
});
  
```

## Building Airtable workflows

Once your Airtable account is connected, you use the Airtable Request step to access any of Airtable's API endpoints without the authentication piece.

When creating or updating records in Airtable, you can reference data from previous steps by typing `{{` to invoke the variable menu.
