---
description: Connect to your users' OpenAI accounts
---

# OpenAI

## Setup Guide

You can find your OpenAI app credentials in your [OpenAI Developer Account.](https://platform.openai.com/docs/api-reference/introduction)

You'll need the following information to set up your OpenAI App with Paragon Connect:

* [OpenAI API Key](https://platform.openai.com/account/api-keys)

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

## Connecting to OpenAI

Once your users have connected their OpenAI account, you can use the Paragon SDK to access the OpenAI API on behalf of connected users.

See the OpenAI [REST API documentation](https://platform.openai.com/docs/api-reference/introduction) for their full API reference.

Any OpenAI API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Perform a completion
paragon.request("openai", "/completions", {
  method: "POST",
  body: {
    "model": "text-davinci-003",
    "prompt": "Say this is a test",
    "max_tokens": 7,
    "temperature": 0,
    "top_p": 1,
    "n": 1,
    "stream": false,
    "logprobs": null,
    "stop": "\n"
  }
});

// Create an image
paragon.request("openai", "/images/generations", {
  method: "POST",
  body: {
    "prompt": "A cute baby sea otter",
    "n": 2,
    "size": "1024x1024"
  }
});
  
```

## Building OpenAI workflows

Once your OpenAI account is connected, you use the OpenAI Request step to access any of OpenAI's API endpoints without the authentication piece.

When creating or updating records in OpenAI, you can reference data from previous steps by typing `{{` to invoke the variable menu.
