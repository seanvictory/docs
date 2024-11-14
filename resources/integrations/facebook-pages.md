---
description: Connect to your users’ Facebook Pages accounts.
---

# Facebook Pages

## Setup Guide

You can find your Facebook Ads app credentials by visiting your [Facebook Developer App Settings.](https://developers.facebook.com/apps/)

{% hint style="info" %}
**Note:** You'll need to create a new Facebook Pages app if you don't already have one.
{% endhint %}

You'll need the following information to set up your Facebook Pages App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Facebook Pages app

Paragon provides a redirect URL to send information to your Facebook Pages app. To add the redirect URL to your Facebook Pages app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log into your [Facebook Developer Portal](https://developers.facebook.com/apps/).

3\. Select your app from the list of apps.

4\. Under **Add a product**, select **Facebook Login**.

5\. Under **Valid OAuth Redirect URIs**, paste-in the redirect URL from Paragon. The redirect URL can be found in Step 1.

6\. Press the blue  `Save changes` button to confirm your changes.

![](<../../.gitbook/assets/Adding the Facebook Ads redirect URL for Paragon Connect.png>)

### Add your Facebook Pages app to Paragon

1\. Select **Facebook** Pages from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials in their respective sections:

* **Client ID:**
  1. Log in to your Facebook Pages [dashboard](https://developers.facebook.com/apps/).
  2. Select your application.
  3. Select **Settings >  Basic** from the sidebar.
  4. Copy the **App ID** to use in Paragon Connect.
* **Client Secret:**
  1. Log in to your Facebook Pages [dashboard](https://developers.facebook.com/apps/).
  2. Select your application.
  3. Select **Settings >  Basic** from the sidebar.
  4. Copy your **App Secret** to use in Paragon Connect.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Facebook Pages app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Facebook Pages

Once your users have connected their Facebook Pages account, you can use the Paragon SDK to access Facebook Pages on behalf of connected users.

See the Facebook Pages [REST API documentation](https://developers.facebook.com/docs/pages) for their full API reference.

Any Facebook Pages endpoints can be accessed with the Paragon SDK as shown in this example.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration.

// Authenticate the user
paragon.authenticate(<ProjectID>, <Paragon User Token>);

// Post content to a Facebook Page
await paragon.request('facebookpages', '/feed', {
  method: 'POST',
  body: {
  'message': 'Hello Fans!'
  }
});

// Get Page Info
await paragon.request('facebookpages', '?fields=about,name,category,description,contact_address,emails,app_id,posts,username,verification_status,link,personal_info,phone', {
  method: 'GET'
});

// Get a single Metric
await paragon.request('facebookpages', '/insights/<metric-name>', {
  method: 'GET'
});
```
{% endtab %}
{% endtabs %}

## Building Facebook Pages workflows

Once your Facebook Pages account is connected, you use the Facebook Pages Request step to access any of Facebook Pages' API endpoints without the authentication piece.

When creating or updating records in Facebook Pages, you can reference data from previous steps by typing `{{` to invoke the variable menu.
