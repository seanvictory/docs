---
description: Connect to your users' Todoist accounts.
---

# Todoist

## Setup Guide

You can find your Todoist app credentials in your [Todoist Developer Account](https://developer.todoist.com/guides/#oauth).

You'll need the following information to set up your Todoist App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Todoist app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Todoist App page.
* **Client Secret:** Found under Client Secret on your Todoist App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Todoist app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Todoist

Once your users have connected their Todoist account, you can use the Paragon SDK to access the Todoist API on behalf of connected users.

See the Todoist [REST API documentation](https://developer.todoist.com/rest/v2/#overview) for their full API reference.

Any Todoist API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create a Project
await paragon.request("todoist", "/rest/v2/projects", {
  method: "POST",
  body: {
    "name": "My Project",
    "parent_id":"Parent project ID"
  }
});

// Get a Project
await paragon.request("todoist", "/sync/v9/projects/get?project_id=<project_id>", {
  method: "GET"
});

// Get a Task
await paragon.request("todoist", "/rest/v2/tasks/<task_id>", {
  method: "GET"
});
  
```

## Building Todoist workflows

Once your Todoist account is connected, you can add steps to perform the following actions:

* Create Project
* Update Project
* Get Project by ID
* Get All Projects
* Delete Project
* Create Task
* Update Task
* Get Task by ID
* Search Tasks
* Close Task
* Delete Task

You can also use the Todoist Request step to access any of Todoist's API endpoints without the authentication piece.

When creating or updating records in Todoist, you can reference data from previous steps by typing `{{` to invoke the variable menu.
