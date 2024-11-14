---
description: Connect to your users' Box accounts
---

# Box

## Setup Guide

You can find your Box app credentials in your [Box Developer Account.](https://developer.box.com/reference/)

You'll need the following information to set up your Box App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Box app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Box App page.
* **Client Secret:** Found under Client Secret on your Box App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Box app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Box

Once your users have connected their Box account, you can use the Paragon SDK to access the Box API on behalf of connected users.

See the Box [REST API documentation](https://developer.box.com/reference/) for their full API reference.

Any Box API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get File Information
await paragon.request("box", "/files/:file_id", {
  method: "GET"
});

// Copy a file
await paragon.request("box", "/files/:file_id/copy", {
  method: "POST",
  body: {
    "parent":{
      "id": "123"
    }
  }
});

// List all collections
await paragon.request("box", "/collections", {
  method: "GET"
});
  
```

## Building Box workflows

Once your Box account is connected, you can add steps to perform the following actions:

* Save File
* Get File by ID
* List Files
* Create Folder
* Move Folder
* Get Folder by ID
* Search Folders
* Delete Folders

You can also use the Box Request step to access any of Box's API endpoints without the authentication piece.

When creating or updating records in Box, you can reference data from previous steps by typing `{{` to invoke the variable menu.
