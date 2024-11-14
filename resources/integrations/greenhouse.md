---
description: Connect to your users' Greenhouse accounts
---

# Greenhouse

## Setup Guide

You can find your Greenhouse API Key in your [Greenhouse Developer Account.](https://developers.greenhouse.io/harvest.html)

You'll need the following information to set up your Greenhouse App with Paragon Connect:

* Greenhouse API Key

## Connecting to Greenhouse

Once your users have connected their Greenhouse account, you can use the Paragon SDK to access the Greenhouse API on behalf of connected users.

See the Greenhouse [REST API documentation](https://developers.greenhouse.io/harvest.html) for their full API reference.

Any Greenhouse API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Retrieve a single application
paragon.request("greenhouse", "/applications/<ID>", {
  method: "GET"
});

// Create a candidate
paragon.request("greenhouse", "/candidates", {
  method: "POST",
  body: {
    first_name: "John",
    last_name: "Appleseed",
    email_addresses: ["john@appleseed.com"]
  }
});

// List all of an organization's jobs
paragon.request("greenhouse", "/jobs", {
  method: "GET"
});
  
```

## Building Greenhouse workflows

Once your Greenhouse account is connected, you can add steps to perform the following actions:

* Create Application
* Update Application
* Get Application by ID
* Delete Application
* Create Candidate
* Update Candidate
* Get Candidate by ID
* Delete Candidate
* Create Job Opening
* Update Job Opening
* Get Job Opening by ID

You can also use the Greenhouse Request step to access any of Greenhouse's API endpoints without the authentication piece.

When creating or updating records in Greenhouse, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Greenhouse account. For example, you might want to trigger a workflow whenever new jobs are created in Greenhouse to sync your users' Greenhouse jobs to your application in real-time.

<figure><img src="../../.gitbook/assets/Greenhouse Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Greenhouse below:

* **Candidate Created**
* **Candidate Updated**
* **Job Created**
* **Job Updated**
