---
description: Connect to your users' Oracle Eloqua accounts
---

# Oracle Eloqua

## Setup Guide

You can find your Oracle Eloqua app credentials by visiting your Oracle Eloqua App dashboard.

{% hint style="info" %}
**Note:** You'll need to create a new Oracle Eloqua app if you don't already have one.
{% endhint %}

You'll need the following information to set up your Oracle Eloqua App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Oracle Eloqua app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Oracle Eloqua App page.
* **Client Secret:** Found under Client Secret on your Oracle Eloqua App page.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting an Oracle Eloqua application to Paragon Connect.png>)

## Connecting to Oracle Eloqua

Once your users have connected their Oracle Eloqua account, you can use the Paragon SDK to access the Oracle Eloqua API on behalf of connected users.

See the Oracle Eloqua [REST API documentation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html) for their full API reference.

Any Oracle Eloqua API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get a list of all campaigns
await paragon.request("eloqua", "/api/rest/2.0/assets/campaigns", {
  method: "GET"
});

// Create a campaign
await paragon.request("eloqua", "/api/rest/2.0/assets/campaign", {
  method: "POST",
  body: {
    name: "New campaign",
    elements: []
  }
});

// Activate a campagin
await paragon.request("eloqua", "/api/rest/2.0/assets/campaign/active/<Campaign ID>", {
method: "POST",
body: {
  activateNow: true
}
});
```

## Building Oracle Eloqua workflows

Once your Oracle Eloqua account is connected, you can add steps to perform the following actions:

* Create Campaign
* Update Campaign
* Activate Campaign
* Search Campaigns
* Get Campaign by ID
* Create Email
* Update Email
* Search Emails
* Send Email Deployment
* Create Contact
* Update Contact
* Search Contacts

When creating or updating campaigns or contacts in Oracle Eloqua, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating a Oracle Eloqua workflow in Paragon Connect.png>)
