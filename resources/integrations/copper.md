---
description: Connect to your users' Copper accounts
---

# Copper

## Setup Guide

You can find your Copper CRM credentials in your Copper settings.

You'll need the following information to set up your Copper account with Paragon Connect:

* Email Address of the Token Owner
* API Key

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Copper

Once your users have connected their Copper account, you can use the Paragon SDK to access the Copper API on behalf of connected users.

See the Copper [REST API documentation](https://developer.copper.com/) for their full API reference.

Any Copper API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a Person
paragon.request("copper", "/v1/people", {
  method: "POST",
  body: {
    "name":"Foo Westwood",
    "emails": [
      {
      "email":"foo@westwood.com",
      "category":"work"
      }
    ],
    "address": {
      "street": "123 Main Street",
      "city": "Savannah",
      "state": "Georgia",
      "postal_code": "31410",
      "country": "United States"
    },
    "phone_numbers": [
      {
      "number":"415-123-45678",
      "category":"mobile"
      }
    ]
  }
});

// Create a Lead
paragon.request("copper", "/v1/leads", {
  method: "POST",
  body: {
    "name":"Foo Westwood",
    "email": {
      "email":"foo@westwood.com",
      "category":"work"
    },
    "phone_numbers": [
      {
        "number":"415-123-45678",
        "category":"mobile"
      }
    ],
    "address": {
      "street": "123 Main Street",
      "city": "Savannah",
      "state": "Georgia",
      "postal_code": "31410",
      "country": "United States"
    },
    "custom_fields": [
      {
        "custom_field_definition_id": 100764,
        "value": "Text fields are 255 chars or less!"
      },
      {
        "custom_field_definition_id": 103481,
        "value": "Text area fields can have long text content"
      }
    ],
    "customer_source_id":331242
  }
});

// Search Opportunities
paragon.request("copper", "/v1/opportunities/search", {
  method: "POST",
  body: {
    "page_size": 5,
    "sort_by": "name"
  }
});
  
```

## Building Copper workflows

Once your Copper account is connected, you use the Copper Request step to access any of Copper's API endpoints without the authentication piece.

When creating or updating records in Copper, you can reference data from previous steps by typing `{{` to invoke the variable menu.
