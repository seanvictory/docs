---
description: Connect to your users' ActiveCampaign accounts.
---

# ActiveCampaign

## Setup Guide

You can find your ActiveCampaign app credentials in your [ActiveCampaign Developer Settings](https://developers.activecampaign.com/reference/authentication).

You'll need the following information to set up your ActiveCampaign App with Paragon Connect:

* API Key
* Domain

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to ActiveCampaign

Once your users have connected their ActiveCampaign account, you can use the Paragon SDK to access the ActiveCampaign API on behalf of connected users.

See the ActiveCampaign [REST API documentation](https://developers.activecampaign.com/reference/overview) for their full API reference.

Any ActiveCampaign API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Contact by ID
await paragon.request("activecampaign", "3/contacts/<id>", {
  method: "GET"
});

// Create a Deal
await paragon.request("activecampaign", "3/deals", {
  method: "POST",
  body: {
    deal: {
      contact: "51",
      account: "45",
      description: "This deal is an important deal",
      currency: "usd",
      group: "1",
      owner: "1",
      percent: null,
      stage: "1",
      status: 0,
      title: "AC Deal",
      value: 45600,
      fields: [
        {
          "customFieldId": 1,
          "fieldValue": "First field value"
        },
      ]
    }
  }
});

// Get all Campaigns
await paragon.request("activecampaign", "3/campaigns", {
  method: "GET"
});
  
```

## Building ActiveCampaign workflows

Once your ActiveCampaign account is connected, you use the ActiveCampaign Request step to access any of ActiveCampaign's API endpoints without the authentication piece.

When creating or updating records in ActiveCampaign, you can reference data from previous steps by typing `{{` to invoke the variable menu.
