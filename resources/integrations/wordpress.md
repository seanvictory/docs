---
description: Connect to your users' Wordpress.com accounts
---

# Wordpress.com

## Setup Guide

You can find your WordPress.com app credentials in your [WordPress.com Developer Account.](https://developer.wordpress.com/docs/api/)

You'll need the following information to set up your WordPress.com App with Paragon Connect:

* Client ID
* Client Secret

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Add your WordPress.com app to Paragon

Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from your developer app in their respective sections:

* **Client ID:** Found under Client ID on your WordPress.com App page.
* **Client Secret:** Found under Client Secret on your WordPress.com App page.
* **Permissions:** Specify any additional scopes required by your integration here. [Learn more](https://developer.wordpress.com/docs/oauth2/) about the scopes supported by WordPress.

{% hint style="info" %}
Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

<figure><img src="../../.gitbook/assets/Connecting your Wordpress app to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Connecting to WordPress.com

Once your users have connected their WordPress.com account, you can use the Paragon SDK to access the WordPress.com API on behalf of connected users.

See the WordPress.com [REST API documentation](https://developer.wordpress.com/docs/api/) for their full API reference.

Any WordPress.com API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Retrieve the connected user's WP sites
paragon.request("wordpress.com", "v1.1/me/sites", {
  method: "GET"
});

// Retrieve the number of likes on a certain WP post
paragon.request("wordpress.com", "v1.1/sites/<site_ID>/posts/<post_ID>/likes", {
  method: "GET"
});

// Create
paragon.request("wordpress.com", "sites/<site_ID>/posts/new", {
  method: "POST",
  body: {
    title: "My Post",
    content: "This is my post",
    tags: "api_posts",
    categories: "API"
  }
});
  
```

## Building WordPress.com workflows

Once your WordPress.com account is connected, you use the WordPress.com Request step to access any of WordPress.com's API endpoints without the authentication piece.

When creating or updating records in WordPress.com, you can reference data from previous steps by typing `{{` to invoke the variable menu.
