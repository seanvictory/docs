---
description: Connect to your users' OneDrive accounts
---

# OneDrive

## Setup Guide

You can find your OneDrive application credentials by visiting your Microsoft Azure Portal.

You'll need the following information to set up your OneDrive app with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* A [Microsoft Azure](https://azure.microsoft.com/) account

### Add the Redirect URL to your OneDrive app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your OneDrive app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/) using your Microsoft account.

3\. Navigate to **All Services > App Registrations** and select your application.

4\. Select **Authentication** from the sidebar.

5\. Under **Platform configurations**, press the  **"Add a platform"** button.

6\. Select the **Web** platform.

7\. Paste the Redirect URL from Step 1 under Redirect URIs.

8\. Press the **Save** button at the top of the page.

### Generate a Client Secret

Since OneDrive does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Enable Multi-tenancy to your OneDrive app

To allow Microsoft users from outside of your organization to connect to your OneDrive application, you must specify this as an option within the OneDrive application registration.

1. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/) using your Microsoft account.
2. Navigate to **All Services > App Registrations** and select your application.
3. Select **Authentication** from the sidebar.
4. Under **Supported account types**, press the  **"Accounts in any organizational directory"** option.
5. Click Save.

### Add your OneDrive app to Paragon

1\. Select **OneDrive** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](onedrive.md#add-the-redirect-url-to-your-onedrive-app) in their respective sections:

* **Client ID:** Found under **Essentials > Application (client) ID** on your Microsoft Azure Portal app page.
* **Client Secret:**
  1. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/).
  2. Navigate to **Manage > Certificates & secrets** in the sidebar.
  3. Under **Client Secrets**, press the **+ New client secret** button.&#x20;
  4. Name your client credentials and select an expiry that works best for your application.
  5. Press **Add** to create your credentials.
  6. Copy the displayed Client Secret under the **Value** column.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** You should only add the scopes you've requested in your application page to Paragon.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your OneDrive app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to OneDrive

Once your users have connected their OneDrive account, you can use the Paragon SDK to access the OneDrive API on behalf of connected users.

See the OneDrive [REST API documentation](https://docs.microsoft.com/en-us/dynamics365/sales-enterprise/help-hub) for their full API reference.

Any OneDrive API endpoints can be accessed with the Paragon SDK as shown in this example:

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// List files in the root of the drive
await paragon.request("onedrive", "/me/drive/root/children", {
  method: "GET"
});


// Download a specific file in a drive
await paragon.request("onedrive", "/me/drive/items/<item-id>/content", {
  method: "GET"
})
```

## Building OneDrive workflows

Once your OneDrive account is connected, you can add steps to perform the following actions:

* Save File
* Get File
* List Files
* Create Folder
* Get Folder by ID
* Search Folders
* Move Folder
* Delete Folder

You can also use the OneDrive Request step to access any of OneDrive API endpoints without the authentication piece.

When creating or updating records in OneDrive, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' OneDrive account. For example, you might want to trigger a workflow whenever files are changed in OneDrive to sync your users' OneDrive files to your application in real-time.

<figure><img src="../../.gitbook/assets/OneDrive Webhook Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for OneDrive below:

* **File Change**
