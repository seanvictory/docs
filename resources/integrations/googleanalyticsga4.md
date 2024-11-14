---
description: Connect to your users' Google Analytics GA4 accounts.
---

# Google Analytics GA4

## Setup Guide

You can find your Google app credentials by visiting your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project).&#x20;

You'll need the following information to set up your Google App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
**Note:** You'll need to create a new project in Google Cloud Console if you don't already have one.
{% endhint %}

### Add the Redirect URL to your Google app

Paragon provides a redirect URL to send information to your Google app. To add the redirect URL to your Google app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project), navigate to **APIs & Services > Credentials** in the sidebar.

3\. Press "**+ Create Credentials**", then select **OAuth client ID.**

4\. Select "**Web application**" from the Application type drop-down menu.

{% hint style="info" %}
**Note:** You'll need to configure Google's [consent screen](https://console.developers.google.com/apis/credentials) for access to **Client ID** and **Client Secret** if you haven't already.
{% endhint %}

![](<../../.gitbook/assets/Selecting Web Application in Google OAuth.png>)

5\. Under **Authorized redirect URIs**, press the "**+ Add URI**" button.

6\. Paste-in the redirect URL from Paragon.

7\. Press the blue "**Create**" button.

![](<../../.gitbook/assets/Connect - Adding Google redirect URI for OAuth.gif>)

Google provides you with the **Client ID** and **Client Secret** needed for the next steps after adding the redirect URL to your project.

### Enable Google Analytics API in Google Cloud Console Dashboard

1\. In your Google Cloud Console dashboard, navigate to **APIs & Services > Library** in the sidebar.

2\. Search for "Google Analytics Data API" from the API Library.

3\. Select the "Google Analytics Data API".

4\. Press the blue "**Enable**" button to enable the API for your application.

<figure><img src="../../.gitbook/assets/Enabling Google Analytics Data API.png" alt=""><figcaption></figcaption></figure>

### Add your Google app to Paragon

1\. Select **Google Analytics GA4** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](google-calendar.md#add-the-redirect-url-to-your-google-app) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.
* **Permissions:** Select the scopes you've requested for your application. They should begin with `analytics`.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Google Analytics GA4 app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Google Analytics

Once your users have connected their Google Analytics account, you can use the Paragon SDK to access the Google Analytics API on behalf of connected users.

See the Google Analytics [REST API documentation](https://developers.google.com/analytics/devguides/config/mgmt/v3) for their full API reference.

Any Google Analytics API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Generate Realtime Reports in Google Analytics GA4
await paragon.request('googleanalyticsGA4', 'v1beta/properties/propertyId:runRealtimeReport', {
  method: 'POST',
  body: {
    "dimensions": [
        {
          "name": "country"
        }
      ],
      "metrics": [
        {
          "name": "activeUsers"
        }
      ]
    }
});
              
// Get Audience List from Google Analytics GA4
await paragon.request('googleanalyticsGA4', 'v1alpha/properties/propertyID/audienceLists', {
  method: 'GET'
});

```

## **Building Google Analytics GA4 workflows**

Once your Google Analytics GA4 account is connected, you use the Google Analytics GA4 Request step to access any of Google Analytics GA4 API endpoints without the authentication piece.

When creating or updating records in Google Analytics GA4, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Publishing your Google Analytics GA4 application

### Setting up a Redirect Page in your app <a href="#setting-up-a-redirect-page-in-your-app" id="setting-up-a-redirect-page-in-your-app"></a>

Your Google Analytics GA4 integration requires a Redirect Page hosted in your application to support verification of your application by Google.

The Redirect Page should be implemented as follows:

* Receives a `GET` request with a number of query parameters.
* Redirect to `https://passport.useparagon.com/oauth` with the same query parameters.

```javascript
paragon.connect("googleanalyticsGA4", {
  overrideRedirectUrl: "https://your-app.url/google-analytics-GA4-redirect"
});
```

### Updating the allowed Redirect URL <a href="#updating-the-allowed-redirect-url" id="updating-the-allowed-redirect-url"></a>

If you were previously testing with `https://passport.useparagon.com/oauth` as your Google Analytics GA4 Redirect URL, you will need to update this value after implementing a Redirect Page:

1. Log into your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) and select your application.
2. Navigate to **APIs & Services > Credentials** and select the credentials you use with Paragon.
3. Under **Authorized redirect URIs**, provide the URL of your Redirect Page.

