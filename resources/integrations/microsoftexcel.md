---
description: Connect to your users' Microsoft Excel accounts
---

# Microsoft Excel

## Setup Guide

You can find your Microsoft Excel application credentials by visiting your Microsoft Azure Portal.

You'll need the following information to set up your Microsoft Excel app with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* A [Microsoft Azure](https://azure.microsoft.com/) account

### Add the Redirect URL to your Microsoft Excel app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Microsoft Excel app:

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

Since Microsoft Excel does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Add your Microsoft Excel app to Paragon

1\. Select **Microsoft Excel** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](microsoftexcel.md#add-the-redirect-url-to-your-microsoft-excel-app) in their respective sections:

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

![](<../../.gitbook/assets/Connecting a Microsoft Outlook application to Paragon Connect.png>)

## Connecting to Microsoft Excel

Once your users have connected their Microsoft Excel account, you can use the Paragon SDK to access the Microsoft Excel API on behalf of connected users.

See the Microsoft Excel [REST API documentation](https://learn.microsoft.com/en-us/graph/api/resources/excel?view=graph-rest-1.0\&preserve-view=true) for their full API reference.

Any Microsoft ExcelExcel API endpoints can be accessed with the Paragon SDK as shown in this example:

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get Spreadsheet
await paragon.request('excel', '<workbook id>/workbook/worksheets/<worksheet name>', {
    method: 'GET'
});

// Query Spreadsheet data
await paragon.request('excel', '[relative URL]', {
    method: 'GET'
});
```

## Building Microsoft Excel workflows

Once your Microsoft Excel account is connected, you use the Microsoft Excel Request step to access any of Microsoft Excel's API endpoints without the authentication piece.

When creating or updating records in Microsoft Excel, you can reference data from previous steps by typing `{{` to invoke the variable menu.
