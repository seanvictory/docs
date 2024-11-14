# ServiceNow

## Setup Guide

### **Creating a ServiceNow Test Account**&#x20;

You can create a ServiceNow test account from the [ServiceNow Developer Portal](https://developer.servicenow.com/dev.do).

In the ServiceNow Developer Portal, you can create a free developer instance by clicking the **Request Instance** button in the page header.&#x20;

To connect to ServiceNow, your users will need to provide an **Instance URL**, **Username**, and **Password**. You can find these values for your test account by going to the **User Icon > Manage instance password.**

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-03 at 14.56.04@2x.png" alt=""><figcaption><p>Creating a developer instance within ServiceNow's Developer Portal is a self-service process.</p></figcaption></figure>

</div>

## Using the Paragon SDK for ServiceNow

Once your users have connected their ServiceNow account, you can use the Paragon SDK to access the ServiceNow API on behalf of connected users.

See the ServiceNow [REST API documentation](https://docs.servicenow.com/bundle/paris-application-development/page/build/applications/concept/api-rest.html) for their full API reference.

Any ServiceNow API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get incident records
await paragon.request("servicenow", "/now/table/incident", {
  method: "GET",
});
            
// Create incident records
await paragon.request("servicenow", "/now/table/incident", {
  method: "POST",
  body: {
    "short_description":"Test incident creation",
    "comments":"These are my comments"
  }
});
```

## Building ServiceNow workflows

Once your ServiceNow account is connected, you can add steps to perform the following actions:

* Get Ticket by ID
* Create Ticket
* Update Ticket

You can also use the ServiceNow Request step to access any of ServiceNow's API endpoints without the authentication piece.

When creating or updating records in ServiceNow, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating a ServiceNow workflow in Paragon Connect.png>)

