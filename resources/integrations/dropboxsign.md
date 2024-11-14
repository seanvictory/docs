---
description: Connect to your users' Dropbox Sign accounts
---

# Dropbox Sign

## Setup Guide

You can find your Dropbox Sign API Key in your [Dropbox Sign API Settings](https://app.hellosign.com/home/myAccount?current\_tab=integrations#api)[.](https://developers.hellosign.com/api/reference/welcome/)

You'll need the following information to set up your Dropbox Sign App with Paragon Connect:

* API Key

## Connecting to Dropbox Sign

Once your users have connected their Dropbox Sign account, you can use the Paragon SDK to access the Dropbox Sign API on behalf of connected users.

See the Dropbox Sign [REST API documentation](https://developers.hellosign.com/api/reference/welcome/) for their full API reference.

Any Dropbox Sign API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create Embedded Signature Request
await paragon.request('dropboxsign', 'signature_request/create_embedded', {
  method: 'POST'
  body: {
    "title": "NDA with Acme Co.",
    "subject": "The NDA we talked about",
    "message": "Please sign this NDA and then we can discuss more. Let me know if you have any questions.",
    "signers": [
      {
        "email_address": "jack@example.com",
        "name": "Jack",
        "order": 0
      },
    ],
    "cc_email_addresses": [
      "lawyer@dropboxsign.com",
      "lawyer@dropboxsign.com"
    ],
    "file_urls": [
      "https://www.dropbox.com/s/ad9qnhbrjjn64tu/mutual-NDA-example.pdf?dl=1"
    ],
    "metadata": {
      "custom_id": 1234,
      "custom_text": "NDA #9"
    },
    "signing_options": {
      "draw": true,
      "type": true,
      "upload": true,
      "phone": false,
      "default_type": "draw"
    },
    "field_options": {
      "date_format": "DD - MM - YYYY"
    },
    "test_mode": true
  }
});

// Get the status of a Signature Request
await paragon.request("dropboxsign", "signature_request/<signature_request_id>", {
  method: "GET",
});  
```

## Building Dropbox Sign workflows

Once your Dropbox Sign account is connected, you can add steps to perform the following actions:

* Create and Send Signature Request
* Update Signature Request
* Get Signature Request by ID
* Search Signature Requests
* Cancel Incomplete Signature Request
* Download Files

You can also use the Dropbox Sign Request step to access any of Dropbox Sign's API endpoints without the authentication piece.

When creating or updating records in Dropbox Sign, you can reference data from previous steps by typing `{{` to invoke the variable menu.
