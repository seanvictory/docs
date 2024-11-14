---
description: Connect your QuickBooks app for OAuth in Paragon.
---

# QuickBooks

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new QuickBooks app if you don't already have one.
{% endhint %}

You can find your QuickBooks app credentials by visiting your [QuickBooks developer portal](https://developer.intuit.com/app/developer/homepage).

You'll need the following information to set up your QuickBooks App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* An [Intuit Developer account](https://developer.intuit.com/app/developer/homepage).
* A QuickBooks app.

### Add the Redirect URL to your QuickBooks app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your QuickBooks app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log in to your [QuickBooks developer dashboard](https://developer.intuit.com/app/developer/dashboard) and select your application.

3\. Depending on whether your application is in **Development** **(Sandbox)** or **Production**, go to **Keys & OAuth > Redirect URIs**.

4\. Paste-in Paragon Connect's redirect URL found in Step 1.

5\. Press the blue **Save** button at the bottom of the page to save your updates.

![](<../../.gitbook/assets/Enabling OAuth for your QuickBooks app.gif>)

### Add your QuickBooks app to Paragon

Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](quickbooks.md#1-add-the-redirect-url-to-your-quickbooks-app) in their respective sections:

* **Client ID:** Found under Keys & OAuth > Keys > Client ID on your QuickBooks App page.
* **Client Secret:** Found under Keys & OAuth > Keys > Client Secret on your QuickBooks App page.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your QuickBooks app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to QuickBooks

Once your users have connected their QuickBooks account, you can use the Paragon SDK to access the QuickBooks API on behalf of connected users.

See the QuickBooks [REST API documentation](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/most-commonly-used/account) for their full API reference.

Any QuickBooks API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Create Customer
await paragon.request("quickbooks", "/customer", { 
  method: "POST",
  body: {
    "FullyQualifiedName": "King Groceries", 
    "PrimaryEmailAddr": {
      "Address": "jdrew@myemail.com"
    }, 
    "DisplayName": "King's Groceries", 
    "Suffix": "Jr", 
    "Title": "Mr", 
    "MiddleName": "B", 
    "Notes": "Here are other details.", 
    "FamilyName": "King", 
    "PrimaryPhone": {
      "FreeFormNumber": "(555) 555-5555"
    }, 
    "CompanyName": "King Groceries", 
    "BillAddr": {
      "CountrySubDivisionCode": "CA", 
      "City": "Mountain View", 
      "PostalCode": "94042", 
      "Line1": "123 Main Street", 
      "Country": "USA"
    }, 
    "GivenName": "James"
  }
});


// Query Customers
await paragon.request("quickbooks", "/query?query=select * from Customer", { 
  method: "GET"
});

```

## Building QuickBooks workflows

Once your QuickBooks account is connected, you can add steps to perform the following actions:

* Get accounts
* Get bills
* Create bill
* Get customer
* Create customer
* Update customer
* Get invoices
* Create invoices
* Send invoices
* Get payments
* Create payments

When creating or updating records in QuickBooks, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Using Quickbooks in Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' QuickBooks account. For example, you might want to trigger a workflow whenever new invoices are created QuickBooks to sync your users' QuickBooks invoices to your application in real-time.

![](<../../.gitbook/assets/QuickBooks webhook triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for QuickBooks below:

* **New Account**
* **New Customer**
* **New Invoice**
