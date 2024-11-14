---
description: Manage boards and cards in Trello
---

# Trello

## Setup Guide

You'll need the following information to set up your Trello App with Paragon Connect:

* App Name
* Scopes Requested

### Add your Trello app to Paragon

1\. Select Trello from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials in their respective sections:

* **App Name:**
  * Specify an app name to appear on Trello
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the App Name blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Trello app to Paragon Connect.png>)

## Connecting to Trello

Once your users have connected their Trello account, you can use the Paragon SDK to access the Trello API on behalf of connected users.

See the Trello [REST API documentation](https://developer.atlassian.com/cloud/trello/rest/) for their full API reference.

Any Trello API endpoints can be accessed with the Paragon SDK as shown in this example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration.

// Authenticate the user
paragon.authenticate(<ProjectID>, <Paragon User Token>);

// Get a board
await paragon.request("trello", "/boards/<Board ID>", {
  method: “GET”,
});

// Create a new card
await paragon.request("trello", "/cards",
  method: “POST”,
  body: {
    idList: “<List ID>”,
    name: “New task”,
    desc: “Integrate all productivity apps using Paragon”
  }
});

```
{% endtab %}
{% endtabs %}

## Building Trello workflows

Once your Trello account is connected, you can add steps to perform the following actions:

* Search Cards
* Get Cards in Board
* Create Card
* Update Card
* Delete Card
* Get Lists in Board
* Search Boards

When using Trello, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Trello account. For example, you might want to trigger a workflow whenever Cards are updated to sync your users' Trello Cards to your application in real-time.

![](<../../.gitbook/assets/Using Trello Triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Trello below:

* **Board Created**
* **Board Updated**
* **Card Created**
* **Card Updated**
* **New Comment**
