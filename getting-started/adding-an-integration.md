# Adding Integrations

### Choose an Integration

In your Paragon Connect dashboard, click on **Catalog** in the sidebar menu and select the integration provider you want to add.

To add an integration to your dashboard, select the integration and click "Connect".

<figure><img src="../.gitbook/assets/Adding an Integration from the Integration Catalog in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

### Create a developer app&#x20;

Once you add an integration from our [Integration Catalog](../resources/integrations/), you'll need to register a developer app with the integration provider.

When you create your developer app, you'll receive app credentials - usually a Client ID and Secret - that you'll enter in your Paragon dashboard in the next step.

You'll need to specify a redirect URL (sometimes called "callback URL") when configuring your developer app for an integration provider. Here, you should provide Paragon's redirect URL:

```
https://passport.useparagon.com/oauth
```

{% hint style="info" %}
You can find provider-specific instructions for setting up a developer app and connecting it to Paragon in the [**Integration Providers section**](../resources/integrations/) of our docs.
{% endhint %}

### Connect your developer app to Paragon

Select your integration from the Paragon dashboard. From here, click on Integration Settings and enter your developer app's credentials - usually a Client ID and Secret.&#x20;

{% hint style="info" %}
You can add an integration using Paragon's development keys by leaving the app credentials blank. This should only be used for testing, and you should add your own app credentials for use in production.
{% endhint %}

Once you've added your developer app's credentials, press the blue "Save Changes" button to save your updates.

<figure><img src="../.gitbook/assets/Adding developer credentials to a Salesforce application in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

### Configuring Permissions

Once you add integration credentials, you can define which permission scopes will be requested from your users under Integration Settings. You'll usually need to make sure the same scopes are defined when configuring your developer app from the third-party app provider.

<figure><img src="../.gitbook/assets/Configuring Permission Scopes to a Salesforce Integration in Paragon Connect.png" alt=""><figcaption></figcaption></figure>
