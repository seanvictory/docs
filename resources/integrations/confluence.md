---
description: Connect to your users' Confluence accounts.
---

# Confluence

## Setup Guide

You can find your Confluence app credentials in your [Confluence Developer Account.](https://developer.atlassian.com/cloud/confluence/rest/v1/intro)

You'll need the following information to set up your Confluence App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Confluence app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Confluence App page.
* **Client Secret:** Found under Client Secret on your Confluence App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Confluence app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Confluence

Once your users have connected their Confluence account, you can use the Paragon SDK to access the Confluence API on behalf of connected users.

See the Confluence [REST API documentation](https://developer.atlassian.com/cloud/confluence/rest/v1/intro) for their full API reference.

Any Confluence API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Retrieve Pages
paragon.request("confluence", "/wiki/api/v2/pages", {
  method: "GET"
});

// Create a Page
paragon.request("confluence", "/wiki/api/v2/pages", {
  method: "POST",
  body: {
    "spaceId": 15,
    "status": "current",
    "title": "<string>",
    "body": {
      "representation": "storage",
      "value": "<string>"
    }
  }
});
  
```

## Building Confluence workflows

Once your Confluence account is connected, you can add steps to perform the following actions:

* Create Page
* Update Page
* Get Page by ID
* Get Pages in Space
* Get Pages by Label
* Search Pages
* Delete Page
* Get Space By ID
* Search Spaces

You can also the Confluence Request step to access any of Confluence's API endpoints without the authentication piece.

When creating or updating records in Confluence, you can reference data from previous steps by typing `{{` to invoke the variable menu.
