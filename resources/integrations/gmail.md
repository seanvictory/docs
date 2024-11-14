---
description: Connect to your users' Gmail accounts
---

# Gmail

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

### Enable Email API in Google Cloud Console Dashboard

1\. In your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project), navigate to **APIs & Services > Library** in the sidebar.

2\. Search for "Gmail" from the API Library.

3\. Select the "Gmail API".

4\. Press the blue "**Enable**" button to enable the API for your application.

![](<../../.gitbook/assets/Choosing the Gmail API in the Google Cloud Console Dashboard.png>)

### Add your Google app to Paragon

1\. Select **Gmail** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](google-sheets.md#1-add-the-redirect-url-to-your-google-app) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.
* **Permissions:** Select the scopes you've requested for your application. They should begin with `gmail`.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting a new Google app to Paragon Connect.png>)

## Connecting to Gmail

Once your users have connected their Gmail account, you can use the Paragon SDK to access the Gmail API on behalf of connected users.

See the Gmail [REST API documentation](https://developers.google.com/gmail/api/reference/rest) for their full API reference.

Any Gmail API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Send an email on behalf of a specified user
paragon.request("gmail", "/upload/gmail/v1/users/{userId}/messages/send", {
  method: "POST",
  body: {
    "raw": <Base64-encoded email>
  }
});

// Get all emails associated with a specified user
paragon.request("gmail", "gmail/v1/users/{userId}/messages", {
  method: "GET"
});
  
```

## Building Gmail workflows

Once your Gmail account is connected, you can add steps to perform the following actions:

* Send Email
* Get Email by ID
* Search for Email
* Delete Email
* Create a Contact
* Get Contact by Resource Name
* Search for Contact
* Delete Contact

When creating or getting emails in Gmail, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Gmail account. For example, you might want to trigger a workflow whenever new threads are created in Gmail to sync your users' Gmail threads to your application in real-time.

<figure><img src="../../.gitbook/assets/Gmail Webhook Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Gmail below:

* **New Thread Created**
* **Thread Updated**
* **Thread Modified**

## Publishing your Gmail application

### Setting up a Redirect Page in your app <a href="#setting-up-a-redirect-page-in-your-app" id="setting-up-a-redirect-page-in-your-app"></a>

Your Gmail integration requires a Redirect Page hosted in your application to support verification of your application by Google.

The Redirect Page should be implemented as follows:

* Receives a `GET` request with a number of query parameters.
* Redirect to `https://passport.useparagon.com/oauth` with the same query parameters.

```javascript
paragon.connect("gmail", {
  overrideRedirectUrl: "https://your-app.url/gmail-redirect"
});
```

### Updating the allowed Redirect URL <a href="#updating-the-allowed-redirect-url" id="updating-the-allowed-redirect-url"></a>

If you were previously testing with `https://passport.useparagon.com/oauth` as your Gmail Redirect URL, you will need to update this value after implementing a Redirect Page:

1. Log into your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) and select your application.
2. Navigate to **APIs & Services > Credentials** and select the credentials you use with Paragon.
3. Under **Authorized redirect URIs**, provide the URL of your Redirect Page.
