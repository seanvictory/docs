---
description: Connect to your users' Notion accounts
---

# Notion

## Setup Guide

You can find your Notion app credentials on your [Notion Integrations Page](https://www.notion.so/my-integrations).

You'll need the following information to set up your Notion App with Paragon Connect:

* Client ID
* Client Secret

### Add your Notion app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Notion App page.
* **Client Secret:** Found under Client Secret on your Notion App page.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Notion application to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Notion

Once your users have connected their Notion account, you can use the Paragon SDK to access the Notion API on behalf of connected users.

See the Notion [REST API documentation](https://developers.notion.com/reference) for their full API reference.

Any Notion API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a page in Notion
paragon.request("notion", "/v1/pages", {
  method: "POST",
  body: {
  	"parent": { "page_id": "d9824bdc84454327be8b5b47500af6ce" },
    "icon": {
        "emoji": "🥬"
    },
	"properties": {
		"Title": {
            "text": "My page"
		},
	},
	"children": []
  }
});

// Retrieve a Notion page
paragon.request("notion", "/v1/pages/<page ID>", {
  method: "GET"
});
  
```

## Building Notion workflows

Once your Notion account is connected, you can add steps to perform the following actions:

* Create a Page
* Update a Page
* Get a Page
* Archive a Page
* Search Pages
* Update a Block
* Retrieve a Block
* Delete a Block

You can also use the Notion Request step to access any of Notion's API endpoints without the authentication piece.

When creating or updating records in Notion, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Notion account. For example, you might want to trigger a workflow whenever new pages are created or updated in Notion to sync your users' Notion pages to your application in real-time.

You can find the full list of Webhook Triggers for Notion below:

* **Page Created**
* **Page Updated**
