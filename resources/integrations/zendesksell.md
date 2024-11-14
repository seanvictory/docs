---
description: Connect to your users' Zendesk Sell accounts
---

# Zendesk Sell

## Setup Guide

You can find your Zendesk Sell app credentials by visiting your [Zendesk Developer App Console](https://developer.zendesk.com/documentation/).

You'll need the following information to set up your Zendesk Sell app with Paragon:

* Client ID
* Client Secret

### Add the Redirect URL to your Zendesk Sell app

Paragon provides a redirect URL to send information to your Zendesk Sell app. To add the redirect URL to your Zendesk Sell app:

1\. Copy the link under "**Redirect URL"** in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. In your Zendesk dashboard, click the gear icon on the left.

3\. Under **Channels > API > OAuth Clients**, click the "Add OAuth Client" button.

![](<../../.gitbook/assets/Accessing Zendesk OAuth Clients.gif>)

4\. Fill out your **Client Name** and **Description**.

5\. Under "**Redirect URLs**", paste the Redirect URL from Paragon.

6\. Press the **Save** button.

7\. Scroll down to the bottom of the page to copy your **Secret**. We'll use this in the next step.

### Add your Zendesk Sell app to Paragon

1\. Select Zendesk Sell from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from the end of [Step 1](zendesksell.md#add-the-redirect-url-to-your-zendesk-sell-app) in their respective sections:

* **Client ID:** Found at the end of Step 1.
* **Client Secret:** Found at the end of Step 1.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

## Connecting to Zendesk Sell

Once your users have connected their Zendesk account, you can use the Paragon SDK to access the Zendesk API on behalf of connected users.

See the Zendesk [REST API documentation](https://developer.zendesk.com/rest\_api/docs/support/introduction) for their full API reference.

Any Zendesk API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Create a Contact
await paragon.request("zendesksell", "/contacts", {
    method: "POST",
    body: {
      "contact_id": 1,
      "name": "Mark Johnson",
      "first_name": "Mark",
      "last_name": "Johnson",
      "title": "CEO",
      "description": "I know him via Tom",
      "industry": "Design Services",
      "website": "http://www.designservice.com",
      "email": "mark@designservices.com",
      "phone": "508-778-6516",
      "mobile": "508-778-6516",
      "fax": "+44-208-1234567",
      "twitter": "mjohnson",
      "facebook": "mjohnson",
      "linkedin": "mjohnson",
      "skype": "mjohnson",
      "address": {
        "line1": "2726 Smith Street",
        "city": "Hyannis",
        "postal_code": "02601",
        "state": "MA",
        "country": "US"
      },
      "tags": [
        "contractor",
        "early-adopter"
      ],
      "custom_fields": {
        "referral_website": "http://www.example.com"
      }
    }
  }
});

// Create a Lead
await paragon.request("zendesksell", "/leads", {
    method: "POST",
    body: {
      "first_name": "Mark",
      "last_name": "Johnson",
      "organization_name": "Design Services Company",
      "source_id": 10,
      "title": "CEO",
      "description": "I know him via Tom",
      "industry": "Design Services",
      "website": "http://www.designservice.com",
      "email": "mark@designservices.com",
      "phone": "508-778-6516",
      "mobile": "508-778-6516",
      "fax": "+44-208-1234567",
      "twitter": "mjohnson",
      "facebook": "mjohnson",
      "linkedin": "mjohnson",
      "skype": "mjohnson",
      "address": {
        "line1": "2726 Smith Street",
        "city": "Hyannis",
        "postal_code": "02601",
        "state": "MA",
        "country": "US"
      },
      "tags": [
        "important"
      ],
      "custom_fields": {
        "known_via": "tom"
      }
    }
  });

// Get all Deals
await paragon.request("zendesksell", "/deals", {
   method: "GET"
})
```

## Building Zendesk Sell workflows

Once your Zendesk Sell account is connected, you can add steps to perform the following actions:

* Create Record
* Update Record
* Get Record by ID
* Search Records
* Delete Records

You can also use the Zendesk Sell Request step to access any of Zendesk Sell's API endpoints without the authentication piece.

When creating or updating records in Zendesk Sell, you can reference data from previous steps by typing `{{` to invoke the variable menu.
