---
description: Connect to your users' Zoho People accounts.
---

# Zoho People

## Setup Guide

You can find your Zoho People app credentials in your [Zoho People Developer Account](https://api-console.zoho.com/).

You'll need the following information to set up your Zoho People App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Creating a Zoho People app

To get started, you'll need to create an app in the [Zoho API Console](https://api-console.zoho.com/).

1. Sign in with your Zoho People Developer Account.
2.  Click "**Add Client**" in the top right:\


    <figure><img src="../../.gitbook/assets/Screen Shot 2022-11-03 at 9.10.23 PM.png" alt=""><figcaption></figcaption></figure>
3.  Select "**Server-based Applications**" as the Client Type:\


    <figure><img src="../../.gitbook/assets/Screen Shot 2022-11-03 at 9.11.18 PM.png" alt=""><figcaption></figcaption></figure>
4. Add your website as the Homepage URL.
5. Add [https://passport.useparagon.com/oauth](https://passport.useparagon.com/oauth) as an **Authorized Redirect URI**.

### Add the Redirect URL to your Zoho People app

Paragon provides a redirect URL to send information to your Zoho CRM app. To add the redirect URL to your Zoho PeoplePeople app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your [Zoho People Developer Account](https://api-console.zoho.com/), select your application.

3\. Under **Authorized Redirect URIs**, paste-in the Paragon Connect redirect URL found in Step 1.

4\. Copy the Client ID and Client Secret provided by Zoho CRM.

### Add your Zoho People app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found at the end of [Step 1](zohopeople.md#add-the-redirect-url-to-your-zoho-people-app) on your Zoho People App page.
* **Client Secret:** Found at the end of [Step 1](zohopeople.md#add-the-redirect-url-to-your-zoho-people-app) on your Zoho People App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Zoho People app to Paragon Connect.png.png" alt=""><figcaption></figcaption></figure>

## Connecting to Zoho People

Once your users have connected their Zoho People account, you can use the Paragon SDK to access the Zoho People API on behalf of connected users.

See the Zoho People [REST API documentation](https://www.zoho.com/crm/developer/docs/api/v3/modules-api.html) for their full API reference.

Any Zoho People API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// List of view details available in all forms
await paragon.request('zohopeople', 'views', {
    method: 'GET'
});

// List of files categories
await paragon.request('zohopeople', 'files/getCategories', {
    method: 'GET'
});
            
// List of field components available in a form with ID
await paragon.request('zohopeople', 'forms/<formLinkName>/components', {
    method: 'GET'
});
```

## Building Zoho People workflows

Once your Zoho People account is connected, you use the Zoho People Request step to access any of Zoho People's API endpoints without the authentication piece.

When creating or updating records in Zoho People, you can reference data from previous steps by typing `{{` to invoke the variable menu.
