---
description: Connect to your users' Twitter accounts
---

# Twitter

## Setup Guide

You can find your Twitter app credentials in your [Twitter Developer Account.](https://developer.twitter.com/en/docs/twitter-api)

You'll need the following information to set up your Twitter App with Paragon Connect:

* Consumer API Key
* Consumer Secret
* Scopes Requested

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add the Redirect URL to your Twitter app

Paragon provides a redirect URL to send information to your Twitter app. To add the redirect URL to your Twitter app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log in to your [Twitter Developer Portal](https://developer.twitter.com/en/portal/dashboard).

3\. Select your application from the developer portal.

4\. Click the Edit (<img src="../../.gitbook/assets/image (78).png" alt="" data-size="line">) button next to **User authentication set up.**

5\. Under **App info,** paste the Paragon redirect URL into the "Callback URI / Redirect URL" field.

6\. Press the `Save` button to save the Redirect URL.

### Add your Twitter app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Consumer API Key:** Found under Consumer API Key on your Twitter App page.
* **Consumer Secret:** Found under Consumer Secret on your Twitter App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
Leaving the Consumer API Key and Consumer Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Twitter app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to Twitter

Once your users have connected their Twitter account, you can use the Paragon SDK to access the Twitter API on behalf of connected users.

See the Twitter [REST API documentation](https://developer.twitter.com/en/docs/twitter-api) for their full API reference.

Any Twitter API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get authenticated user info
paragon.request("twitter", "/2/users/me", {
  method: "GET"
});

// Get tweets for a user
paragon.request("twitter", "/2/users/<User ID>/tweets", {
  method: "GET"
});

// Post a tweet
paragon.request("twitter", "/2/tweets", {
  method: "POST",
  body: { text: "Hello World!" }
});
  
```

## Building Twitter workflows

Once your Twitter account is connected, you use the Twitter Request step to access any of Twitter's API endpoints without the authentication piece.

When creating or updating records in Twitter, you can reference data from previous steps by typing `{{` to invoke the variable menu.
