---
description: Connect to your users' GitHub accounts
---

# GitHub

## Setup Guide

You can find your GitHub app credentials in your [GitHub Developer Account.](https://docs.github.com/en/rest)

You'll need the following information to set up your GitHub App with Paragon Connect:

* Client ID
* Client Secret

### Add the Redirect URL to your GitHub app

Paragon provides a redirect URL to send information to your GitHub app. To add the redirect URL to your GitHub app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log into your GitHub Account.

3\. In the top-right corner, select **Settings**

4\. Under **Developer Settings > OAuth Apps**, select your GitHub app.

{% hint style="info" %}
**Note:** You'll need to create a new GitHub app if you don't already have one
{% endhint %}

5\. Under **General >  Authorization callback URL**, paste the Redirect URL provided in Step 1.

<figure><img src="../../.gitbook/assets/Adding the Redirect URL to your GitHub application for Paragon Connect.gif" alt=""><figcaption></figcaption></figure>

### Add your GitHub app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Settings > Developer settings > {YOUR APP} > Client ID on your GitHub App page.
* **Client Secret:** Found under Settings > Developer settings > {YOUR APP} > Client Secret on your GitHub App page.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your GitHub app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to GitHub

Once your users have connected their GitHub account, you can use the Paragon SDK to access the GitHub API on behalf of connected users.

See the GitHub [REST API documentation](https://docs.github.com/en/rest) for their full API reference.

Any GitHub API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get issues associated with a repository
paragon.request("github", "/repos/{owner}/{repo}/issues", {
  method: "GET"
});

// Create a comment on an issue
paragon.request("github", "/repos/{owner}/{repo}/issues/{issue_number}/comments", {
  method: "POST",
  body: {
    body: "Looks good to me!"
  }
});

// Specify labels for an issue
paragon.request("github", "/repos/{owner}/{repo}/issues/{issue_number}/labels
", {
  method: "PUT",
  body: {
    labels: [
      'bug',
      'enhancement'
    ]
  }
});
  
```

## Building GitHub workflows

Once your GitHub account is connected, you can add steps to perform the following actions:

* Create Issue
* Update Issue
* Get Issue by Number
* Lock an Issue
* Search an Issue
* Create Release
* Update Release
* Get Release by ID
* Get Release by Tag Name
* Delete Release

When creating or updating issues in GitHub, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' GitHub account. For example, you might want to trigger a workflow whenever new issues are created in GitHub to sync your users' GitHub issues to your application in real-time.

You can find the full list of Webhook Triggers for GitHub below:

* **Issue Created**
* **Issue Updated**
* **PR Created**
* **PR Updated**
* **Project Created**
* **Project Updated**
* **Project Created (Classic)**
* **Project Updated (Classic)**
* **Project Item Created**
* **Project Item Updated**

