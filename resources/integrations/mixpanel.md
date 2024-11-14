---
description: Connect to your users' Mixpanel accounts
---

# Mixpanel

## Setup Guide

You can find your Mixpanel service account credentials in your [Mixpanel Account](https://mixpanel.com/).

You'll need the following information to set up your Mixpanel App with Paragon Connect:

* Mixpanel Service Account Username
* Mixpanel Service Account Password

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Mixpanel

Once your users have connected their Mixpanel account, you can use the Paragon SDK to access the Mixpanel API on behalf of connected users.

See the Mixpanel [REST API documentation](https://developer.mixpanel.com/reference/query-api) for their full API reference.

Any Mixpanel API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Fetch data from your insights reports
paragon.request("mixpanel", "/insights?project_id=<PROJECT ID>&bookmark_id=<BOOKMARK ID>", {
  method: "GET"
});

// Fetch segmented data for an event
paragon.request("mixpanel", "/segmentation?project_id=<PROJECT ID>&event=<EVENT>&from_date=<DATE>&to_date=<DATE>&format=csv", {
  method: "GET"
});
  
```

## Building Mixpanel workflows

Once your Mixpanel account is connected, you use the Mixpanel Request step to access any of Mixpanel's API endpoints without the authentication piece.

When creating or updating records in Mixpanel, you can reference data from previous steps by typing `{{` to invoke the variable menu.
