---
description: Connect your Google Docs app for OAuth in Paragon
---

# Google Docs

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

### Enable Google Docs API in Google Cloud Console Dashboard

1\. In your [Google Cloud Console dashboard,](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) navigate to **APIs & Services > Library** in the sidebar.

2\. Search for "Google Docs API" from the API Library.

3\. Select the "Google Docs API".

4\. Press the blue "**Enable**" button to enable the API for your application.

<figure><img src="../../.gitbook/assets/Enabling the Google Docs API.png" alt=""><figcaption></figcaption></figure>

### Add your Google app to Paragon

1\. Select **Google Docs** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](googledocs.md#setup-guide) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.
* **Permissions:** Select the scopes you've requested for your application. They should contain  `/documents`.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Google Docs app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

Once your users have connected their Google Docs account, you can use the Paragon SDK to access the Google Docs API on behalf of connected users.

See the Google Docs [REST API documentation](https://developers.google.com/docs/api/how-tos/overview) for their full API reference.

Any Google Docs API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get the latest version of the specified document
await paragon.request("googledocs", "/v1/documents/<documentId>", {
  method: "GET"
});

// Create a blank document with the provided title
await paragon.request("googledocs", "/v1/documents", {
  method: "POST",
  body: {
    "title": "My Document",
  }
});
```

## **Building Google** Docs **workflows**

When saving or getting files in Google Docs, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Publishing your Google Docs application

### Setting up a Redirect Page in your app <a href="#setting-up-a-redirect-page-in-your-app" id="setting-up-a-redirect-page-in-your-app"></a>

Your Google Docs integration requires a Redirect Page hosted in your application to support verification of your application by Google.

The Redirect Page should be implemented as follows:

* Receives a `GET` request with a number of query parameters.
* Redirect to `https://passport.useparagon.com/oauth` with the same query parameters.

```javascript
paragon.connect("googledocs", {
  overrideRedirectUrl: "https://your-app.url/google-docs-redirect"
});
```

### Updating the allowed Redirect URL <a href="#updating-the-allowed-redirect-url" id="updating-the-allowed-redirect-url"></a>

If you were previously testing with `https://passport.useparagon.com/oauth` as your Google Docs Redirect URL, you will need to update this value after implementing a Redirect Page:

1. Log into your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) and select your application.
2. Navigate to **APIs & Services > Credentials** and select the credentials you use with Paragon.
3. Under **Authorized redirect URIs**, provide the URL of your Redirect Page.
