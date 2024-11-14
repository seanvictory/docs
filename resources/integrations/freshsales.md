---
description: Connect to your users' Freshsales accounts
---

# Freshsales

## Setup Guide

You'll need the following information to set up your Freshsales App with Paragon Connect:

* Domain
* API Key

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your Freshsales app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Domain:** Found under https://\[domain].myfreshworks.com/
* **API Key:** Found under Profile Settings > API Settings > Your API Key on your Freshsales settings page.

## Connecting to Freshsales

Once your users have connected their Freshsales account, you can use the Paragon SDK to access the Freshsales API on behalf of connected users.

See the Freshsales [REST API documentation](https://developer.freshsales.io/api/) for their full API reference.

Any Freshsales API endpoints can be accessed with the Paragon SDK as shown in this example.

<pre class="language-javascript"><code class="lang-javascript">// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(&#x3C;ProjectId>, &#x3C;UserToken>);
            
// Create a Contact
<strong>await paragon.request("freshsales", "/contacts", {
</strong>  method: "POST",
  body: {
    "contact": {
        "first_name": "James",
        "last_name": "Westwood",
        "mobile_number":"1-926-555-9503"
    }
  }
});

// Create a Lead
<strong>await paragon.request("freshsales", "/leads", {
</strong>  method: "POST",
  body: {
  "lead": {
         "first_name": "Foo",
         "last_name": "Westwood",
         "mobile_number":"1-926-652-9503",
         "company": { 
            "name": "Widgetz.io"
        } 
    }
  }
});

// Get all Deals
await paragon.request("freshsales", "/deals/view/&#x3C;view_id>", {
  method: "GET"
});
  
</code></pre>

## Building Freshsales workflows

Once your Freshsales account is connected, you use the Freshsales Request step to access any of Freshsales's API endpoints without the authentication piece.

When creating or updating records in Freshsales, you can reference data from previous steps by typing `{{` to invoke the variable menu.
