# Pipedrive

## Setup Guide

{% hint style="info" %}
**Note:** You'll need to create a new Pipedrive app if you don't already have one.
{% endhint %}

You can find your Pipedrive app credentials by visiting your [Pipedrive Developer Portal](https://developers.pipedrive.com/).

You'll need the following information to set up your Pipedrive app with Paragon:

* Client ID
* Client Secret

### Add the Redirect URL to your Pipedrive app

Paragon provides a redirect URL to send information to your Pipedrive app. To add the redirect URL to your ServiceNow app:

1. Log into your Pipedrive [Developer Portal](https://developers.pipedrive.com/).
2. Navigate to **Tools > Marketplace manager** and select your application. You can press the green **Create new app** button if you don't already have one.
3.  Under **OAuth & Access scopes > Callback URL**, provide the URL of your Redirect Page.

    While testing your integration, you can use `https://passport.useparagon.com/oauth`. Once you [set up a Redirect Page](pipedrive.md#setting-up-a-redirect-page-in-your-app) to go live, you will need to change this to the URL of your Redirect Page.

{% hint style="info" %}
Pipedrive provides you with the **Client ID** and **Client Secret** needed for the next steps after adding the redirect URL to your project.
{% endhint %}

### Add your Pipedrive app to Paragon

1\. Select Pipedrive from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations >** _**{YOUR\_APP}**_ **>** **Settings**, fill out your credentials from the end of [Step 1](asana.md#add-the-redirect-url-to-your-asana-app) in their respective sections:

* **Client ID:**
  * Log in to the [Pipedrive Developer Portal](https://developers.pipedrive.com/).
  * Navigate to **Tools > Marketplace manager** and select your application.
  * Under **OAuth & Access scopes**, copy the **Client ID**.
* **Client Secret:**
  * Log in to the [Pipedrive Developer Portal](https://developers.pipedrive.com/).
  * Navigate to **Tools > Marketplace manager** and select your application.
  * Under **OAuth & Access scopes**, copy the **Client Secret**.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connecting your Pipedrive application to Paragon Connect.png>)

## Connecting to Pipedrive

Once your users have connected their Pipedrive account, you can use the Paragon SDK to access the Pipedrive API on behalf of connected users.

See the Pipedrive REST API documentation for their full API reference.

Any Pipedrive API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get all persons
await paragon.request("pipedrive", "/persons", {
  method: "GET",
});
            
// Create a person
await paragon.request("pipedrive", "/persons", {
  method: "POST",
  body: {
    "name": "David Bowie",
    "email": "name@domain.com"
  }
});
```

## Building Pipedrive workflows

Once your Pipedrive account is connected, you can add steps to perform the following actions:

* Create Record
* Update Record
* Get Record by ID
* Get Records
* Delete Record

When creating or updating records in Pipedrive, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating a Pipedrive workflow in Paragon Connect.png>)

## Using Pipedrive triggers

To use Pipedrive's webhook triggers, you'll need to enable the "Administer account" scope in your Pipedrive application:

1. Log in to the [Pipedrive Developer Portal](https://developers.pipedrive.com/).
2. Navigate to **Tools > Marketplace manager** and select your application.
3. Under **OAuth & Access scopes**, enable **Administer account**.

## Publishing your Pipedrive app

{% hint style="warning" %}
**Required:** Setting up a Redirect Page is a requirement for allowing customers outside of your Pipedrive Developer account to connect an integration.

If you do not set up this page, the Pipedrive team will not approve your app for public use.
{% endhint %}

### Setting up a Redirect Page in your app

Your Pipedrive integration requires a Redirect Page hosted in your application to support an installation flow that _begins_ in the Pipedrive Marketplace (i.e., a user searches the Pipedrive Marketplace for your published app and clicks **Install**).

For an example implementation of the Redirect Page using React (based on our Next.js sample app), [see here](https://github.com/ethanlee16/paragon-connect-nextjs-example/blob/redirect-page/pages/integrations/pipedrive.js).

The Redirect Page should be implemented as follows:

* Import the Paragon SDK and authenticate a user.
  * **Note**: If a user is not yet logged into your app, [Pipedrive's requirements](https://pipedrive.readme.io/docs/app-installation-flows#the-user-isnt-logged-into-your-app) suggest that you redirect to a login form, while preserving the intended URL to redirect to upon successful login. In other words, after logging in, your user should see your Redirect Page.
* Accept and read query parameters, which will be:
  * `code` in case of a successful installation
  * `error` in case of an unsuccessful installation or denied consent
* If the `code` query parameter is present,
  * Call `paragon.completeInstall` to complete the OAuth exchange and save a new connected Pipedrive account.

```javascript
 paragon.completeInstall("pipedrive", {
  authorizationCode: codeQueryParam,
  redirectUrl: "https://your-app.url/pipedrive-redirect"
 }).then(() => {
   // Redirect to your app's integrations page
 });
```

* If the `error` query parameter is present,&#x20;
  * Show this error in your app and allow your user to retry the process.

### Updating the allowed Redirect URL

If you were previously testing with `https://passport.useparagon.com/oauth` as your Pipedrive Redirect URL, you will need to update this value after implementing a Redirect Page:

1. Log into your Pipedrive [Developer Portal](https://developers.pipedrive.com/).
2. Navigate to **Tools > Marketplace manager** and select your application.
3. Under **OAuth & Access scopes > Callback URL**, provide the URL of your Redirect Page.
