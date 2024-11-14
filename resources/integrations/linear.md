---
description: Connect to your users' Linear accounts
---

# Linear

## Setup Guide

You can find your Linear app credentials in your [Linear Developer Account.](https://developers.linear.app/docs/graphql/working-with-the-graphql-api)

You'll need the following information to set up your Linear App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Linear app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Production > Client ID on your Linear App page.
* **Client Secret:** Found under Production > Client Secret on your Linear App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Linear app to Paragon Connect.png>)

## Connecting to Linear

Once your users have connected their Linear account, you can use the Paragon SDK to access the Linear API on behalf of connected users.

See the Linear [REST API documentation](https://developers.linear.app/docs/graphql/working-with-the-graphql-api) for their full API reference.

Any Linear API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get all issues associated with a given team ID
paragon.request("linear", "/", {
  method: "POST",
  body: {
    "query": `
      query Team {
      team(id: "<Team ID>") {
        id
        name
    
        issues {
          nodes {
            id
            title
            description
            assignee {
              id
              name
            }
            createdAt
            archivedAt
          }
        }
      }
    }` 
  }
});

// Get an issue by ID
paragon.request("linear", "/", {
  method: "POST",
  body: {
    "query": `query Issue {
      issue(id: "<Issue ID>") {
        id
        title
        description
      }
    }`
  }
});
  
```

## Building Linear workflows

Once your Linear account is connected, you can add steps to perform the following actions:

* Create Issue
* Update Issue
* Get Issue by ID
* Get Issue by Issue Identifier
* Search Issues
* Delete Issue
* Archive Issue
* Create Sub-Issue
* Create Project
* Update Project
* Get Project by ID
* Delete Project

When creating or updating issues and projects in Linear, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Linear account. For example, you might want to trigger a workflow whenever new issues are created in Linear to sync your users' Linear issues to your application in real-time.

You can find the full list of Webhook Triggers for Linear below:

* Issue Created
* Issue Status Updated
* Label Added or Removed from Issue
* Issue Deleted
