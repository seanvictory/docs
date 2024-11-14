---
description: Connect to your users' BambooHR accounts
---

# BambooHR

## Setup Guide

You can find your BambooHR app credentials in the[ BambooHR Partner Program dashboard.](https://partners.bamboohr.com/apps-marketplace-program/)

You'll need the following information to set up your BambooHR App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your BambooHR app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found in your BambooHR Partner Program dashboard.
* **Client Secret:** Found in your BambooHR Partner Program dashboard.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your BambooHR application to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to BambooHR

Once your users have connected their BambooHR account, you can use the Paragon SDK to access the BambooHR API on behalf of connected users.

See the BambooHR [REST API documentation](https://documentation.bamboohr.com/reference/) for their full API reference.

Any BambooHR API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Company Directory
paragon.request("bamboohr", "/employees/directory", {
  method: "GET"
});

// Create a time-off request
paragon.request("bamboohr", "/employees/<EMPLOYEE ID>/time_off/request", {
  method: "POST",
  body: {
    "status": "approved",
    "start": "2022-07-01",
    "end": "2022-07-04",
    "timeOffTypeId": 86,
    "amount": 16,
    "notes": [{from: "manager", note: "Get well soon!"}],
    "previousRequest": 0
  }
});

// Get benefit deduction types
paragon.request("bamboohr", "/benefits/settings/deduction_types/all", {
  method: "GET"
});
  
```

## Building BambooHR workflows

Once your BambooHR account is connected, you can add steps to perform the following actions:

* Create Employee
* Update Employee
* Get Employee by ID
* Get Employee Directory
* Create a Time Off Request
* Change a Request Status
* Adjust Time Off Balance for an Employee
* Get Time Off Requests for an Employee
* Get Time Off Types
* Get Field List
* Add List Field Values

When creating or updating records in BambooHR, you can reference data from previous steps by typing `{{` to invoke the variable menu.
