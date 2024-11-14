---
description: Connect to your users’ Azure DevOps accounts.
---

# Azure DevOps

## Setup Guide

You can find your Azure DevOps application credentials by visiting your Microsoft Azure Portal.

You'll need the following information to set up your Azure DevOps App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Azure DevOps app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Azure DevOps app:

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

Since Azure DevOps does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Add your Azure DevOps app to Paragon

Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1 ](azure-devops.md#add-the-redirect-url-to-your-azure-devops-app)in their respective sections:

* **Client ID:** Found under **Essentials > Application (client) ID** on your Microsoft Azure Portal app page.
* **Client Secret:**
  1. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/).
  2. Navigate to **Manage > Certificates & secrets** in the sidebar.
  3. Under **Client Secrets**, press the **+ New client secret** button.&#x20;
  4. Name your client credentials and select an expiry that works best for your application.
  5. Press **Add** to create your credentials.
  6. Copy the displayed Client Secret under the **Value** column.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Azure DevOps app to Paragon Connect.png>)

## Connecting to Azure DevOps

Once your users have connected their Azure DevOps account, you can use the Paragon SDK to access the Azure DevOps API on behalf of connected users.

See the Azure DevOps [REST API documentation](https://docs.microsoft.com/en-us/rest/api/azure/devops) for their full API reference.

Any Azure DevOps API endpoints can be accessed with the Paragon SDK as shown in this examples

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
          
// Get Project List
await paragon.request("azuredevops", "/projects?api-version=5.0", {
  method: “GET”,
});
```

## Building Azure DevOps workflows

Once your Azure DevOps account is connected, you can add steps to perform the following actions:

* Search Work Items
* Create Work Item
* Update Work Item
* Delete Work Item

When creating or updating work items in Azure DevOps, you can reference data from previous steps by typing `{{` to invoke the variable menu.
