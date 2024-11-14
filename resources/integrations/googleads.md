# Google Ads

## Setup Guide

You can find your Google app credentials by visiting your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) and your [Google Ads manager](https://ads.google.com/home/tools/manager-accounts/) account.

You'll need the following information to set up your Google App with Paragon Connect:

* Client ID
* Client Secret
* Google Ads Developer Token
* Scopes Requested

{% hint style="info" %}
**Note:** You'll need to create a new project in Google Cloud Console if you don't already have one.
{% endhint %}

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
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

![](<../../.gitbook/assets/Selecting Web Application in Google OAuth.png>)

{% hint style="info" %}
**Note:** You'll need to configure Google's [consent screen](https://console.developers.google.com/apis/credentials) for access to **Client ID** and **Client Secret** if you haven't already.
{% endhint %}

5\. Under **Authorized redirect URIs**, press the "**+ Add URI**" button.

6\. Paste-in the redirect URL from Paragon.

7\. Press the blue "**Create**" button.

![](<../../.gitbook/assets/Connect - Adding Google redirect URI for OAuth.gif>)

Google provides you with the **Client ID** and **Client Secret** needed for the next steps after adding the redirect URL to your project.

### Enable Google Ads API in Google Cloud Console Dashboard

1\. In your Google Cloud Console dashboard, navigate to **APIs & Services > Library** in the sidebar.

2\. Search for "Google Ads API" from the API Library.

3\. Select the "Google Ads API".

4\. Press the blue "**Enable**" button to enable the API for your application.

<figure><img src="../../.gitbook/assets/Enabling the Google Ads API for Paragon Connect.png" alt=""><figcaption></figcaption></figure>

### Obtain a Google Ads Developer Token in Google Ads Manager Account

A Google Ads Developer Token is required to use the Google Ads API. This token serves as an identifier for your app when accessing the Google Ads API, and must be applied for within your [Google Ads Manager account](https://ads.google.com/home/tools/manager-accounts/).

* For initial testing, you may receive a Test Developer Token that allows API requests in a sandbox environment.
* For production use, you’ll need to get your Developer Token approved by Google. Once approved, it can be used to make real API calls.

Navigate to your [Google Ads Manager account](https://ads.google.com/home/tools/manager-accounts/) and search for the **API Center.** Here you can begin the process to request a Developer Token. [For more information, refer to the Google Ads API docs here.](https://developers.google.com/google-ads/api/docs/get-started/dev-token)

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-03 at 10.06.12@2x.png" alt=""><figcaption></figcaption></figure>

### Add your Google app to Paragon

1\. Select **Google Ads** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](googleads.md#add-the-redirect-url-to-your-google-app) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.
* **Developer Token**: Found at the end of the previous step.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-03 at 10.28.41.png" alt=""><figcaption></figcaption></figure>

## Connecting to Google Ads

Once your users have connected their Google Ads account, you can use the Paragon SDK to access the Google Ads API on behalf of connected users.

See the Google Ads [REST API documentation](https://developers.google.com/google-ads/api/reference/rpc/v11/overview) for their full API reference.

Any Google Ads API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Fetch Campaign Data
paragon.request("googleads", "/customers/<Customer ID>/campaigns/<Campaign ID>", {
  method: "GET"
});

// Create a campaign with an existing Campaign Budget
paragon.request("googleads", "/customers/<Customer ID>/campaignBudgets:mutate", {
  method: "POST",
  body: {
    status: 'PAUSED',
    advertisingChannelType: 'SEARCH',
    geoTargetTypeSetting: {
      positiveGeoTargetType: 'PRESENCE_OR_INTEREST',
      negativeGeoTargetType: 'PRESENCE_OR_INTEREST'
    },
    name: 'My Search campaign',
    campaignBudget: 'customers/<Customer ID>/campaignBudgets/<Budget ID>',
    targetSpend: {}
  }
});
  
```

## Building Google Ads workflows

Once your Google Ads account is connected, you use the Google Ads Request step to access any of Google Ads's API endpoints without the authentication piece.

When creating or updating records in Google Ads, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Publishing your Google Ads application

### Setting up a Redirect Page in your app <a href="#setting-up-a-redirect-page-in-your-app" id="setting-up-a-redirect-page-in-your-app"></a>

Your Google Ads integration requires a Redirect Page hosted in your application to support verification of your application by Google.

The Redirect Page should be implemented as follows:

* Receives a `GET` request with a number of query parameters.
* Redirect to `https://passport.useparagon.com/oauth` with the same query parameters.

```javascript
paragon.connect("googleads", {
  overrideRedirectUrl: "https://your-app.url/google-drive-redirect"
});
```

### Updating the allowed Redirect URL <a href="#updating-the-allowed-redirect-url" id="updating-the-allowed-redirect-url"></a>

If you were previously testing with `https://passport.useparagon.com/oauth` as your Google Ads Redirect URL, you will need to update this value after implementing a Redirect Page:

1. Log into your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) and select your application.
2. Navigate to **APIs & Services > Credentials** and select the credentials you use with Paragon.
3. Under **Authorized redirect URIs**, provide the URL of your Redirect Page.
