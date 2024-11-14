---
description: Connect to your users' Snowflake accounts
---

# Snowflake

## Setup Guide

You can find your Snowflake app credentials in your [Snowflake Developer Account.](https://docs.snowflake.com/en/developer-guide/sql-api/index.html)

You'll need the following information to set up your Snowflake App with Paragon Connect:

* Snowflake subdomain
* Snowflake Private Key
* Snowflake Passphrase
* Snowflake Username

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to Snowflake

Once your users have connected their Snowflake account, you can use the Paragon SDK to access the Snowflake API on behalf of connected users.

See the Snowflake [REST API documentation](https://docs.snowflake.com/en/developer-guide/sql-api/index.html) for their full API reference.

Any Snowflake API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Perform a simple select query
await paragon.request('snowflake', '/statements', {
  method: 'POST',
  body: {
    "statement": "SELECT * FROM country",
    "schema": "LOCATION",
    "warehouse": "COMPUT_WH"
  });

// Using Bind Variables in a select query
await paragon.request('snowflake', '/statements', {
  method: 'POST',
  body: {
    {
      "statement": "select * from T where c1=?",
      "timeout": 60,
      "database": "TESTDB",
      "schema": "TESTSCHEMA",
      "warehouse": "TESTWH",
      "role": "TESTROLE",
      "bindings": {
        "1": {
          "type": "FIXED",
          "value": "123"
        }
      }
    }
  });
  
```

## Building Snowflake workflows

Once your Snowflake account is connected, you use the Snowflake Request step to access any of Snowflake's API endpoints without the authentication piece.

When creating or updating records in Snowflake, you can reference data from previous steps by typing `{{` to invoke the variable menu.
