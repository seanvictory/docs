---
description: Connect to your users' Magento accounts
---

# Magento

## Setup Guide

You'll need the following information to set up your Magento App with Paragon Connect:

* Magento Store Domain
* Username
* Password

### Add your Magento app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your store in their respective sections:

* **Magento Store Domain**
* **Username**
* **Password**

## Connecting to Magento

Once your users have connected their Magento account, you can use the Paragon SDK to access the Magento API on behalf of connected users.

See the Magento [REST API documentation](https://magento.redoc.ly/2.3.7-admin/) for their full API reference.

Any Magento API endpoints can be accessed with the Paragon SDK as shown in this example.

{% code lineNumbers="true" %}
```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Fetch all products
paragon.request("magento", "/V1/products?searchCriteria=", {
  method: "GET"
});

// Create a customer
paragon.request("magento", "/V1/customers", {
  method: "POST",
  body: {
    "customer": {
      "email": "user@domain.com",
      "firstname": "John",
      "lastname": "Appleseed",
    }
  }
});

// Get order by ID
paragon.request("magento", "/V1/orders/{id}", {
  method: "GET"
});
  
```
{% endcode %}

## Building Magento workflows

Once your Magento account is connected, you can add steps to perform the following actions:

* Create Customer
* Update Customer
* Get Customer by ID
* Search Customers
* Delete Customer
* Create Order
* Update Order
* Get Order by ID
* Search Orders
* Create Product
* Update Product
* Get Product by SKU
* Search Products
* Delete Product

When creating or updating records in Magento, you can reference data from previous steps by typing `{{` to invoke the variable menu.
