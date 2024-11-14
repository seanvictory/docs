---
description: Connect to your users' Shortcut accounts.
---

# Shortcut

## Setup Guide

You can find your Shortcut app credentials in your [Shortcut Developer Account.](https://developer.shortcut.com/)

You'll need the following information to set up your Shortcut App with Paragon Connect:

* Shortcut API Token

## Connecting to Shortcut

Once your users have connected their Shortcut account, you can use the Paragon SDK to access the Shortcut API on behalf of connected users.

See the Shortcut [REST API documentation](https://developer.shortcut.com/) for their full API reference.

Any Shortcut API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create an Epic
await paragon.request("shortcut", "api/v3/epics", {
   method: "POST",
   body: { 
     "name": "My Work Epic",
     "description": "This is a sample Epic"
   }
});

// Get an Epic by ID
await paragon.request("shortcut", "api/v3/epics/<epic-public-id>", {
   method: "GET"
});
  
```

## Building Shortcut workflows

Once your Shortcut account is connected, you can add steps to perform the following actions:

* Create Story
* Update Story
* Get Story by ID
* Get Stories by Project
* Get Stories by Epic
* Search Stories
* Delete Story
* Create Epic
* Update Epic
* Get Epic by ID
* Delete Epic
* Create Project
* Update Project
* Get Project by ID
* Delete Project

You can also use the Shortcut Request step to access any of Shortcut's API endpoints without the authentication piece.

When creating or updating records in Shortcut, you can reference data from previous steps by typing `{{` to invoke the variable menu.
