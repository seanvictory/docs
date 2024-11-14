---
description: Connect to your users' Sage Intacct accounts
---

# Sage Intacct

## Setup Guide

You can find your Sage Intacct app credentials in your [Sage Intacct Developer Account.](https://developer.intacct.com/api/)

You'll need the following information to set up your Sage Intacct App with Paragon Connect:

* Sender ID
* Sender Password

### Add your Sage Intacct app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Sender ID:** Your Sage Intacct User ID
* **Sender Password:** Your Sage Intacct User Password

{% hint style="info" %}
Leaving the Sender ID and Sender Password blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Sage Intacct application to Paragon Connect.png>)

## Connecting to Sage Intacct

Once your users have connected their Sage Intacct account, you can use the Paragon SDK to access the Sage Intacct API on behalf of connected users.

See the Sage Intacct [REST API documentation](https://developer.intacct.com/api/) for their full API reference.

Any Sage Intacct API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Query IDs of vendors owed
paragon.request("sageintacct", "/", {
  method: "POST",
  body: `
    <query>
      <object>VENDOR</object>
      <select>
        <field>RECORDNO</field>
      </select>
      <filter>
        <greaterthan>
          <field>TOTALDUE</field>
          <value>0</value>
        </greaterthan>
      </filter>
  </query>
  `
})

// Get a single bill by a record number
paragon.request("sageintacct", "/", {
  method: "POST",
  body: `
    <read>
      <object>APBILL</object>
      <keys>[Bill RECORDNO]</keys>
      <fields>*</fields>
    </read>
  `
});

// Update the header of a bill
paragon.request("sageintacct", "/", {
  method: "POST",
  body: `
    <update>
      <APBILL>
        <RECORDNO>[Bill RECORDNO]</RECORDNO>
        <DESCRIPTION>Changing the description</DESCRIPTION>
      </APBILL>
    </update>
  `
});
  
```

## Building Sage Intacct workflows

Once your Sage Intacct account is connected, you can add steps to perform the following actions:

* Create Vendor
* Update Vendor
* Delete Vendor
* Search Vendors
* Get Vendor by ID
* Search Vendor Types
* Create Bill
* Update Bill
* Delete Bill
* Search Bills
* Get Bill by ID
* Search Payment Terms
* Get Payment Term by ID
* Search Accounts
* Get Account by ID
* Get Dimensions

When creating or updating records in Sage Intacct, you can reference data from previous steps by typing `{{` to invoke the variable menu.
