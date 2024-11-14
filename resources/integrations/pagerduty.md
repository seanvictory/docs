---
description: Connect to your users' PagerDuty accounts.
---

# PagerDuty

## Setup Guide

You can find your PagerDuty app credentials in your [PagerDuty Developer Account.](https://developer.pagerduty.com/api-reference/)

You'll need the following information to set up your PagerDuty App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your PagerDuty app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your PagerDuty App page.
* **Client Secret:** Found under Client Secret on your PagerDuty App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your PagerDuty app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to PagerDuty

Once your users have connected their PagerDuty account, you can use the Paragon SDK to access the PagerDuty API on behalf of connected users.

See the PagerDuty [REST API documentation](https://developer.pagerduty.com/api-reference/) for their full API reference.

Any PagerDuty API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Incidents
paragon.request("pagerduty", "/incidents", {
  method: "GET"
});

// Create an Incident
paragon.request("pagerduty", "[relative URL]", {
  method: "POST",
  body: {
    "incident": {
      "type": "incident",
      "title": "The server is on fire.",
      "service": {
        "id": "PWIXJZS",
        "type": "service_reference"
      },
      "priority": {
        "id": "P53ZZH5",
        "type": "priority_reference"
      },
      "urgency": "high",
      "body": {
        "type": "incident_body",
        "details": "A disk is getting full on this machine. You should investigate what is causing the disk to fill, and ensure that there is an automated process in place for ensuring data is rotated (eg. logs should have logrotate around them). If data is expected to stay on this disk forever, you should start planning to scale up to a larger disk."
      },
    }
  }
});

// Get Users
paragon.request("pagerduty", "users", {
  method: "GET"
});
  
```

## Building PagerDuty workflows

Once your PagerDuty account is connected, you use the PagerDuty Request step to access any of PagerDuty's API endpoints without the authentication piece.

When creating or updating records in PagerDuty, you can reference data from previous steps by typing `{{` to invoke the variable menu.
