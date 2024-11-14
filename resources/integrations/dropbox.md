---
description: Connect to your users' Dropbox accounts.
---

# Dropbox

## Setup Guide

You can find your Dropbox app credentials in your [Dropbox Developer Account.](https://www.dropbox.com/developers/documentation/http/documentation)

You'll need the following information to set up your Dropbox App with Paragon Connect:

* App Key
* App Secret
* Scopes Requested

### Add the Redirect URL to your Dropbox app

Paragon provides a redirect URL to send information to your Dropbox app. To add the redirect URL to your Dropbox app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log into your [Dropbox Developer Portal](https://www.dropbox.com/developers/).

3\. Select your app from the list of apps.

5\. Under **Redirect URIs**, paste-in the redirect URL from Paragon. The redirect URL can be found in Step 1.

6\. Press the `Save` button to confirm your changes.

### Add your Dropbox app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **App Key:** Found under **Settings > App key** on your Dropbox App page.
* **App Secret** Found under **Settings > App secret** on your Dropbox App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Dropbox app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Dropbox

Once your users have connected their Dropbox account, you can use the Paragon SDK to access the Dropbox API on behalf of connected users.

See the Dropbox [REST API documentation](https://www.dropbox.com/developers/documentation/http/documentation) for their full API reference.

Any Dropbox API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Query files in Dropbox's root directory
paragon.request("dropbox", "/2/files/list_folder", {
  method: "POST",
  body: {
  {
    "include_deleted": false,
    "include_has_explicit_shared_members": false,
    "include_media_info": false,
    "include_mounted_folders": true,
    "include_non_downloadable_files": true,
    "path": "",
    "recursive": false
  }
});

// Move a file or folder to a different location.
paragon.request("dropbox", "/2/files/move_v2", {
  method: "POST",
  body: {
    "allow_ownership_transfer": false,
    "allow_shared_folder": false,
    "autorename": false,
    "from_path": "/Homework/math",
    "to_path": "/Homework/algebra"
  }
});

  
```

## Building Dropbox workflows

Once your Dropbox account is connected, you can add steps to perform the following actions:

* Save File
* Get File by Name
* List Files
* Create Folder
* Move Folder
* Get Folder by ID
* Search Folders
* Delete Folder

When creating or updating records in Dropbox, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Dropbox account. For example, you might want to trigger a workflow whenever new files are created in Dropbox to sync your users' Dropbox files to your application in real-time.

<figure><img src="../../.gitbook/assets/Dropbox Webhook Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Dropbox below:

* **File Created**
* **File Deleted**
* **File Updated**
