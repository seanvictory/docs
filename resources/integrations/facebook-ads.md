---
description: Connect to your users’ Facebook Ads accounts.
---

# Facebook Ads

## Setup Guide

You can find your Facebook Ads app credentials by visiting your [Facebook Developer App Settings.](https://developers.facebook.com/apps/)

{% hint style="info" %}
**Note:** You'll need to create a new Facebook Ads app if you don't already have one.
{% endhint %}

You'll need the following information to set up your Facebook Ads App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Facebook Ads app

Paragon provides a redirect URL to send information to your Facebook Ads app. To add the redirect URL to your Facebook Ads app:

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

### Add your Facebook Ads app to Paragon

1\. Select **Facebook Ads** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials in their respective sections:

* **Client ID:**
  1. Log in to your Facebook Ads [dashboard](https://developers.facebook.com/apps/).
  2. Select your application.
  3. Select **Settings >  Basic** from the sidebar.
  4. Copy the **App ID** to use in Paragon Connect.
* **Client Secret:**
  1. Log in to your Facebook Ads [dashboard](https://developers.facebook.com/apps/).
  2. Select your application.
  3. Select **Settings >  Basic** from the sidebar.
  4. Copy your **App Secret** to use in Paragon Connect.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Facebook Ads account to Paragon.png>)

## Connecting to Facebook Ads

Once your users have connected their Facebook Ads account, you can use the Paragon SDK to access Facebook Ads on behalf of connected users.

See the Facebook Ads [REST API documentation](https://developers.facebook.com/docs/marketing-apis/overview) for their full API reference.

Any Facebook Ads API endpoints can be accessed with the Paragon SDK as shown in this example.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration.

// Authenticate the user
paragon.authenticate(<ProjectID>, <Paragon User Token>);

// Get Campaigns
await paragon.request(‘facebookAds’, 'act_<AD_ACCOUNT_ID>/campaigns', {
  method: 'GET'
})

// Create a Campaign
await paragon.request('facebookAds', 'act_<AD_ACCOUNT_ID>/campaigns' , {
  method: 'POST',
  body: {
    name: "My First Campaign",
    objective: "POST_ENGAGEMENT",
    status: "PAUSED",
    special_ad_categories: []
  }
})
```
{% endtab %}
{% endtabs %}

## Building Facebook Ads workflows

Once your Facebook Ads account is connected, you can add steps to perform the following actions:

* Create Campaign
* Update Campaign
* Get Campaigns
* Get Campaign by ID
* Create Ad Set
* Update Ad Set
* Get Ad Sets
* Get Ad Set by ID
* Create Ad
* Update Ad
* Get Ad by ID
* Build Ad Creative Object
* Create Ad Creative
* Create Lead Gen Form
* Send Purchase Event
* Send Lead Event
* Send Other Event

When using Facebook Ads, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Facebook Ads Workflow.svg>)
