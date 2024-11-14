---
description: Connect your Outreach app for OAuth in Paragon.
---

# Outreach

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new Outreach app if you don't already have one.
{% endhint %}

You can find your Outreach app credentials by visiting your [Outreach developer portal](https://developer.intuit.com/myapps).

You'll need the following information to set up your Outreach App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* An [Outreach Developer account](https://www.outreach.io/product/platform/api).
* An Outreach app.

### Add the Redirect URL to your Outreach app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Outreach app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```html
https://passport.useparagon.com/oauth
```

2\. Reach out to your Outreach API Integrations Specialist and ask to change the default redirect URL for your application to the one Paragon provides.

### Add your Outreach app to Paragon <a href="#add-your-stripe-app-to-paragon" id="add-your-stripe-app-to-paragon"></a>

1\. Select **Outreach** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials in their respective sections:

* **Client ID:** Provided by Outreach's team.&#x20;
* **Client Secret:** Provided by Outreach's team.&#x20;
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

## Connecting to Outreach

Once your users have connected their Outreach account, you can use the Paragon SDK to access the Outreach API on behalf of connected users.

See the Outreach [REST API documentation](https://api.outreach.io/api/v2/docs) for their full API reference.

Any Outreach API endpoints can be accessed with the Paragon SDK as shown in this example.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get accounts
await paragon.request("outreach", "/accounts", { 
    method: "GET"
  });

// Create a project
await paragon.request("outreach", "/prospect", { 
    method: "POST",
      body: {  
       "type": "prospect",
        "attributes": {
           "emails": ["sally.smith@acme.example.com"],
            "firstName": "Sally",
            "title": "CEO"
          }
        } 
      });
```
{% endtab %}
{% endtabs %}

## Building Outreach workflows

Once your Outreach account is connected, you can add steps to perform the following actions:

* Create Account
* Update Account
* Get Accounts
* Get Account by ID
* Create Opportunity
* Update Opportunity
* Get Opportunities
* Get Opportunity by ID
* Create Prospects
* Update Prospect
* Get Prospects
* Get Prospect by ID
* Add Prospect to Sequence

When creating or updating events in Outreach, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating an Opportunity using Outreach in Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Outreach account. For example, you might want to trigger a workflow whenever new opportunities are created Outreach to sync your users' Outreach contacts to your application in real-time.

![](<../../.gitbook/assets/Outreach triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Outreach below:

* **New Account**
* **Account Updated**
* **New Opportunity**
* **Opportunity Updated**
* **New Prospect**
* **Prospect Updated**
