---
description: Connect to your users' Dynamics accounts
---

# Dynamics 365 Business Central

## Setup Guide

You can find your Dynamics 365 Business Central app credentials in your [Dynamics 365 Business Central Developer Account.](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/)

You'll need the following information to set up your Dynamics 365 Business Central App with Paragon Connect:

* Consumer Key
* Consumer Secret
* Scopes Requested

### Add the Redirect URL to your Dynamics 365 Finance app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Dynamics 365 Business Central app:

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

Since Dynamics 365 Business Central does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

### Add your Dynamics 365 Business Central app to Paragon

1\. Select **Dynamics 365 Business Central** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](dynamicsbusinesscentral.md#add-the-redirect-url-to-your-dynamics-365-finance-app) in their respective sections:

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

![](<../../.gitbook/assets/Connecting your Dynamics 365 Business Central app to Paragon Connect.png>)

## Connecting to Dynamics 365 Business Central

Once your users have connected their Dynamics 365 Business Central account, you can use the Paragon SDK to access the Dynamics 365 Business Central API on behalf of connected users.

See the Dynamics 365 Business Central [REST API documentation](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/) for their full API reference.

Any Dynamics 365 Business Central API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create purchase invoice
paragon.request("dynamicsbusinesscentral", "/purchaseInvoices", {
  method: "POST",
  body: {
    number: "108001",
    invoiceDate: "2019-01-01",
    dueDate: "2019-01-01",
    currencyCode: "USD",
    pricesIncludeTax: false,
    totalAmountExcludingTax: 3122.8,
    totalTaxAmount: 187.37,
    totalAmountIncludingTax: 3310.17,
    status: "Paid",
  }
});

// Get the balance sheet
paragon.request("dynamicsbusinesscentral", "/balanceSheet?$orderby=lineNumber&$filter=dateFilter eq 2020-12-30", {
  method: "GET"
});

//Update a vendor by ID
paragon.request("dynamicsbusinesscentral", "/vendors([Vendor ID])", {
  method: "PATCH",
  body: {
    displayName: "Wide World Importers Inc.",
    blocked: "Payment"
  }
});
  
```

## Building Dynamics 365 Business Central workflows

When creating or updating records in Dynamics 365 Business Central, you can reference data from previous steps by typing `{{` to invoke the variable menu.

* Create Vendor
* Update Vendor
* Get Vendor by ID
* Search for Vendor
* Delete Vendor
* Create Purchase Invoice
* Update Purchase Invoice
* Post a Purchase Invoice
* Get a Purchase Invoice by ID
* Search for Purchase Invoice
* Delete Purchase Invoice
* Create Purchase Invoice Line Item
* Update Purchase Invoice Line Item
* Get Purchase Invoice Lines
* Get Purchase Invoice Line Item by ID
* Search for Purchase Invoice Line Item
* Delete Purchase Invoice Line Item
* Get Accounts
* Get Account by ID
* Create Tax Group
* Update Tax Group
* Get Tax Group by ID
* Search for Tax Group
* Delete Tax Group
* Create Payment Term
* Update Payment Term
* Get Payment Term by ID
* Search for Payment Term
* Delete Payment Term

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Dynamics 365 Business Central account. For example, you might want to trigger a workflow whenever new records are created in Dynamics 365 Business Central to sync your users' Dynamics 365 Business Central records to your application in real-time.

You can find the full list of Webhook Triggers for Dynamics 365 Business Central below:

* **Record Created**
* **Record Updated**
* **Record Deleted**
