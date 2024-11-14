---
description: Connect to your users' Close accounts
---

# Close

## Setup Guide

You can find your Close app credentials in your [Close Developer Account.](https://developer.close.com/)

You'll need the following information to set up your Close App with Paragon Connect:

* Close API Key

## Connecting to Close

Once your users have connected their Close account, you can use the Paragon SDK to access the Close API on behalf of connected users.

See the Close [REST API documentation](https://developer.close.com/) for their full API reference.

Any Close API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a contact
paragon.request("close", "/contact", {
  method: "POST",
  body: {
    "lead_id":"lead_QyNaWw4fdSwxl5Mc5daMFf3Y27PpIcH0awPbC9l7uyo",
    "name":"John Appleseed",
    "title":"CEO",
    "phones":[
        {"phone":"9045551234","type":"mobile"}
    ],
    "emails":[
        {"email":"john@example.com","type":"office"}
    ],
    "urls":[
        {"url":"http://twitter.com/google/","type":"url"}
    ],
  }
});

// Create a lead
paragon.request("close", "[relative URL]", {
  method: "POST",
  body {
    "name": "Example Company",
    "url": "http://company.domain.com/",
    "description": "A company",
    "status_id": "stat_1ZdiZqcSIkoGVnNOyxiEY58eTGQmFNG3LPlEVQ4V7Nk",
    "contacts": [
        {
            "name": "Gob",
            "title": "Sr. Vice President",
            "emails": [
                {
                    "type": "office",
                    "email": "gob@example.com"
                }
            ],
            "phones": [
                {
                    "type": "office",
                    "phone": "8004445555"
                }
            ]
        }
    ]
  }
});

// Get all opportunities
paragon.request("close", "/opportunity", {
  method: "GET"
});
  
```

## Building Close workflows

Once your Close account is connected, you can add steps to perform the following actions:

* Create Record
* Update Record
* Get Record by ID
* Search Record
* Delete Record
* Search Records by JSON Filter

You can also use the Close Request step to access any of Close's API endpoints without the authentication piece.

When creating or updating records in Close, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Close account. For example, you might want to trigger a workflow whenever new leads are created in Close to sync your users' Close leads to your application in real-time.

<figure><img src="../../.gitbook/assets/Close Webhook Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Close below:

* **Record Created**
* **Record Updated**
* **Record Deleted**
