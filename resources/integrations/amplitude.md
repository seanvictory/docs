---
description: Connect to your users' Amplitude accounts.
---

# Amplitude

## Setup Guide

You can find your Amplitude app credentials on your [Amplitude Settings page](https://www.docs.developers.amplitude.com/analytics/find-api-credentials/).

You'll need the following information to set up your Amplitude App with Paragon Connect:

* Amplitude API Key

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Amplitude

Once your users have connected their Amplitude account, you can use the Paragon SDK to access the Amplitude API on behalf of connected users.

See the Amplitude [REST API documentation](https://www.docs.developers.amplitude.com/analytics/api-reference-overview/) for their full API reference.

Any Amplitude API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get cohorts data from Amplitude
paragon.request("amplitude", "/3/cohorts", {
  method: "GET",
});

// Get data from a dashboard chart
paragon.request("amplitude", "/api/3/chart/<chart_id>/query", {
  method: "GET"
});
  
```

## Building Amplitude workflows

Once your Amplitude account is connected, you use the Amplitude Request step to access any of Amplitude's API endpoints without the authentication piece.

When creating or updating records in Amplitude, you can reference data from previous steps by typing `{{` to invoke the variable menu.
