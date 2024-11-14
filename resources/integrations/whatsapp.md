---
description: Connect to your users' WhatsApp accounts
---

# WhatsApp

## Setup Guide

You can find your WhatsApp app credentials in your [WhatsApp Developer Account.](https://developers.facebook.com/docs/whatsapp/cloud-api/reference)

You'll need the following information to set up your WhatsApp App with Paragon Connect:

* [Permanent Access Token](https://developers.facebook.com/blog/post/2022/12/05/auth-tokens)
* Phone Number ID

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to WhatsApp

Once your users have connected their WhatsApp account, you can use the Paragon SDK to access the WhatsApp API on behalf of connected users.

See the WhatsApp [REST API documentation](https://developers.facebook.com/docs/whatsapp/cloud-api/reference) for their full API reference.

Any WhatsApp API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Send a Message
await paragon.request('whatsapp', '/messages', {
  method: 'POST',
  body: {
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "PHONE_NUMBER",
    "type": "text",
    "text": {
      "preview_url": false,
      "body": "MESSAGE_CONTENT"
    }
  }
});

// Register a Phone
await paragon.request('whatsapp', '/register', {
  method: 'POST',
  body: {
    "messaging_product": "whatsapp",
    "pin": "6_DIGIT_PIN"
  }
});
  
```

## Building WhatsApp workflows

Once your WhatsApp account is connected, you use the WhatsApp Request step to access any of WhatsApp's API endpoints without the authentication piece.

When creating or updating records in WhatsApp, you can reference data from previous steps by typing `{{` to invoke the variable menu.
