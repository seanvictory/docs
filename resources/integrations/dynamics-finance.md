---
description: Connect to your users' Dynamics 365 Finance account
---

# Dynamics 365 Finance

## Setup Guide

You can find your Dynamics 365 Finance app credentials in your [Dynamics 365 Finance Developer Account.](https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/data-entities/odata)

You'll need the following information to set up your Dynamics 365 Finance App with Paragon Connect:

* Client Key
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Dynamics 365 Finance app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Dynamics 365 Finance app:

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

Since Dynamics 365 Finance does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

### Add your Dynamics 365 Finance app to Paragon

1\. Select **Dynamics 365 Finance** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](dynamics-finance.md#add-the-redirect-url-to-your-dynamics-365-finance-app) in their respective sections:

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
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Dynamics 365 Finance app to Paragon Connect.png>)

## Connecting to Dynamics 365 Finance

Once your users have connected their Dynamics 365 Finance account, you can use the Paragon SDK to access the Dynamics 365 Finance API on behalf of connected users.

See the Dynamics 365 Finance [REST API documentation](https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/data-entities/odata) for their full API reference.

Any Dynamics 365 Finance API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get a list of customers
paragon.request("dynamicsfinance", "/Customers", {
  method: "GET"
});

// Get a list of vendors
paragon.request("dynamicsfinance", "/Vendors", {
  method: "GET"
});

// Get a list of "Inventory profiles"
paragon.request("dynamicsfinance", "/InventoryProfiles", {
  method: "GET"
});  
  
```

## Building Dynamics 365 Finance workflows

When creating or updating records in Dynamics 365 Finance, you can reference data from previous steps by typing `{{` to invoke the variable menu.

* Get Accounts
* Create Vendor
* Update Vendor
* Get Vendor by ID
* Search for Vendor
* Create Bill
* Update Bill
* Get Bill by ID
* Search for Bill
* Delete Bill
* Create Bill Line Item
* Update Bill Line Item
* Get Bill Line Item by ID
* Search for Bill Line Item
* Delete Bill Line Item
* Create Customer
* Update Customer
* Get Customer by ID
* Search for Customer
* Delete Customer
* Create Invoice
* Update Invoice
* Get Invoice by ID
* Search for Invoice
* Delete Invoice
* Create Payment Journal
* Update Payment Journal
* Get Payment Journal by ID
* Search for Payment Journal
* Delete Payment Journal
* Create Payment Journal Line Item
* Update Payment Journal Line Item
* Get Payment Journal Line Item by ID
* Search for Payment Journal Line Item
* Delete Payment Journal Line Item
