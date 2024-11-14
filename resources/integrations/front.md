---
description: Connect to your users' Front accounts.
---

# Front

## Setup Guide

You can find your Front app credentials in your [Front Developer Account.](https://dev.frontapp.com/reference/introduction)

You'll need the following information to set up your Front App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Front app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Front App page.
* **Client Secret:** Found under Client Secret on your Front App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Front app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Front

Once your users have connected their Front account, you can use the Paragon SDK to access the Front API on behalf of connected users.

See the Front [REST API documentation](https://dev.frontapp.com/reference/introduction) for their full API reference.

Any Front API endpoints can be accessed with the Paragon SDK as shown in this example.

<pre class="language-javascript"><code class="lang-javascript">// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(&#x3C;ProjectId>, &#x3C;UserToken>);
            
<strong>// Create a Conversation
</strong><strong>await paragon.request('front', '/conversations', {
</strong>  method: "POST",
  body: {
    "type": "discussion",
    "inbox_id": "abc123",
    "subject": "Paragon",
    "comment": {
      "body": "Test Comment"
    }
  }
});

// List Contacts
await paragon.request("front", "/contacts", {
  method: "GET"
});

// Create a Contact
await paragon.request('front', '/contacts', {
  method: "POST",
  body: {
    "name": "Foo Westwood",
    "is_spammer": false,
    "handles": [
      {
        "handle": "@foo",
        "source": "twitter"
      }
    ]
  }
});
  
</code></pre>

## Building Front workflows

Once your Front account is connected, you can add steps to perform the following actions:

* Create Account
* Update Account
* Get Account by ID
* Search Accounts
* Delete Account
* Create Contact
* Update Contact
* Get Contact by ID
* Search Contacts
* Delete Contact

You can also use the Front Request step to access any of Front's API endpoints without the authentication piece.

When creating or updating records in Front, you can reference data from previous steps by typing `{{` to invoke the variable menu.
