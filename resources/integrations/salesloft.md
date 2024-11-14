---
description: Connect to your users' Salesloft accounts
---

# Salesloft

## Setup Guide

You can find your Salesloft app credentials in your [Salesloft Developer Account.](https://developers.salesloft.com/api.html)

You'll need the following information to set up your Salesloft App with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Add your Salesloft app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your Salesloft App page.
* **Client Secret:** Found under Client Secret on your Salesloft App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Salesloft app to Paragon Connect.png" alt="Connecting your Salesloft app to Paragon Connect"><figcaption></figcaption></figure>

## Connecting to Salesloft

Once your users have connected their Salesloft account, you can use the Paragon SDK to access the Salesloft API on behalf of connected users.

See the Salesloft [REST API documentation](https://developers.salesloft.com/api.html) for their full API reference.

Any Salesloft API endpoints can be accessed with the Paragon SDK as shown in this example.

<pre class="language-javascript"><code class="lang-javascript">// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(&#x3C;ProjectId>, &#x3C;UserToken>);
            
// Fetch a call by ID
<strong>await paragon.request("salesloft", "/v2/activities/calls/&#x3C;CALL ID>.json", {
</strong>  method: "GET"
});

// List people
await paragon.request("salesloft", "/v2/people.json", {
  method: "GET"
});
  
</code></pre>

## Building Salesloft workflows

Once your Saleloft account is connected, you can add steps to perform the following actions:

* Create an Account
* Update an Account
* Get an Account
* Delete an Account
* Search Accounts
* Create a Custom Field
* Update a Custom Field
* Get a Custom Field
* Delete a Custom Field
* Search Custom Fields
* Create a Call
* Get a Call
* Search Calls
* Create a Person
* Update a Person
* Get a Person
* Delete a Person
* Search Persons
* Create a Task
* Update a Task
* Get a Task
* Search Tasks

You can also use the Salesloft Request step to access any of Salesloft's API endpoints without the authentication piece.

When creating or updating records in Salesloft, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Salesloft account. For example, you might want to trigger a workflow whenever new people are created in Salesloft to sync your users' Salesloft contacts to your application in real-time.

<figure><img src="../../.gitbook/assets/Salesloft Triggers in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

You can find the full list of Webhook Triggers for Salesloft below:

* **New Person Created**
* **Person Updated**
* **New Account Created**
* **Account Updated**
