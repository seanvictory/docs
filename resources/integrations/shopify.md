---
description: Connect your Shopify app for OAuth in Paragon
---

# Shopify

You can find your Shopify application credentials by visiting your [Shopify Partner Dashboard](https://partners.shopify.com/organizations).

You'll need the following information to set up your Shopify App with Paragon:

* Client ID
* Client Secret
* Scopes Requested
* Shopify Developer account, also known as a Shopify Partner account. You can create one [here](https://developers.shopify.com/).
* Shopify development store. Learn more about creating a development store [here](https://help.shopify.com/en/partners/dashboard/managing-stores/development-stores#create-a-development-store-for-testing-apps-or-themes).
* Shopify application. Learn more about creating a Shopify application [here](https://shopify.dev/tutorials/authenticate-a-public-app-with-oauth#generate-credentials-from-your-partner-dashboard).&#x20;

### Add the Redirect URL to your Shopify app

Paragon provides a redirect URL to send information to your Shopify app. To add the redirect URL to your Shopify app:

1. Log in to your Shopify [Partner Dashboard](https://partners.shopify.com/current/resources) and select your app.
2. Navigate to **App setup > URLs > Allowed redirection URL(s)**
3. Add your app's Initial Redirect URL to "**App URL**".\
   While testing your integration, you can use your app's root URL. Once you [set up an Initial Redirect](shopify.md#initial-redirect) to go live, you will need to change this to the URL of your Initial Redirect.
4. Add your app's Redirect Callback URL to "**Allowed redirection URL(s)**".\
   While testing your integration, you can use `https://passport.useparagon.com/oauth`. Once you [set up a Redirect Callback](shopify.md#setting-up-redirect-pages-in-your-app) to go live, you will need to change this to the URL of your Redirect Callback.
5. Press the **Save** button at the top of the page to save your changes.

{% hint style="info" %}
**Note:** You'll need a Shopify application to connect your application to Paragon. Learn more about creating a Shopify application [here](https://shopify.dev/tutorials/authenticate-a-public-app-with-oauth#generate-credentials-from-your-partner-dashboard).&#x20;
{% endhint %}

![](<../../.gitbook/assets/Enabling OAuth for your Shopify app.gif>)

### Add a development store to your Shopify app

1\. Log in to your Shopify [Partner Dashboard](https://partners.shopify.com/current/resources).

2\. Click **Apps** on the sidebar.

3\. Select your Shopify application.

4\. In the **Test your app** section, press the **Select store** button.

5\. Choose the development store you'd like to connect to.

{% hint style="info" %}
**Note:** You'll need to create a development store if you don't already have one. Learn more about creating a Shopify development store [here](https://help.shopify.com/en/partners/dashboard/managing-stores/development-stores#create-a-development-store-for-testing-apps-or-themes).
{% endhint %}

### Add your Shopify app to Paragon

1\. Select **Shopify** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](shopify.md#1-add-the-redirect-url-to-your-shopify-app) in their respective sections:

* **Client ID:** Found under Apps > Client credentials > Client ID on your Shopify app page.
* **Client Secret:** Found under Apps > Client credentials > Client Secret on your Shopify app page.
* **Permissions:** Select the scopes you've requested for your application. A complete list of Shopify's scopes is [here](https://shopify.dev/docs).

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** You should only add the scopes you've requested in your application page to Paragon.
{% endhint %}

<figure><img src="../../.gitbook/assets/CleanShot 2024-03-21 at 12.17.39@2x.png" alt=""><figcaption></figcaption></figure>

## Connecting to Shopify

Once your users have connected their Shopify account, you can use the Paragon SDK to access the Shopify API on behalf of connected users.

See the Shopify [REST API documentation](https://shopify.dev/docs/admin-api/rest/reference) for their full API reference.

Any Shopify API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Create Customer
await paragon.request("shopify", "/admin/api/2020-10/customers.json", { 
  method: "POST",
  body: { 
    "first_name": "John",
    "last_name": "Norman",
    "email": "example@example.com",
    "phone": "+16135551111",
    "note": "Creating customer for testing",
    "tags": ["tag1","tag2"]
   }
});


// Query Customers
await paragon.request("shopify", "/admin/api/2020-10/customers.json", { 
  method: "GET"
});
  
```

## Building Shopify workflows

Once your Shopify account is connected, you can add steps to perform the following actions:

* Get customers
* Search customers
* Create customer
* Update customer
* Get orders
* Create order
* Update order
* Get products
* Create product
* Update product

When creating or updating records in Shopify, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/A Shopify Workflow in Paragon.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Shopify account. For example, you might want to trigger a workflow whenever new orders are created Shopify to sync your users' Shopify orders to your application in real-time.

![](<../../.gitbook/assets/Shopify Webhook Triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Shopify below:

* **New Order**
* **Order Updated**
* **New Customer**
* **Customer Updated**
* **New Product**
* **Product Updated**

## Publishing your Shopify app

{% hint style="info" %}
**Required for publishing:** In order to list your app on the Shopify App Store, you must implement the following additional features in your integration:

* [Setting up Redirect Pages](shopify.md#setting-up-redirect-pages-in-your-app)
* [Subscribing to mandatory privacy webhooks](shopify.md#subscribing-to-mandatory-privacy-webhooks)

For more information, see [Shopify's documentation on publishing requirements](https://shopify.dev/docs/apps/store/requirements).
{% endhint %}

### Setting up Redirect Pages in your app

Your Shopify integration requires two types of pages hosted in your application to support an installation flow that _begins_ in the Shopify App Store (i.e., a user searches the Shopify App Store for your published app and clicks **Add app**).

Here is an annotated version of the [Shopify OAuth flow](https://shopify.dev/docs/apps/auth/oauth) diagram outlining what pages you will need to implement:

<figure><img src="../../.gitbook/assets/Shopify OAuth Flow (1).png" alt=""><figcaption></figcaption></figure>

The pages you will need to implement include:

* **Initial Redirect**: This page will take in a `shop` query parameter and redirect to Shopify's OAuth flow.
* **Redirect Callback**: This page will receive the OAuth authorization code after the Shopify user grants consent and call `paragon.completeInstall` to save the user's account connection.

For an example implementation of the redirect pages using React (based on our Next.js sample app), see:

* [Example Initial Redirect](https://github.com/ethanlee16/paragon-connect-nextjs-example/blob/redirect-page/pages/integrations/index.js#L13-L20)
* [Example Redirect Callback](https://github.com/ethanlee16/paragon-connect-nextjs-example/blob/redirect-page/pages/integrations/shopify.js)

#### Initial Redirect

The Initial Redirect should be implemented as follows:

* Accept and read the query parameter `shop`. If the query parameter is present, redirect to the following URL to start the Shopify OAuth flow:

{% code overflow="wrap" %}
```
https://{shopQueryParam}/admin/oauth/authorize?client_id={SHOPIFY_CLIENT_ID}&redirect_uri={REDIRECT_CALLBACK_URL}&scope={SHOPIFY_SCOPES}
```
{% endcode %}

* The `SHOPIFY_CLIENT_ID` should match the Client ID that you use in your Shopify integration settings.
* The `REDIRECT_CALLBACK_URL` should be the URL of the Redirect Callback page in your app.
* The `SHOPIFY_SCOPES` should match the scopes that you use in your Shopify integration settings.

#### Redirect Callback

The Redirect Callback should be implemented as follows:

* Import the Paragon SDK and authenticate a user.
  * **Note**: If a user is not yet logged into your app, you can redirect to a login form, while preserving the intended URL to redirect to upon successful login. In other words, after logging in, your user should see your Redirect Page.
* Accept and read query parameters, which will be:
  * `code` and `shop` in case of a successful installation
  * `error` in case of an unsuccessful installation or denied consent
* If the `code` query parameter is present,
  * Read the `shop` query parameter and capture the shop name in the pattern `{shop}.myshopify.com`. See the regular expression used below.
  * Call `paragon.completeInstall` to complete the OAuth exchange and save a new connected Shopify account.

```javascript
let params = new URLSearchParams(window.location.search);
let authorizationCode = params.get("code");
let [, shopName] = params.get("shop").match(/^([a-zA-Z0-9][a-zA-Z0-9\-]*)\.myshopify\.com/);

if (authorizationCode && shopName) {
   paragon.completeInstall("shopify", {
    authorizationCode: authorizationCode,
    redirectUrl: "https://your-app.url/shopify-redirect",
    integrationOptions: {
      SHOP_NAME: shopName,
    }
  }).then(() => {
     // Redirect to your app's integrations page
  });
} else {
  let error = params.get("error");
  // Handle error
}
```

* If the `error` query parameter is present,&#x20;
  * Show this error in your app and allow your user to retry the process.

#### Updating your app's redirect and app URLs

1. Log in to your Shopify [Partner Dashboard](https://partners.shopify.com/current/resources) and select your app.
2. Navigate to **App setup > URLs > Allowed redirection URL(s)**
3. Set your **App URL** to your app's Initial Redirect URL.
4. Add your app's Redirect Callback URL to **Allowed redirection URL(s).**

### Subscribing to mandatory privacy webhooks

Shopify requires you to subscribe to 3 privacy webhooks to request or erase personal data that your integration may store in your application.

Paragon's Shopify integration allows you to subscribe and take action on these webhooks via workflows.

#### Setting the Shopify Webhook URL

To get started, visit the Paragon dashboard and navigate to your Shopify integration.

* Click on the **Settings** tab and copy the **Webhook URL** value.

<figure><img src="../../.gitbook/assets/[CleanShot] 2024-02-01 at 11.09.29 AM.png" alt=""><figcaption></figcaption></figure>

Next, log in to [Shopify Partners](https://partners.shopify.com) and navigate to **Apps**.&#x20;

* Select the app that you are using in the environment or project you have opened in Paragon.
* Navigate to **Configuration** (under the Build section) and scroll to **Compliance Webhooks**.
* For each of the endpoints (Customer data request endpoint, Customer data erasure endpoint, Shop data erasure endpoint), paste in the Webhook URL value you copied from the Paragon dashboard.
* Click **Save and release** at the top to save your changes.

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

#### Creating workflows to respond to privacy webhooks

Next, create 3 workflows that listen for these triggers and take action on events received:

* Customer data request
* Customer data erasure
* Shop data erasure

You can create new workflows in the Paragon dashboard, from the **Overview** tab of your Shopify integration and click **Create Workflow**.

For each of the new workflows you create, select a **Shopify** trigger and select one of the Shopify privacy webhook events as the Trigger Event:

<figure><img src="../../.gitbook/assets/image (81).png" alt="" width="375"><figcaption></figcaption></figure>

Define the steps under the workflow to respond to the event type you selected.

From [Shopify's documentation](https://shopify.dev/docs/apps/webhooks/configuration/mandatory-webhooks), here is how you should handle each event type:

* **Customer data request**: If your app has been granted access to [customer or order data](https://shopify.dev/docs/api/usage/access-scopes#authenticated-access-scopes), then it will receive a data request webhook. The webhook contains the resource IDs of the customer data that you need to provide to the store owner. It's your responsibility to provide this data to the store owner directly.
  * **Note**: This request does not require the data to be provided in a response to the webhook. This process happens outside of Shopify and should be provided to the user who connected this Shopify account directly, e.g. through email, within 30 days of receiving the request.
* **Customer data erasure**: Shopify store owners can request that data is deleted on behalf of a customer. When this happens, Shopify sends a Customer Data Erasure event to the apps installed on that store so that you can erase any data for a certain customer of a store from your database.
* **Shop data erasure**: 48 hours after a store owner uninstalls your app, Shopify sends a Shop Data Erasure event. This webhook provides the store's `shop_id` and `shop_domain` so that you can erase data for that store from your database.

<details>

<summary>Example implementation</summary>

Add a Request step under the Trigger to send the privacy event information to your API. We recommend including the following values in the request body for your reference:

* `{{1.result}}`:  This is the full event payload received from Shopify. You will see an example of the event in your workflow Test Data. See [Shopify's documentation on event payloads](https://shopify.dev/docs/apps/webhooks/configuration/mandatory-webhooks#customers-data\_request) for more details.
* `{{userSettings.userId}}`: This is the User ID of the Connected User that received the event. You can use this ID to relate the event to a user in your application.

<img src="../../.gitbook/assets/image (82).png" alt="" data-size="original">

</details>

Finally, configure your 3 workflows to be [hidden from the Connect Portal and enabled by default](../../connect-portal/connect-portal-customization.md#workflows):

* Click the context menu in the Workflow Editor toolbar (![](<../../.gitbook/assets/Workflow Editor three dot menu (1).png>)) and click **Edit Connect Portal Workflow Settings**.
* Switch on **Default to enabled** and **Hide workflow from Portal for all users**.

<figure><img src="../../.gitbook/assets/Default Enabled  Hide Workflow On.png" alt="" width="563"><figcaption></figcaption></figure>

* Repeat for each workflow that has a Shopify privacy event trigger.

Having both options on will mean that this workflow will run for all users of your Shopify integration, and users will not see or need to configure the workflow from your Connect Portal.

#### Testing and validating privacy webhooks

To test your privacy webhook implementation end-to-end:

* Verify that each of your workflows are [deployed](../../workflows/building-workflows.md#deploying-workflows).
* In your application, connect a Shopify store to the Connect Portal. Remember the store and account that you have connected.
* In the [Shopify Admin](https://admin.shopify.com) page for the same store, request or erase a customer's data ([see Shopify documentation](https://help.shopify.com/en/manual/privacy-and-security/privacy/processing-customer-data-requests)). These actions will trigger the "Customer data request" and "Customer data erasure" events, respectively.
* In the Paragon dashboard, visit [Task History](../../monitoring/viewing-task-history.md) and verify that your workflow has executed.
