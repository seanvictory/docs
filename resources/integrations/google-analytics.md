---
description: Connect to your users' Google Analytics accounts.
---

# Google Analytics

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

2\. Search for "Google Analytics API" and "Google Analytics Reporting API" from the API Library.

3\. Select the "Google Analytics API" and "Google Analytics Reporting API".

4\. Press the blue "**Enable**" button to enable the API for your application.

![](<../../.gitbook/assets/Enabling the Google Analytics APIs for Paragon Connect.png>)

### Add your Google app to Paragon

1\. Select **Google Analytics** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](google-calendar.md#add-the-redirect-url-to-your-google-app) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.
* **Permissions:** Select the scopes you've requested for your application. They should begin with `analytics`.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting a new Google app to Paragon Connect.png>)

## Connecting to Google Analytics

Once your users have connected their Google Analytics account, you can use the Paragon SDK to access the Google Analytics API on behalf of connected users.

See the Google Analytics [REST API documentation](https://developers.google.com/analytics/devguides/config/mgmt/v3) for their full API reference.

Any Google Analytics API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get accounts the user has access to
await paragon.request("googleanalytics", "https://www.googleapis.com/analytics/v3/management/accounts", {
  method: "GET"
});
              
// Get goals for an account and web property
await paragon.request("googleanalytics","https://www.googleapis.com/analytics/v3/management/accounts/<Account ID>/webproperties/<Web Property ID>/profiles/<Profile ID>/goals", {
    method: "GET"
  });
  
// Run analytics query for a view
await paragon.request("googleanalytics", "https://analyticsreporting.googleapis.com/v4/reports:batchGet", {
  method: "POST",
  body: {
    reportRequests: [{
      viewId: "<View ID>"
    }],
    useResourceQuotas: true
  }
});

```

## **Building Google Analytics workflows**

Once your Google Analytics account is connected, you can add steps to perform the following actions:

* Run Report
* Get Realtime Data
* Get Custom Metrics
* Get Custom Dimensions

When creating or updating events in Google Analytics, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Publishing your Google Analytics application

### Setting up a Redirect Page in your app <a href="#setting-up-a-redirect-page-in-your-app" id="setting-up-a-redirect-page-in-your-app"></a>

Your Google Analytics integration requires a Redirect Page hosted in your application to support verification of your application by Google.

The Redirect Page should be implemented as follows:

* Receives a `GET` request with a number of query parameters.
* Redirect to `https://passport.useparagon.com/oauth` with the same query parameters.

```javascript
paragon.connect("googleanalytics", {
  overrideRedirectUrl: "https://your-app.url/google-analytics-redirect"
});
```

### Updating the allowed Redirect URL <a href="#updating-the-allowed-redirect-url" id="updating-the-allowed-redirect-url"></a>

If you were previously testing with `https://passport.useparagon.com/oauth` as your Google Analytics Redirect URL, you will need to update this value after implementing a Redirect Page:

1. Log into your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) and select your application.
2. Navigate to **APIs & Services > Credentials** and select the credentials you use with Paragon.
3. Under **Authorized redirect URIs**, provide the URL of your Redirect Page.
