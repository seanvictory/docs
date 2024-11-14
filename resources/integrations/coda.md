---
description: Connect to your users' Coda accounts
---

# Coda

## Setup Guide

You can find your Coda API Token in your [Coda account settings](https://coda.io/account).

You'll need the following information to set up your Coda account with Paragon Connect:

* Coda API Token

## Connecting to Coda

Once your users have connected their Coda account, you can use the Paragon SDK to access the Coda API on behalf of connected users.

See the Coda [REST API documentation](https://coda.io/developers/apis/v1) for their full API reference.

Any Coda API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a Document
paragon.request("coda", "/docs", {
  method: "POST",
  body: {
    "title": "Project Tracker",
    "sourceDoc": "iJKlm_noPq",
    "timezone": "America/Los_Angeles",
    "folderId": "fl-ABcdEFgHJi"
  }
});

// Get Documents
paragon.request("coda", "/docs", {
  method: "GET"
});
  
```

## Building Coda workflows

Once your Coda account is connected, you can add steps to perform the following actions:

* Create Document
* Search Documents
* Get Document by ID
* Delete Document
* Search Tables
* Get Table by ID

You can also use the Coda Request step to access any of Coda's API endpoints without the authentication piece.

When creating or updating records in Coda, you can reference data from previous steps by typing `{{` to invoke the variable menu.
