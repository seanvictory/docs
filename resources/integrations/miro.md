---
description: Connect to your users' Miro accounts
---

# Miro

## Setup Guide

You can find your Miro app credentials in your [Miro Developer Account.](https://developers.miro.com/docs/getting-started-with-oauth)

You'll need the following information to set up your Miro App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Miro app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Miro App page.
* **Client Secret:** Found under Client Secret on your Miro App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Miro app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Miro

Once your users have connected their Miro account, you can use the Paragon SDK to access the Miro API on behalf of connected users.

See the Miro [REST API documentation](https://developers.miro.com/docs/getting-started-with-oauth) for their full API reference.

Any Miro API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Boards
paragon.request("miro", "/boards", {
  method: "GET"
});

// Create a Board
paragon.request("miro", "/boards", {
  method: "POST",
  body: {
    description: 'This board was created over the API',
    name: 'My Board',
    policy: {
      permissionsPolicy: {
        collaborationToolsStartAccess: 'all_editors',
        copyAccess: 'anyone',
        sharingAccess: 'team_members_with_editing_rights'
      },
      sharingPolicy: {
        access: 'private',
        inviteToAccountAndBoardLinkAccess: 'no_access',
        organizationAccess: 'private',
        teamAccess: 'private'
      }
    },
    teamId: '<MIRO_TEAM_ID>',
    projectId: '<MIRO_PROJECT_ID>'
  }
});
  
```

## Building Miro workflows

Once your Miro account is connected, you use the Miro Request step to access any of Miro's API endpoints without the authentication piece.

When creating or updating records in Miro, you can reference data from previous steps by typing `{{` to invoke the variable menu.
