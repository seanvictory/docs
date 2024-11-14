---
description: Connect your Jira app for OAuth in Paragon.
---

# Jira

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new Jira app and Jira site if you don't already have one.
{% endhint %}

You can find your Jira app credentials by visiting your [Jira developer portal](https://developer.atlassian.com/apps/).

You'll need the following information to set up your Jira app with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add the Redirect URL to your Jira app

Paragon provides a redirect URL to send information to your Jira app. To add the redirect URL to your Jira app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your [Jira developer dashboard](https://developer.atlassian.com/apps/), select your application.

3\. Under **APIS and Features > OAuth 2.0 (3LO) > Callback URL**, paste-in the Paragon Connect redirect URL found in Step 1.

![](<../../.gitbook/assets/Selecting your JIRA application and callback URL.gif>)

### Add your Jira app to Paragon

1\. Select **Jira** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](jira.md#add-the-redirect-url-to-your-jira-app) in their respective sections:

* **Client ID:** Found under App Details > Client ID on your Jira App page.
* **Client Secret:** Found under App Details > Secret on your Jira App page.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your JIRA app to Paragon Connect.png>)

## Connecting to Jira

Once your users have connected their Jira account, you can use the Paragon SDK to access the Jira API on behalf of connected users.

See the Jira [REST API documentation](https://developer.atlassian.com/server/jira/platform/rest-apis/) for their full API reference.

Any Jira API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Create Issue
await paragon.request("jira", "/rest/api/3/issue", {
  method: "POST",
  body: {
    "fields": {
      "summary": "Main order flow broken",
      "issuetype": { "id": "10003" },
      "project": { "id": "10000" }
    }
  }
});


// Get Issue
await paragon.request("jira", "/rest/api/3/search", { 
  method: "GET",
});
  
```

## Building Jira workflows

Once your Jira account is connected, you can add steps to perform the following actions:

* Create issue
* Update issue
* Get issue by issue key
* Search issues
* Search issues by JQL query
* Get projects

When creating or updating cards in Jira, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating a JIRA Issue in Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Jira account. For example, you might want to trigger a workflow whenever Issues are updated to sync your users' Jira Issues to your application in real-time.

![](<../../.gitbook/assets/Jira Webhook Triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Jira below:

* **New Issue**
* **Issue Updated**
* **New Comment**
* **Project Created**
* **Project Updated**

{% hint style="info" %}
In order to use the **Project Created** and **Project Updated** triggers, you will need to add the `manage:jira-configuration` scope to your Jira application.
{% endhint %}
