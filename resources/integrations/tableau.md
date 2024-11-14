---
description: Connect to your users' Tableau accounts
---

# Tableau

## Setup Guide

You can find your Tableau app credentials in your [Tableau Developer Account.](https://help.tableau.com/current/api/rest\_api/en-us/REST/rest\_api\_ref.htm)

You'll need the following information to set up your Tableau App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Tableau app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Tableau App page.
* **Client Secret:** Found under Client Secret on your Tableau App page.
* **Client Secret Value:** Found under Value on your Tableau App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Tableau app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Tableau

Once your users have connected their Tableau account, you can use the Paragon SDK to access the Tableau API on behalf of connected users.

See the Tableau [REST API documentation](https://help.tableau.com/current/api/rest\_api/en-us/REST/rest\_api\_ref.htm) for their full API reference.

Any Tableau API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get all Projects
paragon.request("tableau, "/projects", {
  method: "GET"
});

// Get all Jobs
paragon.request("tableau", "/jobs", {
  method: "GET"
});

```

## Building Tableau workflows

Once your Tableau account is connected, you use the Tableau Request step to access any of Tableau's API endpoints without the authentication piece.

When creating or updating records in Tableau, you can reference data from previous steps by typing `{{` to invoke the variable menu.
