---
description: Connect your Klaviyo app for OAuth in Paragon
---

# Klaviyo

## Setup Guide

You can find your Klaviyo API Keys by visiting your [Klaviyo Account dashboard](https://www.klaviyo.com/account#api-keys-tab).

### Prerequisites

* Klaviyo Account. You can create one [here](https://www.klaviyo.com/).

## Connecting to Klaviyo

Once your users have connected their Klaviyo account, you can use the Paragon SDK to access the Klaviyo API on behalf of connected users.

See the Klaviyo [REST API documentation](https://www.klaviyo.com/docs/api/v2/lists) for their full API reference.

Any Klaviyo API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Create List
await paragon.request("klaviyo", "/v2/lists", {
  method: "POST",
  body: { "list_name": "your_list_name" }
});


// Query Lists
await paragon.request("klaviyo", "/v2/lists", {
  method: "GET"
});
```

## Creating your Klaviyo Private API Key

Your end-users will be required to enter their Klaviyo Private API Key as authentication when first connecting to your application.

To create a Klaviyo Private API Key:

1. Login to [Klaviyo Account](https://www.klaviyo.com/account#api-keys-tab).
2. Navigate to **Accounts > Settings > API Keys**, and click the blue "**Create Private API Key**" button.
3. Copy your private API key
4. Paste your private API key to authenticate your account.

## Building Klaviyo workflows

Once your Klaviyo account is connected, you can add steps to perform the following actions:

* Create Campaign
* Get Campaigns
* Send Campaign
* Create List
* Add Subscriber to List
* Remove Subscriber from List
* Get Lists
* Get List Subscribers
* Get Profile
* Update Profile
* Create Template
* Get Templates
* Get Segments
* Get Segment Subscribers

When creating or updating campaigns and lists in Klaviyo, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Adding a new subscriber to Klaviyo in Paragon Connect.png>)
