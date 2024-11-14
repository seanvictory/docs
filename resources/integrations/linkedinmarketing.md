---
description: Connect to your users' LinkedIn Marketing accounts.
---

# LinkedIn Marketing

## Setup Guide

You can find your LinkedIn Marketing app credentials in your [LinkedIn Marketing Developer Account.](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads/getting-started?view=li-lms-2023-11)

You'll need the following information to set up your LinkedIn Marketing App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your LinkedIn Marketing app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your LinkedIn Marketing App page.
* **Client Secret:** Found under Client Secret on your LinkedIn Marketing App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your LinkedIn Marketing app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to LinkedIn Marketing

Once your users have connected their LinkedIn Marketing account, you can use the Paragon SDK to access the LinkedIn Marketing API on behalf of connected users.

See the LinkedIn Marketing [REST API documentation](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads/getting-started?view=li-lms-2023-11) for their full API reference.

Any LinkedIn Marketing API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Search Campaigns
paragon.request("linkedinmarketing", "/adAccounts/<adAccountId>/adCampaigns?q=search&search=(searchCriteria:(values:List(searchValue)))", {
  method: "GET"
});

// Get Page Statistics
paragon.request("linkedinmarketing", "/organizationPageStatistics?q=organization&organization=<organization URN>", {
  method: "GET"
});
  
```

## Building LinkedIn Marketing workflows

Once your LinkedIn Marketing account is connected, you use the LinkedIn Marketing Request step to access any of LinkedIn Marketing's API endpoints without the authentication piece.

When creating or updating records in LinkedIn Marketing, you can reference data from previous steps by typing `{{` to invoke the variable menu.
