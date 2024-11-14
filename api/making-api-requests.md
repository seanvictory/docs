# Connect API

## Introduction

Once your users have connected their third-party app accounts in the Connect Portal, you can access their app account via the Connect API.&#x20;

The Connect API acts as a proxy to the third-party app provider's API, meaning that any of the third-party provider's API methods can be accessed directly via the Connect API. Call [`.request`](api-reference/#request-integrationtype-string-path-string-requestoptions-requestinit-promise-less-than-unknown-greater-than) to send an API request to a third-party app on behalf of one of your users.

Along with [**Workflows**](../workflows/building-workflows.md), the Connect API is one of two primary ways to build integrations with Paragon.

## When to use the Connect API

The Connect API is the most flexible way to interact with your users' third-party apps, and is a useful code-based approach for situations including:

* Performing a simple one-off request (e.g. fetching a list of Salesforce contacts)
* Accessing API methods that may not be available in Workflow [Integration Actions](../workflows/integration-actions.md)
* Writing custom code for complex or unique integration use cases
* Migrating existing integration code to Paragon

## Making requests with the Connect API

Every integration in your dashboard has a code example of using `paragon.request`, which takes three arguments:

* `integrationType`: The short name for the integration. i.e. "salesforce" or "googleCalendar". You can find this string on the Overview tab of the integration you want to access, on your Paragon dashboard.
  * When using a custom integration, the `integrationType` name is prefixed with `"custom."` For example, a custom integration titled "TaskLab" would be called `"custom.tasklab"`.
* `path`: The path (without the hostname) of the API request you are trying to access. An example might be "/v1/charges" for Stripe's charge API or "chat.postMessage" for Slack's Web API.
* `requestOptions`: Request options to include, such as:
  * `body`: An object representing JSON contents of the request.
  * `method`: An HTTP verb such as "GET" or "POST". Defaults to GET.

The function returns a Promise for the request output, which will have a shape that varies depending on the integration and API endpoint.

### **Client-side SDK Usage**

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
await paragon.request('slack', '/chat.postMessage', {
	method: 'POST',
	body: {
		channel: 'CXXXXXXX0' // Channel ID,
		text: 'This message was sent with Paragon Connect :exploding_head:'
	}
});

// -> Responds with { ok: true }, and sends a Slack message :)
```
{% endtab %}
{% endtabs %}

### **Server-side Usage**

**Base URL:**

* Cloud: `https://proxy.useparagon.com`
* [On-premise environments](broken-reference): `https://worker-proxy.`\[your on-prem host name]

If you'd like to issue a request from your server to an integration on behalf of an end-user, you can make a request to one of the following paths:

* `/projects/<Project ID>/sdk/proxy/<Integration Type>/<API Path>`
* or `/projects/<Project ID>/sdk/proxy/custom/<Integration ID>/<API Path>` for [custom-integrations.md](../resources/custom-integrations.md "mention").

{% tabs %}
{% tab title="REST API" %}
```http
https://proxy.useparagon.com/projects/<Paragon Project ID>/sdk/proxy
  /<Integration name>/<API path>

Authorization: Bearer <Paragon User Token>
```

* A Bearer token must also be specified with a Paragon User Token.
* This endpoint accepts any HTTP verb you want to use with the API.
* Body contents must be specified as `application/json`.

**Example**:

```
POST https://proxy.useparagon.com/projects/19d...012/sdk/proxy/slack/chat.postMessage

Authorization: Bearer eyJ...
Content-Type: application/json

{ 
    "channel": "CXXXXXXX0", 
    "text": "This message was sent with Paragon Connect :exploding_head:" 
}
```
{% endtab %}

{% tab title="REST API (Custom Integrations)" %}
When sending Connect API requests for Custom Integrations, the request path differs slightly. Use the `/custom/` path to send requests as shown:

<pre class="language-http"><code class="lang-http">https://proxy.useparagon.com/projects/&#x3C;Paragon Project ID>/sdk/proxy
<strong>  /custom/&#x3C;Integration ID>/&#x3C;API path>
</strong>
Authorization: Bearer &#x3C;Paragon User Token>
</code></pre>

* A Bearer token must also be specified with a Paragon User Token.
* This endpoint accepts any HTTP verb you want to use with the API.
* The Integration ID can be found in the dashboard (`/.../integrations/<Integration ID>`) or with the [#get-projects-integrations](api-reference/#get-projects-integrations "mention") API endpoint.

**Example:**

```
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

## Requesting files or binary response data

By default, the Connect API will attempt to parse the response data from the integration API as JSON. To receive the raw response data (including all HTTP headers that were received from the integration API), you can pass the `X-Paragon-Use-Raw-Response` header to the request.

This can be used when downloading binary/file data, such as images or PDF files, where the response cannot be encoded as JSON.

_The JavaScript SDK currently does not support returning non-JSON payloads. As an alternative, you can use your preferred request client to make the below API request._

{% tabs %}
{% tab title="REST API" %}
Below is an example of using the Connect API to download a file from Google Drive using their [`files.get`](https://developers.google.com/drive/api/v3/reference/files/get) endpoint.

```
GET https://proxy.useparagon.com/projects/19d...012/sdk/proxy/googledrive/files/<File ID>/?alt=media

Authorization: Bearer eyJ...
X-Paragon-Use-Raw-Response: 1
```
{% endtab %}
{% endtabs %}
