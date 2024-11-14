---
description: Connect your Google Drive app for OAuth in Paragon
---

# Google Drive

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

### Enable Google Drive API in Google Cloud Console Dashboard

1\. In your [Google Cloud Console dashboard,](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) navigate to **APIs & Services > Library** in the sidebar.

2\. Search for "Google Drive API" from the API Library.

3\. Select the "Google Drive API".

4\. Press the blue "**Enable**" button to enable the API for your application.

![](<../../.gitbook/assets/Enabling Google Drive API.png>)

### Add your Google app to Paragon

1\. Select **Google Drive** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](google-drive.md#1-add-the-redirect-url-to-your-google-app) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.
* **Permissions:** Select the scopes you've requested for your application. They should begin with `drive`.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting a new Google app to Paragon Connect.png>)

## Connecting to Google Drive

Once your users have connected their Google Drive account, you can use the Paragon SDK to access the Google Drive API on behalf of connected users.

See the Google Drive [REST API documentation](https://developers.google.com/drive/api/v3/reference) for their full API reference.

Any Google Drive API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Query Files
await paragon.request("googledrive", `/files?q=${
  encodeURIComponent('name="test"')
}`, {
  method: "GET"
});
```

## **Building Google Drive workflows**

Once your Google Drive account is connected, you can add steps to perform the following actions:

* Get File by ID
* Save File
* Export Google Doc
* Create Folder
* Delete Folder
* Get Folder by ID
* Move Folder
* Get Files
* Search Folders

When saving or getting files in Google Drive, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Google Drive account. For example, you might want to trigger a workflow whenever new files are created in Google Drive to sync your users' Google Drive files to your application in real-time.

<figure><img src="../../.gitbook/assets/Google Drive Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Google Drive below:

* **File Created**
* **File Updated**
* **File Deleted**

## Using the Google Drive File Picker

You can allow your user to select files from their Google Drive account in your app with the Paragon SDK.

<figure><img src="../../.gitbook/assets/CleanShot 2023-10-18 at 11.47.47.gif" alt="" width="563"><figcaption></figcaption></figure>

**Enable the Google Picker API**

You will need to enable the Google Picker API for your application in order to access the File Picker.

1\. In your [Google Cloud Console dashboard,](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) navigate to **APIs & Services > Library** in the sidebar.

2\. Search for "Google Picker API" from the API Library.

3\. Select the "Google Picker  API".

4\. Press the blue "**Enable**" button to enable the API for your application.

<figure><img src="../../.gitbook/assets/Enabling the Google Picker API for a Google Drive integraiton for Paragon Connect.png" alt=""><figcaption></figcaption></figure>

**Creating a Google Drive API Key**

To show the Google Drive File Picker, you will need a **Google Drive API Key**. This key is a separate key from the Client ID you provided to Paragon during integration setup.

1. Navigate to the [Google Cloud Console > APIs & Services > Credentials](https://console.cloud.google.com/apis/credentials). Make sure the selected project in the header is your app.
2. Click Create Credentials.
3. Select API key.
4. An API Key value will appear. Copy this value to use in the next step.

<figure><img src="../../.gitbook/assets/[Credentials – APIs &#x26; Services – example – Google Cloud console] 2023-11-03 at 05.47.56 PM@2x (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**: While the API Key value is not sensitive and can safely be used in your public application, we recommend restricting the API Key with the following settings:

* Application restrictions: Websites with your origin/domain
* API restrictions: Google Drive API

[Read more](https://cloud.google.com/docs/authentication/api-keys#api\_key\_restrictions) in Google's docs for API Key restrictions.
{% endhint %}

#### **Showing the File Picker**

Use the Paragon SDK in your frontend application to show the File Picker in your app.

The SDK provides an `ExternalFilePicker` class to load Google's JavaScript into your page and authenticate with your user's connected Google Drive account.

```javascript
let picker = new paragon.ExternalFilePicker("googledrive", {
    onFileSelect: (files) => {
        // Handle file selection
    }
});

// Loads external dependencies and user's access token
await picker.init({ developerKey: "YOUR_GOOGLE_API_KEY" });

// Open the File Picker
picker.open();
```

You can configure the File Picker to listen for additional callbacks or to restrict allowed file types. Learn more about configuring File Picker options in the [SDK Reference](../../api/api-reference/#externalfilepicker).

#### Downloading the Selected File

The Google File Picker callback will return a `Response` object describing the user's file picker interaction including an array of any files selected. Using this array of `fileIds`, you can use the Connect API to perform an authenticated proxy requests to download the files.

{% hint style="info" %}
**Note:** Files containing binary content (including photos and videos) should be downloaded using the `files.get` endpoint whereas Google Workspace Documents can be downloaded using `files.export.`
{% endhint %}

{% tabs %}
{% tab title="Download a File" %}
```javascript
// Downloading a non-Google Workspace File like images and videos
await paragon.request('googledrive', '/files/<fileId>?alt=media', {
	method: 'GET'
});
```
{% endtab %}

{% tab title="Export a Google Doc" %}
```javascript
await paragon.request('googledrive', '/files/<fileId>/export?mimeType=<supportedMimeType>/pdf', {
	method: 'GET'
});

// TODO: Should we put backend usage?

POST https://api.useparagon.com/projects/19d...012/sdk/proxy/googledrive/files/<fileId>/export?mimeType=<supportedMimeType>/pdf

Authorization: Bearer eyJ...
Content-Type: application/json

```
{% endtab %}
{% endtabs %}

## Publishing your Google Drive application

### Setting up a Redirect Page in your app <a href="#setting-up-a-redirect-page-in-your-app" id="setting-up-a-redirect-page-in-your-app"></a>

Your Google Drive integration requires a Redirect Page hosted in your application to support verification of your application by Google.

The Redirect Page should be implemented as follows:

* Receives a `GET` request with a number of query parameters.
* Redirect to `https://passport.useparagon.com/oauth` with the same query parameters.

```
paragon.connect("googledrive", {
  overrideRedirectUrl: "https://your-app.url/google-drive-redirect"
});
```

### Updating the allowed Redirect URL <a href="#updating-the-allowed-redirect-url" id="updating-the-allowed-redirect-url"></a>

If you were previously testing with `https://passport.useparagon.com/oauth` as your Google Drive Redirect URL, you will need to update this value after implementing a Redirect Page:

1. Log into your [Google Cloud Console dashboard](https://console.cloud.google.com/projectselector2/home/dashboard?supportedpurview=project) and select your application.
2. Navigate to **APIs & Services > Credentials** and select the credentials you use with Paragon.
3. Under **Authorized redirect URIs**, provide the URL of your Redirect Page.

