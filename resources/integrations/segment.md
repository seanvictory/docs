---
description: Connect to your users' Segment accounts
---

# Segment

## Setup Guide

You can find your Segment account credentials in your [Segment Account](https://segment.com/).

You'll need the following information to set up your Segment App with Paragon Connect:

* Segment API Key

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Segment

Once your users have connected their Segment account, you can use the Paragon SDK to access the Segment API on behalf of connected users.

See the Segment [REST API documentation](https://docs.segmentapis.com/) for their full API reference.

Any Segment API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a new source
paragon.request("segment", "/sources", {
  method: "POST",
  body: {
    "slug": "my-test-source-r-dsv2",
    "name": "My Source",
    "enabled": true,
    "metadataId": "IqDTy1TpoU",
    "settings": { ... }
  }
});

// List all warehouses
paragon.request("segment", "/warehouses", {
  method: "GET"
});
  
```

## Building Segment workflows

Once your Segment account is connected, you use the Segment Request step to access any of Segment's API endpoints without the authentication piece.

When creating or updating records in Segment, you can reference data from previous steps by typing `{{` to invoke the variable menu.
