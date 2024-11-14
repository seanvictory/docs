---
description: Connect to your users' Sage Accounting systems
---

# Sage Accounting

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new ClickUp app if you don't already have one.
{% endhint %}

You can find your Sage Accounting app credentials in your [Sage Accounting Developer Account.](https://developer.sage.com/api/accounting/api/)

You'll need the following information to set up your Sage Accounting App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add the Redirect URL to your Sage Accounting app

Paragon provides a redirect URL to send information to your Sage Accounting app. To add the redirect URL to your Sage Accounting app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log into your [Sage Accounting Developer Portal](https://developer.sage.com/api/accounting/api/).

3\. Navigate to **My Account > Applications** and select your application.

4\. Under **App Details**, click the edit button.&#x20;

5\. Under **Callback URLs**, paste the Redirect URL provided in Step 1.

ServiceNow provides you with the **Client ID** and **Client Secret** needed for the next steps after adding the redirect URL to your project.

### Add your Sage Accounting app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID** Found under App Credentials > Client ID on your Sage Accounting App page.
* **Client Secret:** Found under App Credentials > Client Secret on your Sage Accounting App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Sage Accounting app to Paragon Connect.png>)

## Connecting to Sage Accounting

Once your users have connected their Sage Accounting account, you can use the Paragon SDK to access the Sage Accounting API on behalf of connected users.

See the Sage Accounting [REST API documentation](https://developer.sage.com/api/accounting/api/) for their full API reference.

Any Sage Accounting API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Search for a contact by an email address
paragon.request("sageaccounting", "/contacts?email=<Email>", {
  method: "GET"
});

// Create an invoice
paragon.request("sageaccounting", "/sales_invoices", {
  method: "POST",
  body: {
    contact_id: "<Contact ID>",
    date: "2022-01-31",
    invoice_lines: [{
      description: "Item 1",
      ledger_account_id: "<Ledger Account ID>",
      unit_price: "25.99"
    }]
  }
});

// Create a payment for an invoice
paragon.request("sageaccounting", "/contact_payments", {
  method: "POST",
  body: {
    contact_payment: {
      transaction_type_id: "CUSTOMER_RECEIPT",
      payment_method_id: "CREDIT_DEBIT",
      contact_id: "<Contact ID>",
      bank_account_id: "<Bank Account ID>",
      date: "2022-02-01",
      total_amount: "25.99",
      allocated_artefacts: [{
        artefact_id: "<Invoice ID>",
        amount: "25.99"
      }]
    }
  }
});
  
```

## Building Sage Accounting workflows

Once your Sage Accounting account is connected, you use the Sage Accounting Request step to access any of Sage Accounting's API endpoints without the authentication piece.

When creating or updating records in Sage Accounting, you can reference data from previous steps by typing `{{` to invoke the variable menu.
