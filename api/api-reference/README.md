# SDK / API Reference

## Paragon SDK and API Methods

Below are all the public functions exposed on the Paragon SDK global, accessible at `window.paragon`, and/or the Paragon REST API.

**For** [**on-premise**](broken-reference)**/single-tenant users:**

If you are using an on-prem/single-tenant instance of Paragon, you can call the `.configureGlobal` function to point the SDK to use the base hostname of your Paragon instance.

```typescript
import { paragon } from '@useparagon/connect';

// If your login URL is https://dashboard.mycompany.paragon.so:
paragon.configureGlobal({
    host: "mycompany.paragon.so"
});
```

### .authenticate(projectId: string, userToken: string)

`.authenticate` should be called at the beginning of your application's lifecycle in all cases. This is to make sure that the `userToken` is always as fresh as possible, with respect to your user's existing session on your own site.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
await paragon.authenticate(
	// You can find your project ID in the Overview tab of any Integration
	"38b1f170-0c43-4eae-9a04-ab85325d99f7",

	// See Setup for how to encode your user token
	"eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.ey..."
);
```
{% endtab %}
{% endtabs %}

Once `.authenticate` has been called, you can access the user's integration state with `.getUser()`. `.authenticate()` only needs to be called when using the Paragon SDK - when making requests to the Paragon REST API, you should instead provide the Paragon User Token in the Authorization header.

### .connect(integrationType: string, installOptions?: InstallOptions)

Call `.connect` to launch your Connect Portal for a specific integration provider. You can find the `integrationType` identifier you need in the Overview page for the integration.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
paragon.connect("salesforce");
```
{% endtab %}
{% endtabs %}

This function must be called after the Paragon SDK has completed authentication. You can `await` the Promise returned by [#.authenticate-projectid-string-usertoken-string](./#.authenticate-projectid-string-usertoken-string "mention") to show a loading state before users are able to access the Connect Portal.

You _must_ have an integration configured of this `integrationType` in your Paragon project for the Connect Portal to appear. Otherwise, this function does nothing.

<details>

<summary>Optional <code>installOptions</code></summary>

* `onSuccess` Callback invoked when an integration is successfully enabled.&#x20;
* `onError` Callback if an unexpected error occurs.
* `accountType` For integrations that support multiple account types, you can optionally designate a specific `accountType` to skip the account selection dialog.&#x20;

**Example**

```javascript
paragon.connect("salesforce", {
    // Only allow production-type Salesforce accounts to connect
    accountType: "default"
});
```

</details>

You can also connect multiple accounts for the same integration.

{% content-ref url="multiple-account-authorizations.md" %}
[multiple-account-authorizations.md](multiple-account-authorizations.md)
{% endcontent-ref %}

### .disableWorkflow(workflowId: string) -> Promise

Call `.disableWorkflow` to turn off a workflow for a user by ID.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
paragon.disableWorkflow("<Workflow ID>");
```
{% endtab %}

{% tab title="REST API" %}
**Request**

{% code overflow="wrap" %}
```
DELETE https://api.useparagon.com/projects/<Project ID>/sdk/workflows/<Workflow ID>

Authorization: Bearer <Paragon User Token>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### .getIntegrationMetadata(integrationType: string?) <a href="#getintegrationmetadata" id="getintegrationmetadata"></a>

Call `.getIntegrationMetadata` to get the `name`, `brandColor`, and `icon`, for any of your active integration providers. This is a great way to create your integrations page!

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
paragon.getIntegrationMetadata();

// Response
{
    [
        {
            type: 'salesforce',
            name: 'Salesforce',
            brandColor: '#057ACF',
            icon: 'https://cdn.useparagon.com/2.35.0/dashboard/public/integrations/salesforce.svg'
        },
        {
            type: 'hubspot',
            name: 'Hubspot',
            brandColor: '#F67600',
            icon: 'https://cdn.useparagon.com/2.35.0/dashboard/public/integrations/hubspot.svg'
        },
        {
            type: 'slack',
            name: 'Slack',
            brandColor: '#4A154B',
            icon: 'https://cdn.useparagon.com/2.35.0/dashboard/public/integrations/slack.svg'
        }
    ]
}
```
{% endtab %}

{% tab title="REST API" %}
```javascript
GET https://api.useparagon.com/projects/<Paragon Project ID>/sdk/metadata

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Response
{
    [
        {
            type: 'salesforce',
            name: 'Salesforce',
            brandColor: '#057ACF',
            icon: 'https://cdn.useparagon.com/2.35.0/dashboard/public/integrations/salesforce.svg'
        },
        {
            type: 'hubspot',
            name: 'Hubspot',
            brandColor: '#F67600',
            icon: 'https://cdn.useparagon.com/2.35.0/dashboard/public/integrations/hubspot.svg'
        },
        {
            type: 'slack',
            name: 'Slack',
            brandColor: '#4A154B',
            icon: 'https://cdn.useparagon.com/2.35.0/dashboard/public/integrations/slack.svg'
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### .getUser() → ParagonUser

Call `.getUser` to retrieve the currently authenticated user and their connected integration state.

A **ParagonUser** is an object shaped like:

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
paragon.getUser();

// Response
{
	authenticated: true,
	userId: "xyz", // The user ID you specified in the signed JWT
	integrations: {
		salesforce: {
			configuredWorkflows: {},
			credentialId: "987654-56a7-89b1-cd23-456789abcdef",
			credentialStatus: "VALID",
			enabled: true
			providerData: {
				instanceURL: "https://mycompany.my.salesforce.com"
			},
			providerId: "1234567890"
		},
		shopify: {
			configuredWorkflows: {},
			enabled: false
		}
	}
}
```
{% endtab %}

{% tab title="REST API" %}
```javascript
GET https://api.useparagon.com/projects/<Paragon Project ID>/sdk/me

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Response
{
	authenticated: true,
	userId: "xyz", // The user ID you specified in the signed JWT
	integrations: {
		salesforce: {
			configuredWorkflows: {},
			credentialId: "987654-56a7-89b1-cd23-456789abcdef",
			credentialStatus: "VALID",
			enabled: true
			providerData: {
				instanceURL: "https://mycompany.my.salesforce.com"
				},
			providerId: "1234567890"
		},
		shopify: {
			configuredWorkflows: {},
			enabled: false
		}
	}
}
```
{% endtab %}
{% endtabs %}

If the user is not authenticated, you'll receive back only `{ authenticated: false }` instead. Please check the `authenticated` property before using the `user.integrations` field.

### **.event(name: string, json: JSON)**

App Events can be sent from your application using the Paragon SDK or REST API. In both cases, you must pass two parameters:

* **name** - the event name defined in your App Event
* **payload** - the event payload that should match the event schema defined in your App Event

See the code examples below for how to send App Events using the Paragon SDK or API.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
var eventName = "Contact Created";
var eventPayload = { "name": "Brandon", "email": "b@useparagon.com" };

// Called once during your user's session 
paragon.authenticate("project-id", <Paragon User Token>);

// Trigger the "Contact Created" App Event
paragon.event(eventName, eventPayload);
```
{% endtab %}

{% tab title="REST API" %}
```http
// Trigger the "Contact Created" App Event
POST https://api.useparagon.com/projects/<Paragon Project ID>/sdk/events/trigger

// Headers
Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Body
{ 
    "name": "Contact Created", 
    "payload": { 
        "name": "Brandon", 
        "email": "b@useparagon.com" 
    }
}
```
{% endtab %}
{% endtabs %}

When sending live events from your application, Paragon will not validate that your event payload matches the defined event schema.



### .installIntegration(integrationType: string, installOptions?: InstallOptions) -> Promise\<void> <a href="#installintegration" id="installintegration"></a>

{% hint style="info" %}
This function should be used only if you are using your own components to show connected integrations and their status, instead of the Connect Portal.

Otherwise, you can use [the `.connect` function](./#.connect-integrationtype-string).
{% endhint %}

The `.installIntegration` can be used to start the connection process for an integration _without_ the Connect Portal appearing over your user interface. You can find the `integrationType` identifier you need in the Overview page for the integration.

This function rejects the returned Promise if the integration is already installed for the authenticated user.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
paragon.installIntegration("googledrive");
```
{% endtab %}
{% endtabs %}

**Note**: If the integration specified by `integrationType` requires API keys or post-authentication options, the Connect Portal will still appear to capture those values from your user at that time. The Connect Portal will automatically be dismissed after those values are entered.

This function accepts the same optional install options as [#.connect-integrationtype-string-installoptions-installoptions](./#.connect-integrationtype-string-installoptions-installoptions "mention").

### .subscribe(eventName: string, handler: Function) <a href="#subscribe" id="subscribe"></a>

Call `.subscribe` to subscribe to different events and changes from the Paragon SDK. You can find the  possible `eventNames`below:

| Event Type                | Usage in `.subscribe()`    | Usage in `.connect()` |
| ------------------------- | -------------------------- | --------------------- |
| **Integration enabled**   | `"onIntegrationInstall"`   | `"onInstall"`         |
| **Integration disabled**  | `"onIntegrationUninstall"` | `"onUninstall"`       |
| **Workflow state change** | `"onWorkflowChange"`       | `"onWorkflowChange"`  |
| **Connect Portal opened** | `"onPortalOpen"`           | `"onOpen"`            |
| **Connect Portal closed** | `"onPortalClose"`          | `"onClose"`           |

Subscribing to SDK Events applies to all integrations _globally_. Specifying callbacks to `.connect()` only applies to a currently open Connect Portal _locally_.

See the code examples below for how to subscribe to events using the Paragon SDK.

{% tabs %}
{% tab title="Integration Enabled / Disabled" %}
```javascript
type IntegrationUninstallEvent = {
  integrationId: string;
  integrationType: VisibleConnectAction;
};

// Using global subscribe
paragon.subscribe(
  "onIntegrationUninstall",
  (event: IntegrationUninstallEvent, user: AuthenticatedConnectUser) => { /* ... */ }
);
```
{% endtab %}

{% tab title="Workflow State Changed" %}
```javascript
type WorkflowStateChangeEvent = {
  integrationId: string;
  workflowId: string;
};

// Using global subscribe
paragon.subscribe(
  "onWorkflowChange",
  (event: WorkflowStateChangeEvent, user: AuthenticatedConnectUser) => { /* ... */ }
);
```
{% endtab %}

{% tab title="Connect Portal Opened / Closed" %}
```javascript
type PortalOpenEvent = {
  integrationId: string;
  integrationType: VisibleConnectAction;
};

type PortalCloseEvent = {
  integrationId: string;
  integrationType: VisibleConnectAction;
};

// Using global subscribe
paragon.subscribe(
  "onPortalOpen",
  (event: PortalOpenEvent, user: AuthenticatedConnectUser) => { /* ... */ }
);
paragon.subscribe(
  "onPortalClose",
  (event: PortalCloseEvent, user: AuthenticatedConnectUser) => { /* ... */ }
);
```
{% endtab %}
{% endtabs %}

Alternatively, you can subscribe `onOpen`, `onClose`, `onUninstall` , and `onWorkflowChange` as a one-time event locally.

{% tabs %}
{% tab title="Integration Enabled / Disabled" %}
```javascript
type IntegrationUninstallEvent = {
  integrationId: string;
  integrationType: VisibleConnectAction;
};

// Using local call to paragon.connect
paragon.connect("<integration>", {
  onSuccess: {/* ... */},
  onError: {/* ... */},
  onUninstall: (event: IntegrationUninstallEvent, user: AuthenticatedConnectUser) => { /* ... */ }
});
```
{% endtab %}

{% tab title="Workflow State Changed" %}
```javascript
type WorkflowStateChangeEvent = {
  integrationId: string;
  workflowId: string;
};

// Using local call to paragon.connect
paragon.connect("<integration>", {
  onWorkflowChange: (event: WorkflowStateChangeEvent, user: AuthenticatedConnectUser) => {/* ... */}
});
```
{% endtab %}

{% tab title="Connect Portal Opened / Closed" %}
```javascript
type PortalOpenEvent = {
  integrationId: string;
  integrationType: VisibleConnectAction;
};

type PortalCloseEvent = {
  integrationId: string;
  integrationType: VisibleConnectAction;
};

// Using local call to paragon.connect
paragon.connect("<integration>", {
  onOpen: (event: PortalOpenEvent, user: AuthenticatedConnectUser) => {/* ... */},
  onClose: (event: PortalCloseEvent, user: AuthenticatedConnectUser) => {/* ... */}
});
```
{% endtab %}
{% endtabs %}

### .request(integrationType: string, path: string, requestOptions: RequestInit ) → Promise

Call `.request` to send an API request to a third-party integration on behalf of one of your users.

Every integration in your dashboard has a code example of using `paragon.request`, which takes three arguments:

* `integrationType`: The short name for the integration. i.e. "salesforce" or "googleCalendar". You can find this string on the Overview tab of the integration you want to access, on your Paragon dashboard.
* `path`: The path (without the hostname) of the API request you are trying to access. An example might be: "/v1/charges" for Stripe's charge API or "chat.postMessage" for Slack's Web API.
* `requestOptions`: Request options to include, such as:
  * `body`: An object representing JSON contents of the request.
  * `method`: An HTTP verb such as "GET" or "POST". Defaults to GET.

The function returns a promise for the request output, which will have a shape that varies depending on the integration and API endpoint.

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

// -> Responds with { ok: true }, and sends a message :)
```
{% endtab %}

{% tab title="REST API" %}
```http
POST https://proxy.useparagon.com/projects/<Paragon Project ID>/sdk/proxy/slack/chat.postMessage

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

{ 
    "channel": "CXXXXXXX0", 
    "text": "This message was sent with Paragon Connect :exploding_head:" 
}

// -> Responds with { output: { ok: true }}, and sends a message :)
```
{% endtab %}
{% endtabs %}

### .setUserMetadata(meta: object)

Call `.setUserMetadata()` to associate the authenticated user with metadata from your application. This metadata can be accessed with `.getUser()` or retrieved over the API.

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

### .uninstallIntegration(integrationType: string) -> Promise <a href="#workflow" id="workflow"></a>

Call `.uninstallIntegration()` to disconnect an integration for the authenticated user.

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

### .workflow(workflowId: string, **options: FetchOptions)** <a href="#workflow" id="workflow"></a>

Call `.workflow()` to trigger a Paragon workflow that sends a custom response back to your app. Note: The workflow must be enabled and use a Request-type trigger.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
// Called once during your user's session 
paragon.authenticate("project-id", <Paragon User Token>)

// Trigger the "Lead Created" workflow
await paragon.workflow("<workflow_id>", {
  "body": {
    "email": "bowie@useparagon.com",
    "first_name": "Bowie",
    "last_name": "Foo"
  }
});
  
```
{% endtab %}

{% tab title="REST API" %}
<pre><code><strong>// Trigger the "Lead Created" Workflow
</strong>POST https://api.useparagon.com/projects/&#x3C;Paragon Project ID>/sdk/triggers/&#x3C;Workflow ID>

Authorization: Bearer &#x3C;Paragon User Token>
Content-Type: application/json

{
  "email": "bowie@useparagon.com",
  "first_name": "Bowie",
  "last_name": "Foo
}
</code></pre>
{% endtab %}
{% endtabs %}

### Get project's integrations

Returns a list of the integrations enabled for the Paragon project by the ID in the URL.&#x20;

* Includes the Connect Portal configuration for each integration (as `.configs`) and the Workflows associated with each integration (as `.workflows`)
* The **providerId** is the authenticated user's ID assigned by their integration provider (e.g. for a Salesforce integration, this would would be the user's Salesforce user ID)

This method is currently available via REST API only.

{% tabs %}
{% tab title="REST API" %}
```http
GET https://api.useparagon.com/projects/<Paragon Project ID>/sdk/integrations

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Example response (may include more than is in this list):

[{
  "id": "2f08e65f-d924-42ab-9618-b6023d82ffbd",
  "dateCreated": "2021-03-02T00:22:33.166Z",
  "dateUpdated": "2021-03-02T00:22:33.166Z",
  "projectId": "908f4c5e-6394-46a5-9355-3f729edbd160",
  "customIntegrationId": null,
  "type": "slack",
  "isActive": true,
  "configs": [
        {
        "id": "3ebcc179-a1a6-447f-8dc9-5017f40f08ef",
        "dateCreated": "2021-03-02T00:22:33.166Z",
        "dateUpdated": "2023-05-15T21:01:00.260Z",
        "integrationId": "2f08e65f-d924-42ab-9618-b6023d82ffbd",
        "values": {
          "overview": "####Our Slack integration enables you to:\n   \n\n• Receive alerts and notifications in your Slack workspace\n• Notify or DM specific team members based on certain activity",
          "sharedMeta": {},
          "accentColor": "#4A154B",
          "description": "Send notifications to Slack",
          "workflowMeta": {}
    },
  ],
  "workflows" [
        {
        "id": "1b22193b-e355-458d-b6a3-5e5516edb588",
        "dateCreated": "2021-06-02T23:17:05.714Z",
        "dateUpdated": "2021-07-13T20:55:41.895Z",
        "description": "Send Updates to Slack",
        "projectId": "908f4c5e-6394-46a5-9355-3f729edbd160",
        "teamId": "2116f794-07c7-4dfe-a302-e816a2f7ed72",
        "isOnboardingWorkflow": false,
        "integrationId": "2f08e65f-d924-42ab-9618-b6023d82ffbd",
        "steps": []
      },
  ],
  "customIntegration": null,
  "hasCredential": true,
  "connectedUserLimitOnDevCred": 0,
  "connectedUserLimitReached": true,
  "name": "Slack",
  "brandColor": "#4A154B",
  "needPreOauthInputs": false,
  "providerType": "slack",
  "authenticationType": "oauth"
}]
```
{% endtab %}
{% endtabs %}

### Get user's Connect credentials

Returns a list of the user's Connect credentials (i.e., the accounts connected and authorized by the end user).

This method is currently available via REST API only.

{% tabs %}
{% tab title="REST API" %}
```http
GET https://api.useparagon.com/projects/<Paragon Project ID>/sdk/credentials

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Example response (may include more than is in this list):

[{
  "id": "00da4146-7ac4-4253-a8f7-96849b8137d9",
  "dateCreated": "2021-03-24T12:19:21.511Z",
  "dateUpdated": "2021-03-24T12:19:28.512Z",
  "dateDeleted": null,
  "projectId": "db06d291-ba2c-41c5-9a12-9362abfd6228",
  "integrationId": "95bedc9f-6a22-4855-b08d-e68dc073ad91",
  "personaId": "0563109f-5e71-46c5-8483-1ac8c0913d6c",
  "config": {
    "configuredWorkflows": {
      "3eb95154-3c7b-413c-bf14-ba367d95b53f": {
        "enabled": true,
        "settings": {
					"example-input-id": "example value"
				}
      }
    }
  },
  "isPreviewCredential": false,
  "providerId": "50150244515"
}]
```
{% endtab %}
{% endtabs %}

### Update user's Connect credential

Updates the user's connected integration account, including any settings and configured workflows.

This endpoint updates by replacement with respect to the `config` property, so this endpoint should only be used after retrieving the existing value (which can be done by using the above endpoint: [#get-users-connect-credentials](./#get-users-connect-credentials "mention")).

This method is currently available via REST API only.

{% tabs %}
{% tab title="REST API" %}
```http
PATCH https://api.useparagon.com/projects/<Paragon Project ID>/sdk/credentials/<Connect Credential ID>

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Body: Example showing <Workflow ID> being enabled
{
    "config": {
        "configuredWorkflows": {
            ...
            "<Workflow ID>": {
                "enabled": true,
                "settings": {}
            }
        },
        "sharedSettings": {...}
    }
}
```

**Note**: In the above example, the existing value for `config` must be provided in full, with the intended changes applied. This is because `config` will be updated by replacement.
{% endtab %}
{% endtabs %}

## ExternalFilePicker

You can use the Paragon SDK to allow your user to select files from a File Storage integration in your app.

The SDK provides an `ExternalFilePicker` class to load any necessary JavaScript dependencies into your page and authenticate with your user's connected account.

#### Supported integrations for ExternalFilePicker:

* [Google Drive](../../resources/integrations/google-drive.md#using-the-google-drive-file-picker)

### new paragon.ExternalFilePicker(integrationType, options)

Construct a new instance of an ExternalFilePicker for an integration given by `integrationType`. Any required JS dependencies do not start loading until [`.init`](./#picker.init-initconfig) is called.

**Example:**

```javascript
const picker = new paragon.ExternalFilePicker("googledrive", {
  allowedTypes: ["application/pdf"],
  allowMultiselect: false,
  onFileSelect(files) {
    console.log("User picked files", files);
  }
});
```

#### **Options:**

* `allowedTypes` (default: `undefined`)
  * An array of MIME types to allow for file selection, e.g. `["application/pdf", "image/jpeg"]`
  * If `undefined`, all types will be allowed.
* `allowMultiSelect` (default: `false`)
  * If `true`, allow multiple files to be selected.
* `allowFolderSelect` (default: `false`)
  * If `true`, allow folders to be selected.
* `onOpen()`
  * Called when a Picker successfully appears in the app.
* `onClose()`
  * Called when a Picker gets closed.
* `onFileSelect(files)`
  * Called when a Picker file selection is made.
  * `files` is an Array of objects with the selected file objects from the 3rd-party picker script.
* `onCancel()`
  * Called when a Picker gets closed without any files selected.

### picker.init(initConfig)

Initialize a file picker with required configuration `initConfig`. Required configuration varies per integration; see [integration-specific documentation](./#supported-integrations-for-externalfilepicker) for specific details.

This function loads required JS dependencies into the page, if they have not already been loaded. Other methods, like `.open` and `.getInstance`, cannot be called until the Promise returned by `.init` is resolved.

**Example:**

```javascript
await picker.init({
  // Google Developer Key
  developerKey: "AIzaS..."
});
```

### picker.open()

Presents the file picker in your app.

Selected files or other events will be received in the [callbacks](./#options) you specified in the constructor.

**Example:**

```javascript
picker.open();
```

### picker.getInstance()

Returns a reference to the third-party JS library object that this file picker is using. This object can be used for additional integration-specific customization.

