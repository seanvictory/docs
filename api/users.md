# Users API

## Introduction

The Users API allows you to query and modify the state of your Connected Users and their integrations.

The API includes REST endpoints (and matching SDK functions) for identifying what integrations your user has enabled, disconnecting integrations, and disabling workflows. The API also allows your application to associate metadata with a Connected User.

{% hint style="success" %}
✨ User Metadata is included in the **Pro Plan** and above. [**Contact us**](mailto:sales@useparagon.com) to schedule a demo of User Metadata or upgrade your account.
{% endhint %}

### When to use the Users API

The Users API can be used for integration usage analysis or maintenance of Connected Users. For example, using the API methods, you can...

* Automatically disconnect integrations when a user deletes or downgrades their account in your application
* Enrich your Connected Users' profile information with email, name, and other metadata
* Check if a user has enabled a certain integration and view account connection status

## Authorization

Requests to the Users API are authorized with a Bearer-type `Authorization` header using a Paragon User Token:

```
https://api.useparagon.com/projects/<Paragon Project ID>/sdk/...

Authorization: Bearer <Paragon User Token>
```

In the SDK, the Users API can be called directly after calling `paragon.authenticate`:

```javascript
// Authenticate the user
await paragon.authenticate("<Paragon Project ID>", "<Paragon User Token>");

// Call a Users API method, like setUserMetadata
paragon.setUserMetadata({ ... });
```

## Examples

### Associate Connected User with metadata

You can associate your user with metadata by including it in your existing SDK call to `paragon.authenticate`, as an additional parameter:

```javascript
await paragon.authenticate("<Paragon Project ID>", "<Paragon User Token>", {
    metadata: {
        Name: user.fullName,
        Email: user.email,
        apiKey: user.apiKey
    }
});
```

{% hint style="info" %}
**Note:** `Name` and `Email` are special parameters that you can view within the [Connected Users Dashboard](../monitoring/users.md). They are also case-sensitive.
{% endhint %}

Alternatively, you can supply the metadata from your application after authenticating:

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
paragon.setUserMetadata({
    Name: "Sean V",
    Email: "sean@useparagon.com",
    apiKey: "key_Y0kBVldPFInxK"
});
```
{% endtab %}

{% tab title="REST API" %}
**Request**

```
PATCH https://api.useparagon.com/projects/<Project ID>/sdk/me

// Headers
Authorization: <Paragon User Token>
Content-Type: application/json

// Body
{ "meta": { "Email": "sean@useparagon.com", "apiKey": "key_Y0kBVldPFInxK" } }
```
{% endtab %}
{% endtabs %}

#### **Using Metadata in Workflows**

Metadata properties are available for use in workflows in the variable menu of the Workflow Editor. To select a metadata property in a workflow, you'll first need to set a sample metadata object.

From any workflow, click the <img src="../.gitbook/assets/image (37).png" alt="" data-size="line">menu in the top navigation and select **Set User Metadata**:

![](<../.gitbook/assets/image (41).png>)

A dialog will appear to set a sample metadata object that represents the object you will pass through to the API or SDK as shown above in [#associate-connected-user-with-metadata](users.md#associate-connected-user-with-metadata "mention").

Any properties set in this sample object will be available for selection in the variable menu, in the "User Info" section:

![](<../.gitbook/assets/image (43).png>)

### Get Connected User info and integration state

You can access Connected User info (including any associated metadata) using `paragon.getUser` or with the REST API.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
paragon.getUser();

// Returns:
{
    authenticated: true,
    integrations: {
        salesforce: {
            enabled: true,
            credentialStatus: "VALID",  // "INVALID" if account is unreachable
            providerData: {...},        // Account details for integration
            providerId: "00502000..."   // Account's unique ID for integration
        }
    },
    meta: {...}, // Metadata provided by your application
    userId: "12345" // User ID specified in "sub" field of Paragon User Token
}
```
{% endtab %}

{% tab title="REST API" %}
**Request**

```
GET https://api.useparagon.com/projects/<Project ID>/sdk/me

// Headers
Authorization: Bearer <Paragon User Token>
```

**Response**

```
{
  "authenticated": true,
  "integrations": {
    "salesforce": {
      "enabled": true,
      "credentialStatus": "VALID",
      "providerData": {...},
      "providerId": "00502000..."
    }
  },
  "meta": {...},
  "userId": "12345"
}
```
{% endtab %}
{% endtabs %}

#### Validating account status with the `credentialStatus` property

If a previously connected account is unreachable (e.g. your user revokes access from the integration), the Connect Portal will show a warning and prompt your user to reconnect their account:

<figure><img src="../.gitbook/assets/Portal with invalid credential status.png" alt="" width="450"><figcaption></figcaption></figure>

You can check for this condition with the SDK with the `credentialStatus` property. For example:

<pre class="language-javascript"><code class="lang-javascript">paragon.getUser();

// Returns:
{
    integrations: {
        salesforce: {
<strong>            enabled: false,
</strong><strong>            credentialStatus: "INVALID",
</strong>            ...
        }
    },
    ...
}
</code></pre>

* When `credentialStatus` is `"INVALID"`, the `enabled` key will also be `false`.
* When `credentialStatus` is `"INVALID"`, Workflows and Connect API requests will error for this user's connected account until it is reconnected.

If you are using the [headless-connect-portal.md](../connect-portal/headless-connect-portal.md "mention"), you should show a reconnection prompt when `credentialStatus` is not `"VALID"`. You can initiate a reconnection flow with the same function used to start a connection flow: [#installintegration](api-reference/#installintegration "mention").

### Disconnecting integrations

Integrations can be disconnected using `paragon.uninstallIntegration` or with the REST API.

When an integration is disconnected, workflows for that integration will stop running for the authenticated user and any saved User Settings will be cleared.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
// Use the integration name, as used in paragon.connect();
await paragon.uninstallIntegration("salesforce");
```
{% endtab %}

{% tab title="REST API" %}
Get the ID of the integration you want to disconnect, with the `/sdk/integrations` endpoint:

**Request**

```
GET https://api.useparagon.com/projects/<Project ID>/sdk/integrations

// Headers
Authorization: Bearer <Paragon User Token>
```

**Response**

```
[
    { "id": "<Integration ID>", "type": "salesforce", ... },
    {...}
]
```



The `<Integration ID>` can be used to disconnect the integration for the user:

**Request**

{% code overflow="wrap" %}
```http
DELETE https://api.useparagon.com/projects/<Project ID>/sdk/integrations/<Integration ID>

// Headers
Authorization: Bearer <Paragon User Token>
```
{% endcode %}
{% endtab %}
{% endtabs %}
