---
description: Connect to your users' LinkedIn accounts.
---

# LinkedIn

## Setup Guide

You can find your LinkedIn app credentials in your [LinkedIn Developer Account.](https://learn.microsoft.com/en-us/linkedin/consumer/integrations/self-serve/share-on-linkedin?context=linkedin%2Fconsumer%2Fcontext)

You'll need the following information to set up your LinkedIn App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your LinkedIn app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your LinkedIn App page.
* **Client Secret:** Found under Auth > OAuth 2.0 Client Secret on your LinkedIn App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your LinkedIn app to Paragon Connect.png" alt="Connecting your LinkedIn app to Paragon Connect"><figcaption></figcaption></figure>

## Connecting to LinkedIn

Once your users have connected their LinkedIn account, you can use the Paragon SDK to access the LinkedIn API on behalf of connected users.

See the LinkedIn [REST API documentation](https://learn.microsoft.com/en-us/linkedin/consumer/integrations/self-serve/share-on-linkedin?context=linkedin%2Fconsumer%2Fcontext) for their full API reference.

Any LinkedIn API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a post on LinkedIn
await paragon.request("linkedin", "/v2/ugcPosts", {
  method: "POST",
  body: {
      "author": "urn:li:organization:5515715",
      "commentary": "Sample text Post",
      "visibility": "PUBLIC",
      "distribution": {
        "feedDistribution": "MAIN_FEED",
        "targetEntities": [],
        "thirdPartyDistributionChannels": []
      },
      "lifecycleState": "PUBLISHED",
      "isReshareDisabledByAuthor": false
    }
});

// Get a profile by ID
await paragon.request("linkedin", "/v2/people/:id", {
  method: "GET",
});  
```

## Building LinkedIn workflows

Once your LinkedIn account is connected, you can add steps to perform the following actions:

* Get Profile by ID
* Create Post

You can also use the LinkedIn Request step to access any of LinkedIn's API endpoints without the authentication piece.

When creating or updating records in LinkedIn, you can reference data from previous steps by typing `{{` to invoke the variable menu.
