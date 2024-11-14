---
description: Connect to your users' Figma accounts.
---

# Figma

## Setup Guide

You can find your Figma app credentials in your [Figma Developer Account.](https://www.figma.com/plugin-docs/api/api-reference/)

You'll need the following information to set up your Figma App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Figma app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Figma App page.
* **Client Secret:** Found under Client Secret on your Figma App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Figma app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Figma

Once your users have connected their Figma account, you can use the Paragon SDK to access the Figma API on behalf of connected users.

See the Figma [REST API documentation](https://www.figma.com/plugin-docs/api/api-reference/) for their full API reference.

Any Figma API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get a File
paragon.request("figma", "/v1/files/:key", {
  method: "GET"
});

// Get a Project's Files
paragon.request("figma", "/v1/projects/:project_id/files", {
  method: "GET"
});
  
```

## Building Figma workflows

Once your Figma account is connected, you can add steps to perform the following actions:

* Get Files by ID
* Get File Node
* Get Rendered Image from File
* Get Users' Projects
* Get Project Files
* Create Comment
* Get Comments by File
* Delete Comment
* Create Comment Reaction
* Get Comment Reactions by File
* Delete Comment Reaction

You can also the Figma Request step to access any of Figma's API endpoints without the authentication piece.

When creating or updating records in Figma, you can reference data from previous steps by typing `{{` to invoke the variable menu.
