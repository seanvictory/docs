---
description: Connect your Marketo app for OAuth in Paragon.
---

# Marketo

## Setup Guide

You can find your Marketo application credentials by visiting LaunchPoint in the Admin section of your [Marketo Dashboard](https://www.marketo.com/).

You'll need the following information to set up your Marketo App with Paragon Connect:

* Client ID
* Client Secret
* Endpoint URL
* Identity URL

### Prerequisites

* A Marketo Account. You can create one [here](https://www.marketo.com/).
* A Custom Service. Learn more about creating Custom Services in Marketo [here](https://developers.marketo.com/rest-api/custom-services/).&#x20;

## Gathering your Credentials

Your end-users will be required to enter their Marketo Client ID, Client Secret, Endpoint URL, and Identity URL as authentication when first connecting to your application.

You can find the credentials for your Marketo account in their respective sections:

* **Client ID:** Found under Admin > Integration > LaunchPoint > View Details > Client Id on your Marketo dashboard.
* **Client Secret:** Found under Admin > Integration > LaunchPoint > View Details > Client Secret on your Marketo dashboard.
* **Endpoint URL:** Found under Admin > Integration > Web Services in the REST API section.
* **Identity URL:** Found under Admin > Integration > Web Services in the REST API section.

Press the blue "**Continue**" button to save your credentials.

![](<../../.gitbook/assets/Connecting your Marketo account to Paragon.png>)

## Connecting to Marketo

Once your users have connected their Marketo account, you can use the Paragon SDK to access the Marketo API on behalf of connected users.

See the Marketo [REST API documentation](https://developers.marketo.com/getting-started/) for their full API reference.

Any Marketo API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get Leads
await paragon.request("marketo", "leads.json?filterType=id&filterValues=1", {
  method: "GET",
});


// Create a new Lead
await paragon.request("marketo", "leads.json", {
  method: "POST",
  body: { 
      "input": [
        {  
          "email":"kjashaedd-1@klooblept.com",
          "firstName":"Kataldar-1"
        },
      ]
  }
});
```

## Building Marketo workflows

Once your Marketo account is connected, you can add steps to perform the following actions:

* Create or Update Lead
* Get Leads
* Get Lead by ID
* Add Leads to List

When creating or updating leads in Marketo, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Using Marketo in Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Marketo account. For example, you might want to trigger a workflow whenever new leads are added to a list in Marketo to sync your users' Marketo leads to your application in real-time.

<figure><img src="../../.gitbook/assets/Marketo Webhook Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Marketo below:

* **Lead Added to a List**
