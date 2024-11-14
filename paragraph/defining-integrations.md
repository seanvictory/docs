---
description: >-
  Learn how to define and configure workflows as code within a Paragraph
  project.
---

# Defining Integrations

## Project Structure

The folder structure of your Paragraph project defines what integrations are available.

The **src/integrations/** folder from your project root (the location of your paragon.json file) defines what integrations are available:

<figure><img src="../.gitbook/assets/[.prettierrc — tasklab-integrations] 2024-03-23 at 05.14.51 PM@2x.png" alt="" width="366"><figcaption></figcaption></figure>

Each subfolder in the **src/integrations/** folder contains:

* `workflows/` subfolder for each workflow for the integration.
* `config.ts` configures the display settings for the [Connect Portal](broken-reference) used for this integration, including the description and overview text. See more below in [#configuring-an-integration](defining-integrations.md#configuring-an-integration "mention").
* `inputs.ts` configures integration-level [User Settings](../connect-portal/workflow-user-settings.md) exposed to your customers in the Connect Portal. For example, if you need to prompt your users to select a Field Mapping for Salesforce or a Destination Folder for Google Drive, you can define a User Setting. See more below in [#configuring-user-settings](defining-integrations.md#configuring-user-settings "mention").

## Adding an Integration

To add an integration, you can use the CLI wizard:

```
para new integration
```

The CLI will prompt you to search the integration you want to use and install the necessary dependencies.

## Configuring an Integration

The **config.ts** file in any integration folder describes the Connect Portal configuration.

**Example:**

```typescript
import { IIntegrationConfig } from '@useparagon/core/integrations';

export const config: IIntegrationConfig = {
	description: "Sync records from Microsoft Dynamics",
	overviewText: `Connect your Microsoft Dynamics 365 account and sync your Dynamics 365 accounts, contacts, leads, or opportunities. Enable your sales team to close more deals by keeping your Dynamics 365 CRM records up to date - without manual data entry.
  
Our Dynamics 365 integration enables you to:  
  
- Automatically create or update records in Dynamics 365
- Sync records from Dynamics 365
- Receive updates when a record in Dynamics 365 is created or updated`,
}
```

The configuration includes the following fields:

* Short description of the integration
* An overview of the integration, as a string of Markdown-formatted text

## Configuring User Settings

The **inputs.ts** file in any integration folder defines integration-level [User Settings](../connect-portal/workflow-user-settings.md) exposed to your customers in the Connect Portal.

For example, if you need to prompt your users to select a Field Mapping for Salesforce or a Destination Folder for Google Drive, you can expose these options in the Connect Portal.&#x20;

**Example:**

```typescript
import { createInputs } from '@useparagon/integrations/salesforce';

const integrationInputs = createInputs({
    "fieldMapping": {
        id: "fieldMapping",
        type: 'field_mapping',
        title: "Map a custom Salesforce Object to an object in TaskLab",
        required: true,
    }
});

export default integrationInputs;
```

Define inputs as entries in the object passed to the `createInputs` function.

* The key (`"fieldMapping"`) is how you will reference this input in other Paragraph workflows.
* The `id` property of the object is how you will reference the value of this User Setting in the [SDK or API](../api/users.md) and must be a stable identifier. Changing this property will result in existing selections for this setting losing their values in your customers' Connect Portal.
* The `type` property of the object refers to the type of User Setting that is shown. Standard options include `"text"`, `"boolean"`, `"number"`, and `"password"`.
  * Integration-specific options like `"field_mapping"` are defined in the integration-specific types and can be found with your editor autocomplete (e.g. Ctrl-space in VS Code).
* The `title` property of the object is what will be displayed in the Connect Portal for your customers, to explain usage for this User Setting.
* Optionally, include:
  * `required`: Specify if this User Setting will be required for input by your customers.
  * `tooltip`: Specify a tooltip that will explain usage of this input for your customers.

_Workflow-level_ User Settings (settings specific to a particular workflow) can be defined within Workflows with the same format, in the `inputs` property of the workflow file.

## Custom Integrations

To define a [Custom Integration](../resources/custom-integrations.md) in your project, create a subfolder with the name `custom.[integrationName]`, where `integrationName` is the lowercased, alphanumeric name of the integration (for example: "GitHub Enterprise" -> `custom.githubenterprise`).

{% hint style="info" %}
Any changes to the `name` property of your Custom Integration will affect the subfolder name and string used in `paragon.connect()`.
{% endhint %}

In this folder, add the following `config.ts` file to configure the Custom Integration and its authentication and display settings:

```typescript
import {
  ICustomIntegrationConfig,
  createConfigInputs,
} from '@useparagon/core/integration';

export const inputs = createConfigInputs({});

const config: ICustomIntegrationConfig = {
  name: '',
  description: '',
  accentColor: '#000000',
  authenticationType: '', // oauth | basic | oauth_client_credential
  
  // For OAuth
  authorizationUrl: ``,
  accessTokenUrl: ``,
  scopes: '',
  includeClientIdAndSecrets: false,
  usePKCEInCodeExchange: true,
  
  apiBaseUrl: ``,
  testEndpointPath: ``,
  authorization: {
    type: 'bearer',
    token: `{{settings.oauthAccessToken}}`,
  },
};

export default config;
```

You'll also need to add an `inputs.ts` file to add any User Settings for this integration:

```typescript
import { createInputs } from '@useparagon/core/inputs';

const integrationInputs = createInputs({});

export default integrationInputs;
```

When defining workflows for Custom Integrations, you can import `ICustomIntegration` from the core library to get started:

<pre class="language-typescript"><code class="lang-typescript">import {
  // ...
<strong>  ICustomIntegration,
</strong>  // ...
} from '@useparagon/core';

export default class extends Workflow&#x3C;
<strong>  ICustomIntegration,
</strong>  IPersona&#x3C;typeof personaMeta>,
  DefaultInputToResultMap
> {
  define(
<strong>    integration: ICustomIntegration,
</strong>    context: IContext&#x3C;DefaultInputToResultMap>,
    connectUser: IConnectUser&#x3C;IPersona&#x3C;typeof personaMeta>>,
  ) {
  }
}
</code></pre>
