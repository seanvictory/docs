---
description: Connect to your users' TikTok Ads accounts.
---

# TikTok Ads

## Setup Guide

You can find your TikTok Ads app credentials in your [TikTok for Business Developers](https://ads.tiktok.com/marketing\_api/homepage) portal.

You'll need the following information to set up your TikTok Ads App with Paragon Connect:

* App ID
* App Secret

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your TikTok Ads app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **App ID:** Found under App ID on your TikTok Ads App page.
* **App Secret:** Found under App Secret on your TikTok Ads App page.

{% hint style="info" %}
Leaving the App ID and App Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your TikTok Ads app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to TikTok Ads

Once your users have connected their TikTok Ads account, you can use the Paragon SDK to access the TikTok Ads API on behalf of connected users.

See the TikTok Ads [REST API documentation](https://ads.tiktok.com/marketing\_api/docs) for their full API reference.

Any TikTok Ads API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Campaigns
paragon.request("tiktokads", "v1.3/campaign/get/", {
  method: "GET"
});

// Create a Campaign
paragon.request("tiktokads", "v1.3/campaign/create/", {
  method: "POST",
  body: {
    "advertiser_id": "ADVERTISER_ID",
    "budget_mode": "BUDGET_MODE",
    "objective_type": "OBJECTIVE_TYPE",
    "budget": "BUDGET",
    "campaign_name": "CAMPAIGN_NAME"
  }
});
  
```

## Building TikTok Ads workflows

Once your TikTok Ads account is connected, you use the TikTok Ads Request step to access any of TikTok Ads's API endpoints without the authentication piece.

When creating or updating records in TikTok Ads, you can reference data from previous steps by typing `{{` to invoke the variable menu.
