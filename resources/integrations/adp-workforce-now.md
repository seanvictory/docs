---
description: Connect to your users' ADP Workforce Now accounts
---

# ADP Workforce Now

## Setup Guide

You can find your ADP Workforce Now app credentials in your [ADP Workforce Now Developer Account.](https://developers.adp.com/build/api-explorer)

You'll need the following information to set up your ADP Workforce Now App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your ADP Workforce Now app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your ADP Workforce Now App page.
* **Client Secret:** Found under Client Secret on your ADP Workforce Now App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your ADP Workforce Now app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to ADP Workforce Now

Once your users have connected their ADP Workforce Now account, you can use the Paragon SDK to access the ADP Workforce Now API on behalf of connected users.

See the ADP Workforce Now [REST API documentation](https://developers.adp.com/build/api-explorer) for their full API reference.

Any ADP Workforce Now API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Workers
paragon.request("adpworkforcenow", "hr/v2/workers", {
  method: "GET"
});

// Get Worker's Pay Distributions
paragon.request("adpworkforcenow", "/payroll/v2/workers/<aoid>/pay-distributions", {
  method: "GET"
});

// Get a Job Application by ID
paragon.request("adpworkforcenow", "/staffing/v2/job-applications/<job-application-id>", {
  method: "GET"
});
  
```

## Building ADP Workforce Now workflows

Once your ADP Workforce Now account is connected, you use the ADP Workforce Now Request step to access any of ADP Workforce Now's API endpoints without the authentication piece.

When creating or updating records in ADP Workforce Now, you can reference data from previous steps by typing `{{` to invoke the variable menu.
