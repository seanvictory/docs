---
description: Connect to your users' Vimeo accounts.
---

# Vimeo

## Setup Guide

You can find your Vimeo app credentials in your [Vimeo Developer Account.](https://developer.vimeo.com/api)

You'll need the following information to set up your Vimeo App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Vimeo app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Vimeo App page.
* **Client Secret:** Found under Client Secret on your Vimeo App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Vimeo app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Vimeo

Once your users have connected their Vimeo account, you can use the Paragon SDK to access the Vimeo API on behalf of connected users.

See the Vimeo [REST API documentation](https://developer.vimeo.com/api) for their full API reference.

Any Vimeo API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Search for Videos
paragon.request("vimeo", "/videos?query=[Search Query]", {
  method: "GET"
});
// Edit a Video's Metadata
paragon.request("vimeo", "/videos/[Video ID]", {
  method: "PATCH",
  body: {
    "name": "New video name"
  }
});
// Get Video Subtitles
paragon.request("vimeo", "/videos/[Video ID]/texttracks", {
  method: "GET"
});
  
```

## Building Vimeo workflows

Once your Vimeo account is connected, you use the Vimeo Request step to access any of Vimeo's API endpoints without the authentication piece.

When creating or updating records in Vimeo, you can reference data from previous steps by typing `{{` to invoke the variable menu.
