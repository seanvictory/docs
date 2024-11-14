---
description: Create your own custom integration with any app provider on Paragon.
---

# Custom Integrations

## Overview

{% hint style="success" %}
✨ Custom Integrations are included in all **paid plans**. [**Contact us**](https://calendly.com/useparagon/paragon-demo) to schedule a demo of Custom Integrations or upgrade your account.
{% endhint %}

Custom Integrations allow you to build your own custom integration with any app provider on Paragon, even if it's not natively supported by our integration catalog.

Similar to natively supported integration on Paragon, Custom Integrations provide the following features:

* **Embedded Connect Portal** for your customers to activate and configure the integration in your app.
* **Fully managed authentication** with OAuth 2.0 or API Keys.
* **Visual workflow editor** for creating custom integration logic.
* **Access to any API methods** provided by the application's API.

## Building a Custom Integration

The general prerequisites for building a Custom Integration with any app provider on Paragon are:

* The app provider must have a public API.
* Have access to the app provider's API documentation.
* If the app provider uses OAuth authentication, create a developer account and developer application from the app provider.
* A Paragon account with a **paid plan**.

To start building a Custom Integration, click the **build your own custom integration** button at the top of your integration catalog in Paragon. You'll need to complete the following steps:

### Step 1. Basic Info

You'll first need to provide some basic information about the app provider that will appear in the Connect Portal for the integration.

* **Name** - A short name for the app provider.
* **Description** - A short description for what the app provider does.
* **App Icon** - Only SVG formats accepted.
* **Accent Color** -  The brand color that will be used in the accents of the Connect Portal for this integration.

![](<../.gitbook/assets/Basic info for custom integrations on Paragon.png>)

### Step 2. Authentication Method

Select a method of authentication for your app provider. You can usually find this in your app provider's API documentation.

**OAuth 2.0** is typically used when a user needs to authenticate access to their account. For example, a user signing into Salesforce so that your application can make changes on their behalf.

Some app providers use **API keys** for authorization. An API key is a token that a client provides when making API calls. API keys are typically found within the app provider's account settings.

![](<../.gitbook/assets/Choosing an authentication method for a custom integration on Paragon.png>)

### Step 3. Authentication Setup

#### OAuth 2.0

Specify the sign-in URL, also known as the **Authorization URL**, that this integration uses to begin the OAuth 2.0 authentication flow. If the URL includes a value that must be supplied by your end-user, use the **Advanced Options** to add input fields.

You can usually find the OAuth credentials for your selected provider in their API Documentation. You'll need access to the following credentials:

* Auth URL
* Access Token URL
* Client ID
* Client Secret
* Scopes Requested

<figure><img src="../.gitbook/assets/Setting up the OAuth flow for a custom integration in Paragon Connect-1.png" alt=""><figcaption></figcaption></figure>

#### API Keys

You can add **Input Fields** for API keys or user details that are required to authenticate with your selected app provider.

<figure><img src="../.gitbook/assets/Setting up the API Key flow for a custom integration in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

#### OAuth Client Credentials

Specify the URL that this integration uses to exchange an authorization code for access tokens, also known as the **Access Token URL**. The Paragon Connect Portal prompt your user for their Client ID and Client Secret needed to validate the authentication.&#x20;

![](<../.gitbook/assets/Using Client OAuth Credentials when creating integrations in Paragon Connect.png>)

Once you've added your authentication method, press the `Enable` button inside the Connect Portal preview to validate the connection. You must successfully enable your integration before moving to the next step.

### Step 4. API Setup

You can also access your custom provider through the **Workflow Builder** or **Paragon SDK.**&#x20;

* **API Base URL** - Specify the base URL for API requests made to this integration.
* **API Authorization** - Specify how API requests get authenticated for this integration.
* **Test Endpoint URL** - Specify a request URL that can be used to test that your user’s account credentials are valid. This endpoint must be reachable via a `GET` request.

![](<../.gitbook/assets/API Setup for custom integrations on Paragon Connect.png>)

Once you've added the fields above, you can press the `Send test request` button to validate your custom integration configuration. Press the `Finish` button to save your custom integration.

## Using Custom Integrations

Once you've added a custom integration to Paragon, you can access it through the Workflow Builder or Paragon SDK.

### Workflow Builder

You can make API Requests to your app provider from the Workflow Builder by selecting your app provider from the workflow sidebar. Paragon prefills the request URL with the API Base URL from [**Step 4**](custom-integrations.md#step-4-api-setup). Just provide the API endpoint to the request that you want to make. Since you built your integration on Paragon Connect, there is no need to include any `Authorization` information in the request.

Learn more about using the Workflow Builder below:

{% content-ref url="../workflows/building-workflows.md" %}
[building-workflows.md](../workflows/building-workflows.md)
{% endcontent-ref %}

{% content-ref url="../workflows/requests/" %}
[requests](../workflows/requests/)
{% endcontent-ref %}

### Paragon SDK

Once your users have connected their accounts, you can use the Paragon SDK to access any of your app provider's endpoints on behalf of connected users. You'll need to prefix the app provider's name with `custom.` when making requests. For example, a custom GitHub integration would be referenced as `custom.github`.

{% hint style="info" %}
**Note:** When using custom app providers in the Paragon SDK, prefix the app provider name with **`custom.`**.
{% endhint %}

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get Data 
await paragon.request("custom.<app_provider_name>", "<api_endpoint>", {
  method: "GET",
})

```
{% endtab %}
{% endtabs %}

**Example:**

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>)

// Create new Issue
await paragon.request("custom.onesignal", "/notifications", {
    method: "POST",
    body: { 
    "title": "This notification was created from your app"
    }
})
```
{% endtab %}
{% endtabs %}

### **Connect API**

{% hint style="info" %}
See full Connect API documentation here: [making-api-requests.md](../api/making-api-requests.md "mention")
{% endhint %}

If you'd like to issue a request from your server to your custom integration on behalf of an end-user, you can make the request to:

{% tabs %}
{% tab title="REST API" %}
```http
https://proxy.useparagon.com/projects/<Paragon Project ID>/sdk/proxy
  /custom/<Integration ID>/<API path>

Authorization: Bearer <Paragon User Token>
```
{% endtab %}
{% endtabs %}

* A Bearer token must also be specified with a Paragon User Token.
* This endpoint accepts any HTTP verb you want to use with the API.
* The Integration ID can be found in the dashboard (`/.../integrations/<Integration ID>`) or with the [#get-projects-integrations](../api/api-reference/#get-projects-integrations "mention") API endpoint.

**Example:**

{% tabs %}
{% tab title="REST API" %}
```http
POST https://proxy.useparagon.com/projects/19d...012/sdk/proxy
    /fb243b75-35e7-46b3-ba6c-967ccebeb449/notifications

Authorization: Bearer eyJ...
Content-Type: application/json

{ 
    "title": "This notification was created from your app"
}
```
{% endtab %}
{% endtabs %}
