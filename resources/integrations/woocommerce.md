---
description: Connect to your users' WooCommerce accounts
---

# WooCommerce

## Setup Guide

You can find your WooCommerce app credentials in your [WooCommerce Developer Account.](https://woocommerce.github.io/woocommerce-rest-api-docs/)

## Connecting to WooCommerce

Once your users have connected their WooCommerce account, you can use the Paragon SDK to access the WooCommerce API on behalf of connected users.

See the WooCommerce [REST API documentation](https://woocommerce.github.io/woocommerce-rest-api-docs/) for their full API reference.

Any WooCommerce API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get all customers
paragon.request("woocommerce", "/customers", {
  method: "GET"
});

// Get order by id
paragon.request("woocommerce", "/orders/<id>", {
  method: "GET"
});

// Create a product
paragon.request("woocommerce", "/products", {
  method: "POST",
  body: {
    name: "Premium Quality",
    type: "simple",
    regular_price: "21.99",
    description: "This is our Premium Quality offering",
  }
});
  
```

## Building WooCommerce workflows

Once your WooCommerce account is connected, you can add steps to perform the following actions:

* Create Customer
* Get Customer by ID
* Search Customers
* Update Customer
* Delete Customer
* Create Order
* Get Order by ID
* Search Orders
* Update Order
* Delete Order
* Create Product
* Get Product by ID
* Search Products
* Update Product
* Delete Product

You can also use the WooCommerce Request step to access any of WooCommerce's API endpoints without the authentication piece.

When creating or updating records in WooCommerce, you can reference data from previous steps by typing `{{` to invoke the variable menu.
