# Productboard

## Setup Guide

You can find your Productboard app credentials in your [Productboard Integration Settings](https://paragon-sandbox.productboard.com/settings/integrations).

{% hint style="info" %}
**Note:** Productboard API access is restricted to Productboard Pro plans and above. Your users will need to have Productboard Pro plans or above to use this integration.
{% endhint %}

{% hint style="info" %}
This is an **API-only** integration - workflow actions for this integration are still in development. You can still connect user accounts, build workflows, and access the API for this integration.
{% endhint %}

### Getting your Productboard API Key

1\. Login to your Productboard account

2\. Navigate to **Workspace Settings** > **Integrations** > **Public API** > **Access Token**

3\. Click **+** to generate a new token.

## Connecting to Productboard

Once your users have connected their Productboard account, you can use the Paragon SDK to access the Productboard API on behalf of connected users.

See the Productboard [REST API documentation](https://developer.productboard.com/) for their full API reference.

Any Productboard API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get a Feature by ID
paragon.request("productboard", "/features/{id}", {
  method: "GET"
});

// Update a Feature
paragon.request("productboard", "/features/{id}", {
  method: "PATCH",
  body: {
    "data": {
      "name": "Custom branding",
      "description": "<p>Custom <s>branding</s> for the agent and user portals.</p>",
      "archived": true,
      "status": {
        "id": "00000000-0000-0000-0000-000000000000",
        "name": "In Progress"
      },
      "timeframe": {
        "startDate": "2022-01-01",
        "endDate": "2022-03-31",
        "granularity": "quarter"
      },
      "parent": {
        "feature": {
          "id": "00000000-0000-0000-0000-000000000000"
        }
      },
      "owner": {
        "email": "email@example.com"
      }
    }
  }
});

// Create a new Release
paragon.request("productboard", "/releases", {
  method: "POST",
  body: {
    "data": {
      "name": "R123",
      "description": "<p>Release <s>R123</s></p>",
      "releaseGroup": {
        "id": "00000000-0000-0000-0000-000000000000"
      },
      "timeframe": {
        "startDate": "2023-01-01",
        "endDate": "2023-03-31",
        "granularity": "quarter"
      },
      "state": "upcoming"
    }
  }
});
  
```

## Building Productboard workflows

Once your Productboard account is connected, you use the Productboard Request step to access any of Productboard's API endpoints without the authentication piece.

When creating or updating records in Productboard, you can reference data from previous steps by typing `{{` to invoke the variable menu.
