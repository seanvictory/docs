---
description: Connect your Oracle Financials Cloud for OAuth in Paragon.
---

# Oracle Financials Cloud

## Setup Guide

You'll need the following information to set up your Oracle Financials Cloud App with Paragon Connect:

* App Name
* Scopes Requested

### Add your Oracle Financials Cloud app to Paragon

1\. Select Oracle Financials Cloud from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials in their respective sections:

* **App Name:**
  * Specify an app name to appear on Oracle Financials Cloud
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the App Name blank will use Paragon development keys.
{% endhint %}

## Connecting to Oracle Financials Cloud

Once your users have connected their Oracle Financials Cloud account, you can use the Paragon SDK to access the Oracle Financials Cloud API on behalf of connected users.

See the Oracle Financials Cloud [REST API documentation](https://docs.oracle.com/en/cloud/saas/financials/21d/farfa/) for their full API reference.

Any Oracle Financials Cloud API endpoints can be accessed with the Paragon SDK as shown in this example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration.

// Authenticate the user
paragon.authenticate(<ProjectID>, <Paragon User Token>);

// Get an Invoice
await paragon.request("oraclefinancialscloud", "/invoices/<Invoice ID>", {
  method: “GET”,
});

// Calculate Tax for an Invoice
await paragon.request("oraclefinancialscloud", "/invoices", {
  method: “POST”,
  body: {
    name: “calculateTax”,
    parameters: [“<Invoice ID>”, “<Business Unit>”, “<Supplier>”]
  }
});

```
{% endtab %}
{% endtabs %}

## Building Oracle Financials Cloud workflows

Once your Oracle Financials Cloud account is connected, you can add steps to perform the following actions:

* Search Invoices
* Create Invoice
* Update Invoice
* Build Invoice Line Item
* Validate Invoice

When using Oracle Financials Cloud, you can reference data from previous steps by typing `{{` to invoke the variable menu.
