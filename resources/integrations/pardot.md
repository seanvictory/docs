---
description: Connect your Pardot app for OAuth in Paragon.
---

# Pardot

## Setup Guide

You can find your Salesforce app credentials in your [Salesforce Developer Account.](https://developer.salesforce.com/)

You'll need the following information to set up your Salesforce App with Paragon Connect:

* Consumer Key
* Consumer Secret
* Scopes Requested

### Add the Redirect URL to your Pardot app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Salesforce app:

1\. Log in to your [Salesforce dashboard](https://www.salesforce.com/).

2\. Navigate to the gear icon at the top of the page and click **Setup.**

![](<../../.gitbook/assets/Going to Setup in Salesforce.gif>)

3\. In the left-hand sidebar, go to **Platform Tools > Apps > App Manager**.

{% hint style="info" %}
**Note:** You must have the proper admin permissions on your Salesforce account to access the App Manager. If you don't, please speak to your admin.
{% endhint %}

![](<../../.gitbook/assets/Platform tools to Apps to App Manager in Salesforce.gif>)

4\. Click on the registered application you'd like to use. If you don't already have one, click **New Connected App**.

5\. Under **API (Enable OAuth Settings)**, mark the "**Enable OAuth Settings**" checkbox.

6\. Under **Callback URL**, paste-in Paragon Connect's redirect URL:

```
https://passport.useparagon.com/oauth
```

7\. Select any scopes you'd like to use in your application.

8\. Press the **Save** button at the bottom of the page.

Salesforce provides your **Consumer Key** and **Consumer Secret** needed for the next step once you register your application.&#x20;

![](<../../.gitbook/assets/Adding OAuth Scopes to Salesforce.gif>)

### Add your Pardot app to Paragon

Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](salesforce.md#1-add-the-redirect-url-to-your-salesforce-app) in their respective sections:

* **Consumer Key:** Found under Manage Connected Apps > API (Enable OAuth Settings) > Consumer Key on your Salesforce App page.
* **Consumer Secret:** Found under Manage Connected Apps > API (Enable OAuth Settings) > Consumer Secret on your Salesforce App page.
* **Permissions:** Select the scopes you've requested for your application.

{% hint style="info" %}
**Note:** Leaving the Client ID and Client Secret blank will use Paragon development keys.
{% endhint %}

![](<../../.gitbook/assets/Connectng your Salesforce app to Paragon Connect.png>)

## Connecting to Pardot

Once your users have connected their Pardot account, you can use the Paragon SDK to access the Pardot API on behalf of connected users.

See the Pardot [REST API documentation](https://developer.salesforce.com/docs/) for their full API reference.

Any Pardot API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
          
// Get Prospects
await paragon.request("pardot", "/api/prospect/version/4/do/query/?format=json", {
  method:"GET",
});


// Create a new Prospect
await paragon.request("pardot", "/api/prospect/version/4/do/create?format=json", {
  method: "POST",
  body: "email=b%40useparagon.com&first_name=Brandon&last_name=Foo",
  headers:{
    'Content-Type': 'application/x-www-form-urlencoded',
  }
});
  
```

## Building Pardot workflows

Once your Pardot account is connected, you can add steps to perform the following actions:

* Create or Update Prospect
* Search Prospects
* Get Prospect by ID
* Delete Prospect by ID
* Add Prospect to List
* Remove Prospect from List

When creating or updating prospects in Pardot, you can reference data from previous steps by typing `{{` to invoke the variable menu.



## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Pardot account. For example, you might want to trigger a workflow whenever new contacts are created Pardot to sync your users' Pardot contacts to your application in real-time.

![](<../../.gitbook/assets/Salesforce Pardot triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Pardot below:

* **Prospect Created**
* **List Membership Created**
