---
description: Connect to your users' Lever accounts
---

# Lever

## Setup Guide

You can find your Lever app credentials in your [Lever Developer Account.](https://hire.lever.co/developer/documentation)

You'll need the following information to set up your Lever App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Lever app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Lever App page.
* **Client Secret:** Found under Client Secret on your Lever App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Lever app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Lever

Once your users have connected their Lever account, you can use the Paragon SDK to access the Lever API on behalf of connected users.

See the Lever [REST API documentation](https://hire.lever.co/developer/documentation) for their full API reference.

Any Lever API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Retrieve a single application
paragon.request("lever", "/opportunities/:opportunity/applications/:application", {
  method: "GET"
});

// Retrieve a single opportunity
paragon.request("lever", "/opportunities/:opportunity", {
  method: "GET"
});

// Create an opportunity
paragon.request("lever", "[relative URL]", {
  method: "POST",
  body: {
    "name": "John Appleseed",
    "email": "john@domain.com",
    "phone": "1012223333"
  }
});
  
```

## Building Lever workflows

Once your Lever account is connected, you can add steps to perform the following actions:

* Create an Opportunity
* Get Opportunity by ID
* Get Opportunities
* Update Contact
* Get Contact by ID
* Create a Posting
* Update Posting
* Get Postings by ID
* Get Postings

When creating or updating records in Lever, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Lever account. For example, you might want to trigger a workflow whenever new candidates are created in Lever to sync your users' Lever candidates to your application in real-time.

<figure><img src="../../.gitbook/assets/Lever Webhook Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Lever below:

* **Candidate Created**
* **Candidate Updated**
* **Posting Created**
* **Posting Updated**
