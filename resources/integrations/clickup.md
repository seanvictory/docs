---
description: Connect to your users’ ClickUp accounts.
---

# ClickUp

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new ClickUp app if you don't already have one.
{% endhint %}

You can find your ClickUp app credentials by visiting your ClickUp Integrations Portal.

You'll need the following information to set up your ClickUp App with Paragon Connect:

* Client ID
* Client Secret

### Add the Redirect URL to your ClickUp app

Paragon provides a redirect URL to send information to your ClickUp app. To add the redirect URL to your ClickUp app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your [ClickUp account](https://clickup.com/), click your Workspace avatar in the lower-left corner

3\. Select **Integrations**.

4\. Click **ClickUp API**.

5\. Select your application.

6\. Under **Redirect URL(s)**, paste-in Paragon Connect's redirect URL found in Step 1. Click the **Save** button to save your changes.

![](<../../.gitbook/assets/Adding the Paragon Redirect URL to Clickup for Paragon Connect.png>)

### Add your ClickUp app to Paragon

1\. Select ClickUp from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](clickup.md#add-the-redirect-url-to-your-clickup-app) in their respective sections:

* **Client ID:**&#x20;
  * Log in to your ClickUp dashboard.
  * Select "**Settings"** from the sidebar.
  * Under **Integrations > ClickUp API**, select your application.
  * Copy the **Client ID** from "**Client ID**".
* **Client Secret:**
  * Log in to your ClickUp dashboard.
  * Select "**Settings"** from the sidebar.
  * Under **Integrations > ClickUp API**, select your application.
  * Copy the **Client Secret** from "**Client Secret**".

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your ClickUp application to Paragon Connect (1).png>)

## Connecting to ClickUp

Once your users have connected their ClickUp account, you can use the Paragon SDK to access the ClickUp API on behalf of connected users.

See the ClickUp [REST API documentation](https://clickup.com/api) for their full API reference.

Any ClickUp API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get current team information
await paragon.request("clickup", "/team", {
  method: "GET"
});

// Get lists outside of folders
await paragon.request("clickup", "/space/<Space ID>/list?archived=false", {
  method: "GET"
});

// Create task in list
await paragon.request("clickup", "/list/<List ID>/task", {
  method: "POST",
  body: {
    name: "New Task Name",
    description: "New Task Description",
    status: "Open"
  }
});
  
```

## Building ClickUp workflows

Once your ClickUp account is connected, you can add steps to perform the following actions:

* Create Task
* Update Task
* Get Task by ID
* Search Tasks
* Delete Task

When creating or updating Tasks in ClickUp, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' ClickUp account. For example, you might want to trigger a workflow whenever new tasks are created in ClickUp to sync your users' ClickUp tasks to your application in real-time.

You can find the full list of Webhook Triggers for ClickUp below:

* **New Folder Created**
* **Folder Updated**
* **New List Created**
* **List Updated**
* **New Space Created**
* **Space Updated**
* **New Task Created**
* **Task Updated**
