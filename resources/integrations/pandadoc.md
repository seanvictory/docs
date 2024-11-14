---
description: Connect to your users' PandaDoc accounts
---

# PandaDoc

## Setup Guide

You can find your PandaDoc app credentials in your [PandaDoc Developer Account.](https://api.pandadoc.com/public/v1)

You'll need the following information to set up your PandaDoc App with Paragon Connect:

* PandaDoc API Key

## Connecting to PandaDoc

Once your users have connected their PandaDoc account, you can use the Paragon SDK to access the PandaDoc API on behalf of connected users.

See the PandaDoc [REST API documentation](https://api.pandadoc.com/public/v1) for their full API reference.

Any PandaDoc API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Send a document
paragon.request("pandadoc", "/documents/<ID>/send", {
  method: "POST",
  body: {
     "message": "Hello! This document was sent from the PandaDoc API.",
     "subject": "Please check this test API document from PandaDoc",
     "silent": false,
     "sender": {
          "membership_id": "gEy74Zx4VjNfV3Q2rHdgZW"
     }
  }
});

// List documents
paragon.request("pandadoc", "/documents?", {
  method: "GET"
});

// Create a contact
paragon.request("pandadoc", "/contacts", {
  method: "POST",
  body: {
     "email": "john@appleseed.com",
     "first_name": "John",
     "last_name": "Appleseed",
     "company": "Apples & Company",
  }
});
  
```

## Building PandaDoc workflows

Once your PandaDoc account is connected, you can add steps to perform the following actions:

* Create a Document
* Update a Document
* Get a Document by ID
* Delete Document
* Send a Document
* Search Documents

You can also use the PandaDoc Request step to access any of PandaDoc API endpoints without the authentication piece.

When creating or updating records in DocuSign, you can reference data from previous steps by typing `{{` to invoke the variable menu.
