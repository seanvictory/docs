---
description: Connect to your users' SharePoint accounts
---

# SharePoint

## Setup Guide

You can find your SharePoint application credentials by visiting your Microsoft Azure Portal.

You'll need the following information to set up your SharePoint app with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* A [Microsoft Azure](https://azure.microsoft.com/) account

### Add the Redirect URL to your SharePoint app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your SharePoint app:

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

Since SharePoint does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Enable Multi-tenancy to your SharePoint app

To allow Microsoft users from outside of your organization to connect to your SharePoint application, you must specify this as an option within the SharePoint application registration.

1. &#x20;Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/) using your Microsoft account.
2. Navigate to **All Services > App Registrations** and select your application.
3. Select **Authentication** from the sidebar.
4. Under **Supported account types**, press the  **"Accounts in any organizational directory"** option.
5. Click Save.

### Add your SharePoint app to Paragon

1\. Select **SharePoint** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](sharepoint.md#add-the-redirect-url-to-your-sharepoint-app) and [Step 2](sharepoint.md#generate-a-client-secret) in their respective sections:

* **Client ID:** Found under Essentials > Application (client) ID on your Microsoft Azure Portal app page.
* **Client Secret:** Found at the end of [Step 2](sharepoint.md#generate-a-client-secret).
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** You should only add the scopes you've requested in your application page to Paragon.
{% endhint %}

![](<../../.gitbook/assets/Connecting Sharepoint to Paragon Connect.png>)

## Connecting to SharePoint

Once your users have connected their SharePoint account, you can use the Paragon SDK to access the SharePoint API on behalf of connected users.

See the SharePoint [REST API documentation](https://docs.microsoft.com/en-us/graph/api/resources/sharepoint?view=graph-rest-1.0) for their full API reference.

Any SharePoint API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get organization’s default site
await paragon.request("sharepoint", "/sites/root", { 
  method: "GET",
});


// Get list under a site
await paragon.request("sharepoint", "/sites/{site-id}/lists", { 
  method: "GET",
});

// Create task in list
await paragon.request("sharepoint", "sites/{site-id}/lists/{list-id}/items", { 
  method: "POST",
  body: {
    "fields": {
      "Title": "Widget",
      "Color": "Purple",
      "Weight": 32
    }
}
});
```

## Building SharePoint workflows

Once your SharePoint account is connected, you can add steps to perform the following actions:

* Create Item
* Update Item
* Get Item by ID
* Get Items in a List
* Delete Item
* Create List
* Get List by ID
* Get Lists
* Create List column
* Get List columns
* Get default site
* Search sites
* Get subsites in a site

When creating messages in SharePoint, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Sharepoint account. For example, you might want to trigger a workflow whenever new items are created in Sharepoint to sync your users' Sharepoint items to your application in real-time.

<figure><img src="../../.gitbook/assets/Sharepoint Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Sharepoint below:

* **Item Created**
* **Item Updated**
* **Page Modified**
* **File Deleted**
