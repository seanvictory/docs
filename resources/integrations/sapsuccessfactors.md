---
description: Connect to your users' SAP SuccessFactors accounts
---

# SAP SuccessFactors

## Setup Guide

You'll need the following information to set up your SAP SuccessFactors App with Paragon Connect:

* SAP SuccessFactor API Server
* Username
* Password

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to SAP SuccessFactors

Once your users have connected their SAP SuccessFactors account, you can use the Paragon SDK to access the SAP SuccessFactors API on behalf of connected users.

See the SAP SuccessFactors [REST API documentation](https://api.sap.com/package/SuccessFactorsEmployeeCentral/all) for their full API reference.

Any SAP SuccessFactors API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Company Directory
paragon.request("sapsucessfactors", "/", {
  method: "GET"
});

// Create a time-off request
paragon.request("sapsucessfactors", "/WorkScheduleDay", {
  method: "POST"
});

// Get benefit deduction types
paragon.request("sapsucessfactors", "/BenefitDeductionDetails?$top=10", {
  method: "GET"
});
  
```

## Building SAP SuccessFactors workflows

Once your SAP SuccessFactors account is connected, you use the SAP SuccessFactors Request step to access any of SAP SuccessFactors's API endpoints without the authentication piece.

When creating or updating records in SAP SuccessFactors, you can reference data from previous steps by typing `{{` to invoke the variable menu.
