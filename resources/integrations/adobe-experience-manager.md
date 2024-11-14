---
description: Connect to your users' Adobe Experience Manager accounts
---

# Adobe Experience Manager

## Setup Guide

You can find your Adobe Experience Manager app credentials in your [Adobe Experience Manager Developer Account.](https://developer.adobe.com/dep/guides/postman/setup-environment/)

You'll need the following information to set up your Adobe Experience Manager App with Paragon Connect:

* Domain
* [Technical Account Details](https://experience.adobe.com/#/cloud-manager/landing.html)

## Connecting to Adobe Experience Manager

Once your users have connected their Adobe Experience Manager account, you can use the Paragon SDK to access the Adobe Experience Manager API on behalf of connected users.

See the Adobe Experience Manager [REST API documentation](https://developer.adobe.com/dep/guides/postman/setup-environment/) for their full API reference.

Any Adobe Experience Manager API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get a Folder
await paragon.request("adobeexperiencemanager", "/myFolder.json", {
    method: "GET"
});

// Create a Folder
await paragon.request("adobeexperiencemanager", "/*", {
    method: 'POST',
    body: {
      "name": "myAssetsFolder",
      "jcr:title": "My Assets Folder"
    }
});
  
```

## Building Adobe Experience Manager workflows

Once your Adobe Experience Manager account is connected, you can add steps to perform the following actions:

* Create Folder
* Delete Folder
* Delete Asset
* Create Asset Rendition
* Update Asset Rendition
* Delete Asset Rendition

You can also use the Adobe Experience Manager Request step to access any of Adobe Experience Manager's API endpoints without the authentication piece.

When creating or updating records in Adobe Experience Manager, you can reference data from previous steps by typing `{{` to invoke the variable menu.
