---
description: Connect to your users' iManage accounts
---

# iManage

## Setup Guide

You can find your iManage app credentials in your [iManage Developer Account.](https://docs.imanage.com/cc-help/10.3.2/en/Applications.html)

You'll need the following information to set up your iManage App with Paragon Connect:

* Client Key
* Client Secret
* Scopes Requested

### Add your iManage app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client Key:** Found under Client Key on your iManage App page.
* **Client Secret:** Found under Client Secret on your iManage App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys
{% endhint %}

![](<../../.gitbook/assets/Connecting your iManage app to Paragon Connect.png>)

## Connecting to iManage

Once your users have connected their iManage account, you can use the Paragon SDK to access the iManage API on behalf of connected users.

See the iManage [REST API documentation](https://docs.imanage.com/cc-help/10.3.2/en/Applications.html) for their full API reference.

Any iManage API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get library folders
paragon.request("imanage", "/work/api/v2/customers/{customerId}/libraries/{libraryId}/folders", {
  method: "GET"
});

// Create a library folder
paragon.request("imanage", "/customers/{customerId}/libraries/{libraryId}/folders/{folderId}/subfolders", {
  method: "POST",
  body: {
    "name": "Employee Agreements",
    "default_security": "inherit",
    "description": "Contract documents",
    "profile": {
      "custom1": "001",
      "custom1_description": "Microsoft"
    },
    "group_trustees": [],
    "user_trustees": [
      {
        "id": "CPIERCE",
        "access_level": "read_write"
      }
    ]
  }
});
  
```

## Building iManage workflows

Once your iManage account is connected, you use the iManage Request step to access any of iManage's API endpoints without the authentication piece.

When creating or updating records in iManage, you can reference data from previous steps by typing `{{` to invoke the variable menu.
