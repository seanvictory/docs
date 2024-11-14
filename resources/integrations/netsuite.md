---
description: Connect to your users' NetSuite ERP systems
---

# NetSuite

## Setup Guide

### **Select an authentication strategy for your users**

Selecting an authentication strategy is the first step to building a NetSuite integration on Paragon. Paragon supports two methods for authenticating against your users' NetSuite systems, **Authorization Code grant** and **Client Credentials**. Your selection will affect the user experience of your connected users.

*   **Authorization Code –** Paragon will use the **Client ID** and **Client Secret** from the NetSuite app you create to initiate OAuth 2.0 flow on behalf of your connecting users.

    <figure><img src="../../.gitbook/assets/CleanShot 2024-08-02 at 12.16.14.png" alt="" width="563"><figcaption></figcaption></figure>
* **Client Credentials –** your connecting users are required to create their own client apps within their NetSuite instances.

<figure><img src="../../.gitbook/assets/CleanShot 2024-08-02 at 12.17.57 (1).png" alt="" width="563"><figcaption></figcaption></figure>

We recommend developers use the **Authorization Code** method to optimize for a more seamless user experience for your connecting users.&#x20;

### **Enabling the OAuth 2.0 feature in your NetSuite test instance**

Enabling the OAuth 2.0 and SuiteScript features in NetSuite are the first steps for configuring your NetSuite sandbox instance to Paragon Connect.

1. Navigate to **Setup > Company > Enable Features** then select the **SuiteCloud** tab.
2. Check the boxes for enabling **Client SuiteScript**, **Server SuiteScript**, and **OAuth 2.0**.
3. Click **Save.**&#x20;

### **Creating a NetSuite OAuth application**

Now you can create your NetSuite app credentials in your NetSuite instance's Integration Management Settings. This is found under **Setup > Integration > Manage Integrations > New**.

1. Add a **Name**, a **Description**, and click to change the **State** dropdown to _**Enabled**_.
2. Enable the _**Token-Based Authentication**_ checkbox, _**Authorization Code Grant**,_ and _**Public Client**_ options under **Authorization**.
3. Add the Paragon _**Redirect URL**_

```
https://passport.useparagon.com/oauth
```

4. Select the three scopes: `RESTLETS`, `REST WEB SERVICES`, and `SUITEANALYTICS`.

You'll need the following information from the NetSuite application registration to set up your NetSuite App with Paragon Connect:

* Consumer Key
* Consumer Secret
* Scopes Requested

### Add your NetSuite app to Paragon

In the Paragon Dashboard under **Integrations > Connected Integrations >** **NetSuite** **>** **Settings**, fill out your credentials from your NetSuite app in their respective sections:

* **Client ID:** Found under Setup > Integration > Manage Integrations on your NetSuite App page.
* **Client Secret:** Found under Setup > Integration > Manage Integrations on your NetSuite App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your NetSuite application to Paragon Connect.png>)

## Connecting to NetSuite

Once your users have connected their NetSuite account, you can use the Paragon SDK to access the NetSuite API on behalf of connected users.

See the NetSuite [REST API documentation](https://system.netsuite.com/help/helpcenter/en\_US/APIs/REST\_API\_Browser/record/v1/2021.2/index.html) for their full API reference.

Any NetSuite API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get a list of purchase orders filtered by a search
paragon.request("netsuite", "/purchaseOrder?q=[Query]", {
  method: "GET"
});

// Get a list of vendors
paragon.request("netsuite", "/vendor", {
  method: "GET"
});
  
```

## Building NetSuite workflows

Once your NetSuite account is connected, you can add steps to perform the following actions:

* Create Vendor
* Update Vendor
* Get Vendor by ID
* Search Vendors
* Delete Vendor
* Create Bill
* Update Bill
* Get Bill by ID
* Search Bills
* Delete Bill
* Create Account
* Update Account
* Get Account by ID
* Search Accounts
* Delete Account
* Create Tax Group
* Update Tax Group
* Get Tax Group by ID
* Delete Tax Group
* Search Payment Terms
* Get Payment Term by ID
* Search Posting Periods

When using NetSuite, you can reference data from previous steps by typing `{{` to invoke the variable menu.
