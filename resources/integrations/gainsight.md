---
description: Connect to your users' Gainsight accounts.
---

# Gainsight

## Setup Guide

You can find your Gainsight API credentials in your [Gainsight account](https://support.gainsight.com/Gainsight\_NXT/Connectors/Connectors/API\_Integrations/Generate\_API\_Access\_Key).

You'll need the following information to set up your Gainsight account with Paragon Connect:

* Access Key
* Instance URL

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Gainsight

Once your users have connected their Gainsight account, you can use the Paragon SDK to access the Gainsight API on behalf of connected users.

See the Gainsight [REST API documentation](https://support.gainsight.com/Gainsight\_NXT/API\_and\_Developer\_Docs) for their full API reference.

Any Gainsight API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Playbooks
await paragon.request("gainsight", "/v2/cockpit/task/list", {
  method: "POST",
  body: {
    "select": [
        "Name"
    ]
 }
});

// Create CTAs from Cockpit
await paragon.request("gainsight", "/v2/cockpit/cta", {
  method: "POST",
  body: {
    "requests": [
      {
        "record": {
          "CompanyId": "1P02E3XFM9XIZFHS8U1E2JVX0AHMII6OIR1J",
          "OwnerId": "1P01KW4KG3SOEBEZMX7RSBJ0GI6BXXZ7NEX6",
          "referenceId": "1",
          "Name": "Potential Cancelation",
          "type": "Risk",
          "status": "New",
          "priority": "High",
          "reason": "Bugs Risk",
          "Comments": "test"
        }
      }
    ]
  }
});
  
```

## Building Gainsight workflows

Once your Gainsight account is connected, you use the Gainsight Request step to access any of Gainsight's API endpoints without the authentication piece.

When creating or updating records in Gainsight, you can reference data from previous steps by typing `{{` to invoke the variable menu.
