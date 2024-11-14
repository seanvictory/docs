---
description: Connect to your users' Monday.com accounts
---

# Monday.com

## Setup Guide

You can find your Monday.com app credentials by visiting your [Monday.com account](https://monday.com/).

You'll need the following information to set up your Monday.com app with Paragon:

* API Key

### Getting your Monday.com API Key

1. Go to your Monday.com account.&#x20;
2. Click the Account icon in the bottom-left corner
3. Select **Administration**
4. Select **"Connections"**&#x20;
5. Select **"API"** from the top sidebar.
6. Copy the API Key under **Personal API Token**.&#x20;

## Connecting to Monday.com

Once your users have connected their Monday.com account, you can use the Paragon SDK to access the Monday.com API on behalf of connected users.

See the Monday.com [REST API documentation](https://api.developer.monday.com/docs/basics) for their full API reference.

Any Monday.com API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Query Items
await paragon.request("monday.com", "/", { 
  method: "POST",
  body: {"query":"query { items (ids: [157244624, 201781760, 239164869]) { name } }"}
});

// Create an item
await paragon.request("monday.com", "/", { 
  method: "POST",
  body: {"query":"mutation { create_item (board_id: 1234567, group_id: \"today\", item_name: \"new item\") { id }}
});

```

## Building Monday.com workflows

Once your Monday.com account is connected, you can add steps to perform the following actions:

* Create Item
* Update Item
* Get Item by ID
* Get Item by External ID
* Search Items
* Delete Item
* Archive Item
* Create Subitem
* Search users

When creating or updating items in Monday.com, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Monday.com account. For example, you might want to trigger a workflow whenever items are updated to sync your users' Monday.com items to your application in real-time.

![](<../../.gitbook/assets/Monday.com webhook triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Monday.com below:

* **Item Created**
* **Item Updated**\
  Trigger when Monday.com items have either a name change or a column value change.

