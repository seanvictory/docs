---
description: Connect to your users' Freshdesk accounts.
---

# Freshdesk

## Setup Guide

You can find your Freshdesk credentials in your [Freshdesk account.](https://developers.freshdesk.com/api/)

You'll need the following information to set up your Freshdesk account with Paragon Connect:

* Freshdesk Domain
* API Key

## Connecting to Freshdesk

Once your users have connected their Freshdesk account, you can use the Paragon SDK to access the Freshdesk API on behalf of connected users.

See the Freshdesk [REST API documentation](https://developers.freshdesk.com/api/) for their full API reference.

Any Freshdesk API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get all tickets
paragon.request("freshdesk", "/tickets", {
  method: "GET"
});

// Create a ticket
paragon.request("freshdesk", "/tickets", {
  method: "POST",
  body: { 
     description: "Details about the issue...",
     subject: "Support Needed...",
     email: "tom@outerspace.com",
     priority: 1,
     status: 2,
     cc_emails: ["ram@freshdesk.com","diana@freshdesk.com"]
    }
});

// Get all contacts
paragon.request("freshdesk", "/contacts", {
  method: "GET"
});
  
```

## Building Freshdesk workflows

Once your Freshdesk account is connected, you can add steps to perform the following actions:

* Create Ticket
* Update Ticket
* Get Ticket by ID
* Delete Ticket

Additionally, you can also use the Freshdesk Request step to access any of Freshdesk's API endpoints without the authentication piece.

When creating or updating records in Freshdesk, you can reference data from previous steps by typing `{{` to invoke the variable menu.
