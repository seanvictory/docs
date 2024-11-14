---
description: Use the SDK to connect multiple accounts for the same integration.
---

# Multiple Account Authorizations

Multiple Account Authorizations is a set of SDK options that enables you to connect multiple accounts for the same integration type for a user.

For example, one Connected User can connect a Google Calendar integration for both their Google Workspace account and personal Gmail account.

## Usage

A subset of SDK functions can be passed an additional parameter for Multiple Account Authorizations, as outlined below.

In general, to use Multiple Account Authorizations, you will need to:

* Use `user.integrations.[integration].allCredentials` (a field returned in [`getUser`](multiple-account-authorizations.md#.getuser-greater-than-paragonuser)) to display multiple connected accounts in your Integrations UI.
* Update references to [`connect`](./#connect-integrationtype-string-installoptions-installoptions) (or [`installIntegration`](multiple-account-authorizations.md#installintegration) and [`uninstallIntegration`](multiple-account-authorizations.md#.workflow)) to use the SDK with Multiple Account Authorizations enabled.
* Update references to [`paragon.request`](multiple-account-authorizations.md#.request-integrationtype-string-path-string-requestoptions-requestoptions-promise) and [`paragon.workflow`](multiple-account-authorizations.md#.workflow-1) (and API equivalents) to make sure that a specific account is targeted for a given integration type.

App Events and Workflows do not need to be updated to support Multiple Account Authorizations.

## Reference

### .getUser() -> ParagonUser

Call `.getUser` to retrieve the currently authenticated user and their connected integration state.

With Multiple Account Authorizations, the `getUser()` method additionally returns `allCredentials`, an array of connected accounts for a given integration.

{% tabs %}
{% tab title="JavaScript SDK" %}
<pre class="language-javascript" data-full-width="true"><code class="lang-javascript">paragon.getUser();

{
  authenticated: true,
  userId: "xyz", // The user ID you specified in the signed JWT
  integrations: {
    salesforce: {
      enabled: true,
<strong>      allCredentials: [
</strong><strong>        {
</strong><strong>          id: "a5e995c2-7709-43fd-9cdf-f759faa52497",
</strong><strong>          dateCreated: "2023-05-30T22:33:20.349Z",
</strong><strong>          dateUpdated: "2023-05-30T22:33:20.349Z",
</strong><strong>          projectId: "d1f142cd-1dfe-4d76-ab4c-8f64901a9c5c",
</strong><strong>          integrationId: "8aaad9ff-5adb-433c-a17b-da093f9d4528",
</strong><strong>          personaId: "30975f6a-c50c-4e74-914a-3eb700db8b05",
</strong><strong>          config: { configuredWorkflows: { ... } },
</strong><strong>          isPreviewCredential: false,
</strong><strong>          providerId: "1223115691",
</strong><strong>          providerData: {},
</strong><strong>          status: "VALID",
</strong><strong>          dateRefreshed: "2023-05-30T22:33:20.349Z",
</strong><strong>          dateValidUntil: "2023-05-30T23:33:17.809Z",
</strong><strong>          refreshFailureCount: 0,
</strong><strong>          isRefreshing: false,
</strong><strong>        },
</strong><strong>      ],
</strong>      configuredWorkflows: {},
      credentialId: "a5e995c2-7709-43fd-9cdf-f759faa52497",
      credentialStatus: "VALID",
      providerId: "1223115691",
      providerData: {},
    },
    shopify: {
      enabled: false,
    },
  },
};
</code></pre>
{% endtab %}

{% tab title="REST API" %}
```
GET https://api.useparagon.com/projects/<Paragon Project ID>/sdk/me

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

{
  authenticated: true,
  userId: "xyz", // The user ID you specified in the signed JWT
  integrations: {
    salesforce: {
      enabled: true,
      allCredentials: [
        {
          id: "a5e995c2-7709-43fd-9cdf-f759faa52497",
          dateCreated: "2023-05-30T22:33:20.349Z",
          dateUpdated: "2023-05-30T22:33:20.349Z",
          projectId: "d1f142cd-1dfe-4d76-ab4c-8f64901a9c5c",
          integrationId: "8aaad9ff-5adb-433c-a17b-da093f9d4528",
          personaId: "30975f6a-c50c-4e74-914a-3eb700db8b05",
          config: { configuredWorkflows: {} },
          isPreviewCredential: false,
          providerId: "1223115691",
          providerData: {},
          status: "VALID",
          dateRefreshed: "2023-05-30T22:33:20.349Z",
          dateValidUntil: "2023-05-30T23:33:17.809Z",
          refreshFailureCount: 0,
          isRefreshing: false,
        }
      ],
      configuredWorkflows: {},
      credentialId: "a5e995c2-7709-43fd-9cdf-f759faa52497",
      credentialStatus: "VALID",
      providerId: "1223115691",
      providerData: {},
    },
    shopify: {
      enabled: false,
    }
  }
}
```
{% endtab %}
{% endtabs %}

### .installIntegration(integrationType: string, options?: IntegrationInstallOptions) -> Promise <a href="#installintegration" id="installintegration"></a>

* **Full docs**: [#installintegration](./#installintegration "mention")
* **Additional options**: If `allowMultipleCredentials` is specified as `true` in the `options` object, this function will not throw an error if the user already has this integration installed.

{% tabs %}
{% tab title="JavaScript SDK" %}
<pre class="language-javascript"><code class="lang-javascript">paragon.installIntegration("googledrive", {
<strong>    allowMultipleCredentials: true
</strong>});
</code></pre>
{% endtab %}
{% endtabs %}

**Replacing an account**

You can replace one of your user's existing connected accounts with the `selectedCredentialId` property. This option replaces the underlying connected account, keeping their enabled workflows and settings intact.

{% tabs %}
{% tab title="JavaScript SDK" %}
<pre class="language-javascript"><code class="lang-javascript">paragon.installIntegration("googledrive", {
<strong>    allowMultipleCredentials: true,
</strong><strong>    selectedCredentialId: "0d2cca60-268b-45f1-ac5e-af6aad403d8c"
</strong>});
</code></pre>
{% endtab %}
{% endtabs %}

### .uninstallIntegration(integrationType: string, options?: IntegrationUninstallOptions) -> Promise <a href="#workflow" id="workflow"></a>

Call `.uninstallIntegration()` to disconnect an integration for the authenticated user.

* **Full docs**: [#.workflow](./#.workflow "mention")
* **Additional options:** `selectedCredentialId` (SDK) or `X-Paragon-Credential` (API) can be used to select a specific account to uninstall.

{% tabs %}
{% tab title="JavaScript SDK" %}
<pre class="language-javascript"><code class="lang-javascript">paragon.uninstallIntegration("googledrive", {
<strong>    selectedCredentialId: "de06dea8-8680-483c-95ea-cfcf66582c96"
</strong>});
</code></pre>
{% endtab %}

{% tab title="REST API" %}
**Request**

<pre><code>DELETE https://api.useparagon.com/projects/&#x3C;Project ID>/sdk/integrations/&#x3C;Integration ID>

Authorization: Bearer &#x3C;Paragon User Token>
<strong>X-Paragon-Credential: de06dea8-8680-483c-95ea-cfcf66582c96
</strong></code></pre>
{% endtab %}
{% endtabs %}

### .connect(integrationType: string, options: IntegrationInstallOptions) -> Promise

With Multiple Account Authorizations, use `.connect` to present the Connect Portal for an _existing_ account for the intended integration. [`.installIntegration`](multiple-account-authorizations.md#installintegration) is used to connect _new_ accounts.

* The Connect Portal can show the settings and workflows enabled for one account at a time, set by the `selectedCredentialId` property. If `selectedCredentialId` is not defined, the Connect Portal will use the first account available.
* When the Connect Portal appears, a user can enable or disable workflows, update User Settings, and disconnect the account that is selected.

{% tabs %}
{% tab title="JavaScript SDK" %}
<pre class="language-typescript"><code class="lang-typescript">// Connect a new account for this integration.
// NOTE: You must use `.installIntegration` rather than `.connect`.
<strong>paragon.installIntegration("salesforce", {
</strong><strong>    allowMultipleCredentials: true
</strong>})

// Show the Connect Portal to configure an existing account for this integration.
paragon.connect("salesforce", {
<strong>    selectedCredentialId: "de06dea8-8680-483c-95ea-cfcf66582c96"
</strong>});
</code></pre>
{% endtab %}
{% endtabs %}

### .request(integrationType: string, path: string, requestOptions: RequestOptions) → Promise

Call `.request` to send an API request to a third-party integration on behalf of one of your users.

* **Full docs**: [#.request-integrationtype-string-path-string-requestoptions-requestinit-promise](./#.request-integrationtype-string-path-string-requestoptions-requestinit-promise "mention")
* **Additional options:** `selectedCredentialId` (SDK) or `X-Paragon-Credential` (API) can be used to select a specific account to use with the [Proxy API](../making-api-requests.md).

{% tabs %}
{% tab title="JavaScript SDK" %}
<pre class="language-javascript"><code class="lang-javascript">await paragon.request('slack', '/chat.postMessage', {
	method: 'POST',
	body: {
		channel: 'CXXXXXXX0' // Channel ID,
		text: 'This message was sent with Paragon Connect :exploding_head:'
	},
<strong>	selectedCredentialId: "de06dea8-8680-483c-95ea-cfcf66582c96"
</strong>});
</code></pre>
{% endtab %}

{% tab title="REST API" %}
<pre><code>POST https://proxy.useparagon.com/projects/&#x3C;Paragon Project ID>/sdk/proxy/slack/chat.postMessage

Authorization: Bearer &#x3C;Paragon User Token>
Content-Type: application/json
<strong>X-Paragon-Credential: de06dea8-8680-483c-95ea-cfcf66582c96
</strong>
{ 
    "channel": "CXXXXXXX0", 
    "text": "This message was sent with Paragon Connect :exploding_head:" 
}
</code></pre>
{% endtab %}
{% endtabs %}

### .workflow(workflowId: string, **options: FetchOptions)** <a href="#workflow" id="workflow"></a>

Call `.workflow()` to trigger a Paragon workflow that sends a custom response back to your app. Note: The workflow must be enabled and use a Request-type trigger.

* **Full docs**: [#.workflow-1](./#.workflow-1 "mention")
* **Additional options:** `selectedCredentialId` (SDK) or `X-Paragon-Credential` (API) can be used to select a specific account to trigger a workflow for. The Credential ID that is used will be recorded for viewing in [Task History](../../monitoring/viewing-task-history.md).

{% tabs %}
{% tab title="JavaScript SDK" %}
<pre class="language-javascript"><code class="lang-javascript">// Trigger the "Lead Created" workflow
await paragon.workflow("&#x3C;workflow_id>", {
  body: {
    "email": "bowie@useparagon.com",
    "first_name": "Bowie",
    "last_name": "Foo"
  },
<strong>  selectedCredentialId: "de06dea8-8680-483c-95ea-cfcf66582c96"
</strong>});
  
</code></pre>
{% endtab %}

{% tab title="REST API" %}
<pre><code>// Trigger the "Lead Created" Workflow
POST https://api.useparagon.com/projects/&#x3C;Paragon Project ID>/sdk/triggers/&#x3C;Workflow ID>

Authorization: Bearer &#x3C;Paragon User Token>
Content-Type: application/json
<strong>X-Paragon-Credential: de06dea8-8680-483c-95ea-cfcf66582c96
</strong>
{
  "email": "bowie@useparagon.com",
  "first_name": "Bowie",
  "last_name": "Foo
}
</code></pre>
{% endtab %}
{% endtabs %}

