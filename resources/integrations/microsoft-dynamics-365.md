# Microsoft Dynamics 365

## Setup Guide

You can find your Microsoft Dynamics 365 application credentials by visiting your Microsoft Azure Portal.

You'll need the following information to set up your Microsoft Dynamics 365 app with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* A [Microsoft Azure](https://azure.microsoft.com/) account

### Add the Redirect URL to your Microsoft Dynamics 365 app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Microsoft Dynamics 365 app:

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

Since Microsoft Dynamics 365 does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Add your Microsoft Dynamics app to Paragon

1\. Select **Microsoft Dynamics** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](microsoft-teams.md#add-the-redirect-url-to-your-microsoft-teams-app)in their respective sections:

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

## Connecting to Microsoft Dynamics 365

Once your users have connected their Microsoft Dynamics 365 account, you can use the Paragon SDK to access the Microsoft Dynamics 365 API on behalf of connected users.

See the Microsoft Dynamics 365 [REST API documentation](https://docs.microsoft.com/en-us/dynamics365/sales-enterprise/help-hub) for their full API reference.

Any Microsoft Dynamics 365 API endpoints can be accessed with the Paragon SDK as shown in this example:

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Create an Account
await paragon.request("microsoftDynamics", "/accounts", {
  method: "POST",
  body: { "name": "Sample Account" }
});


// Query Accounts by number of employees
await paragon.request("microsoftDynamics", "/accounts?$filter=Microsoft.Dynamics.CRM.Between(PropertyName='numberofemployees',PropertyValues=["5","2000"])”
    method: "GET"
});
```

## Building Microsoft Dynamics 365 workflows

Once your Microsoft Dynamics 365 account is connected, you can add steps to perform the following actions:

* Create Record
* Update Record
* Get Record by ID
* Search Records
* Delete Record by ID

When creating or updating records in Microsoft Dynamics 365, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Using Microsoft Dynamics 365 in Paragon.png>)
