---
description: Connect to your users' Stripe accounts.
---

# Stripe

## Setup Guide

You can find your Stripe app credentials by visiting your [Stripe API Key Settings](https://app.gitbook.com/s/-MCNfhzJ-anjX9piqrOb/)

{% hint style="info" %}
**Note:** You'll need to create a new Stripe API Key if you don't already have one.
{% endhint %}

You'll need the following information to set up your Stripe API Key with Paragon Connect:

* [Stripe API Key](https://dashboard.stripe.com/apikeys)

## Connecting to Stripe

Once your users have connected their Stripe account, you can use the Paragon SDK to access the Stripe API on behalf of connected users.

See the Stripe [REST API documentation](https://stripe.com/docs/api) for their full API reference.

Any Stripe API endpoints can be accessed with the Paragon SDK as shown in this example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration.

// Authenticate the user
paragon.authenticate(<ProjectID>, <Paragon User Token>);

// Create Customer
await paragon.request("stripe", "/v1/customers", {
  method: "POST",
  body: {
    name: "test",
    email: "example@example.com",
    description: "Create customer for test",
    }
});

// Get Customers
await paragon.request("stripe", "/v1/customers", {
  method: "GET",
});

```
{% endtab %}
{% endtabs %}

## Building Stripe workflows

Once your Stripe account is connected, you can add steps to perform the following actions:

* Create Customer
* Update Customer
* Get Customer by ID
* List Customers
* Create Subscription
* List Subscriptions
* Create Product
* Get Product by ID
* List Products
* List Balance Transaction
* List Plans

When using Stripe, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating Stripe workflows in Paragon Connect.png>)

## Using the Connect Portal

The Connect Portal supports Secret API keys and Restricted API keys. While Secret API keys can be used immediately, some configuration is required for Restricted API keys.

The Restricted API key must allow the `rak_connected_account_read` permission (called “All Connect resources” in the Resource Types section of configuring a Restricted API key). The Connect Portal cannot save the key if it does not include this permission.
