---
description: Connect to your users' Intellum accounts
---

# Intellum

## Setup Guide

You can find your Intellum app credentials in your [Intellum Account](https://www.intellum.com/).

You'll need the following information to set up your Intellum App with Paragon Connect:

* Organization Domain
* Application UID
* Private Key

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Intellum

Once your users have connected their Intellum account, you can use the Paragon SDK to access the Intellum API on behalf of connected users.

See the Intellum [REST API documentation](https://experience.intellum.com/student/path/643313-intellum-api-v3) for their full API reference.

Any Intellum API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Users
paragon.request("intellum", "/api/v3/users", {
  method: "GET"
});
// Get Enrollments for a particular user ID
paragon.request("intellum", "/api/v3/enrollments?user_id=<User ID>,", {
  method: "GET"
});
  
```

## Building Intellum workflows

Once your Intellum account is connected, you use the Intellum Request step to access any of Intellum's API endpoints without the authentication piece.

When creating or updating records in Intellum, you can reference data from previous steps by typing `{{` to invoke the variable menu.
