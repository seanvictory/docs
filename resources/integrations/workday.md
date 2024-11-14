---
description: Connect to your users' Workday accounts.
---

# Workday

## Setup Guide

You'll need the following information to set up your Workday App with Paragon Connect:

* Subdomain
* Username
* Password
* Tenant Name

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Workday app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Subdomain:** Found in your account URL address: https://\[host\_name].workday.com/
* **Username:** The username for the account connected account.
* **Password:** The password for the connected account/
* **Tenant Name:** Found in your account URL address: https://.workday.com/\[Tenant Name]/d/home/html.

## Connecting to Workday

Once your users have connected their Workday account, you can use the Paragon SDK to access the Workday API on behalf of connected users.

See the Workday [REST API documentation](https://community.workday.com/api) for their full API reference.

Any Workday API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
await paragon.request("workday", "/Human_Resources/v40.1", { 
  method: "POST",
  body: `<soapenv:Body>
  <bsvc:Get_Workers_Request>
    <bsvc:Request_Criteria></bsvc:Request_Criteria>
    <bsvc:Response_Filter></bsvc:Response_Filter>
    <bsvc:Response_Group>
      <bsvc:Include_Reference>true</bsvc:Include_Reference>
    </bsvc:Response_Group>
  </bsvc:Get_Workers_Request>
</soapenv:Body>`
});
  
```

## Building Workday workflows

Once your Workday account is connected, you use the Workday Request step to access any of Workday's API endpoints without the authentication piece.

When creating or updating records in Workday, you can reference data from previous steps by typing `{{` to invoke the variable menu.
