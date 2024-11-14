---
description: Connect to your users' OneNote accounts
---

# OneNote

## Setup Guide

You can find your OneNote application credentials by visiting your Microsoft Azure Portal.

You'll need the following information to set up your OneNote app with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Prerequisites

* A [Microsoft Azure](https://azure.microsoft.com/) account

### Add the Redirect URL to your OneNote app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your OneNote app:

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

Since OneNote does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Add your OneNote app to Paragon

1\. Select OneNote from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](onenote.md#add-the-redirect-url-to-your-onenote-app) in their respective sections:

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

<figure><img src="../../.gitbook/assets/Connecting your OneNote app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to OneNote

Once your users have connected their OneNote account, you can use the Paragon SDK to access the OneNote API on behalf of connected users.

See the OneNote [REST API documentation](https://learn.microsoft.com/en-us/graph/api/resources/onenote-api-overview?view=graph-rest-1.0\&amp;preserve-view=true) for their full API reference.

Any OneNote API endpoints can be accessed with the Paragon SDK as shown in this example:

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Retrieve a Page
await paragon.request('onenote', '/groups/<Group-ID>/onenote/pages/<Page-ID>', {
  method: 'GET'
});


// Create a Page
await paragon.request('onenote', '/me/onenote/sections/<Section-ID>/pages', {
  method: 'POST',
  body: `
    <!DOCTYPE html>
    <html>
      <head>
          <title>A page with a block of HTML</title>
      </head>
      <body>
          <p>This page contains some <i>formatted</i> <b>text</b>.</p>
      </body>
    </html>`
});
```

## Building OneNote workflows

Once your OneNote account is connected, you can add steps to perform the following actions:

* Create a Page
* Update Page
* Get Page by ID
* Delete Page
* Search Pages

You can also use the OneNote Request step to access any of OneNote API endpoints without the authentication piece.

When creating or updating records in OneNote, you can reference data from previous steps by typing `{{` to invoke the variable menu.
