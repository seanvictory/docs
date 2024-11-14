---
description: Connect to your users' Adobe Acrobat Sign accounts
---

# Adobe Acrobat Sign

## Setup Guide

You can find your Adobe Acrobat Sign app credentials in your [Adobe Acrobat Sign Developer Account.](https://opensource.adobe.com/acrobat-sign/developer\_guide/index.html)

You'll need the following information to set up your Adobe Acrobat Sign App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Adobe Acrobat Sign app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Adobe Acrobat Sign App page.
* **Client Secret:** Found under Client Secret on your Adobe Acrobat Sign App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Adobe Acrobat SIgn app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Adobe Acrobat Sign

Once your users have connected their Adobe Acrobat Sign account, you can use the Paragon SDK to access the Adobe Acrobat Sign API on behalf of connected users.

See the Adobe Acrobat Sign [REST API documentation](https://opensource.adobe.com/acrobat-sign/developer\_guide/index.html) for their full API reference.

Any Adobe Acrobat Sign API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Agreements for the Connected User
paragon.request("acrobatsign", "/agreements", {
  method: "GET"
});

// Get the Status of an Agreement
paragon.request("acrobatsign", "/agreements/<AGREEMENT_ID>", {
  method: "GET"
});

// Create an Agreement for signature request
paragon.request("acrobatsign", "/agreements", {
  method: "POST",
  body: {
    "fileInfos": [
      {
        "transientDocumentId": ""
      }
    ],
    "name": "My Document Agreement",
    "participantSetsInfo": [
      {
        "order": 1,
        "role": "",
        "memberInfos": [
          {
            "email": "bowie@useparagon.com"
          }
        ]
      }
    ],
    "signatureType": "",
    "state": ""
  }
});
  
```

## Building Adobe Acrobat Sign workflows

Once your Adobe Acrobat Sign account is connected, you use the Adobe Acrobat Sign Request step to access any of Adobe Acrobat Sign's API endpoints without the authentication piece.

When creating or updating records in Adobe Acrobat Sign, you can reference data from previous steps by typing `{{` to invoke the variable menu.
