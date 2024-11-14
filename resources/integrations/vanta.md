---
description: Connect to your users' Vanta accounts.
---

# Vanta

## Setup Guide

You can find your Vanta app credentials in your [Vanta Developer Account.](https://developer.vanta.com/reference)

You'll need the following information to set up your Vanta App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Vanta app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Vanta App page.
* **Client Secret:** Found under Client Secret on your Vanta App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Vanta app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Vanta

Once your users have connected their Vanta account, you can use the Paragon SDK to access the Vanta API on behalf of connected users.

See the Vanta [REST API documentation](https://developer.vanta.com/reference) for their full API reference.

Any Vanta API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// List SecurityTask
paragon.request('vanta', 'v1/resources/security_task/list_all?resourceId=<id>', {
  method: 'GET'
});
  
```

## Building Vanta workflows

Once your Vanta account is connected, you use the Vanta Request step to access any of Vanta's API endpoints without the authentication piece.

When creating or updating records in Vanta, you can reference data from previous steps by typing `{{` to invoke the variable menu.e
