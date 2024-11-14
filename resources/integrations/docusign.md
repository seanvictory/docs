---
description: Connect to your users' DocuSign accounts.
---

# DocuSign

## Setup Guide

You can find your DocuSign app credentials in your [DocuSign Developer Account.](https://developers.docusign.com/docs/esign-rest-api/reference/)

You'll need the following information to set up your DocuSign App with Paragon Connect:

* Integration Key
* Secret Key
* Scopes Requested

### Add your DocuSign app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Integration Key:** Found under Apps and Keys section on your DocuSign App page.
* **Secret Key:** Found under Apps and Keys section on your DocuSign App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Integration Key and Secret Key blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your DocuSign app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to DocuSign

Once your users have connected their DocuSign account, you can use the Paragon SDK to access the DocuSign API on behalf of connected users.

See the DocuSign [REST API documentation](https://developers.docusign.com/docs/esign-rest-api/reference/) for their full API reference.

Any DocuSign API endpoints can be accessed with the Paragon SDK as shown in this example.

<pre class="language-javascript"><code class="lang-javascript">// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(&#x3C;ProjectId>, &#x3C;UserToken>);
            
// Get recipient signature information for a signer
await paragon.request("docusign", "/restapi/v2.1/accounts/{accountId}/envelopes/{envelopeId}/recipients/{recipientId}/signature", {
  method: "GET"
});

// List documents associated with a DocuSign envelope object
<strong>await paragon.request("docusign", "/restapi/v2.1/accounts/{accountId}/envelopes/{envelopeId}/documents
</strong>", {
  method: "GET"
});

// Get a list of invoices for the account
await paragon.request("docusign", "/billing_invoices", {
  method: "GET"
});
  
</code></pre>

## Building DocuSign workflows

Once your DocuSign account is connected, you can add steps to perform the following actions:

* Create an Envelope
* Get Envelope by ID
* Update Envelope
* Send an Envelope
* Search Envelopes
* Envelope Custom Fields (CRUD)

You can also use the DocuSign Request step to access any of DocuSign's API endpoints without the authentication piece.

When creating or updating records in DocuSign, you can reference data from previous steps by typing `{{` to invoke the variable menu.

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' DocuSign account. For example, you might want to trigger a workflow whenever new envelopes are signed in DocuSign to sync your users' DocuSign envelopes to your application in real-time.

You can find the full list of Webhook Triggers for DocuSign below:

* **Envelope Sent**
* **Envelope Delivered**
* **Envelope Signed/Completed**
* **Envelope Declined**
* **Recipient Sent**
* **Recipient Signed/Completed**
* **Recipient Declined**
