---
description: >-
  Use a Field Mapping User Setting to allow your users to define a mapping
  between objects in your application and their integration.
---

# Field Mapping

A **Field Mapping** is a type of User Setting that allows your users to define a mapping between an object in your application (an "Application Object") and an object in their connected integration account (an "Integration Object").

## Overview

For example: let's say your integration needs to sync your user's Task records from your application to their Tasks in a Salesforce account.

To do that, you'll need to build up a **Mapping** between fields in your application's Tasks and fields for a Task in a connected Salesforce account, as illustrated below:

<figure><img src="../.gitbook/assets/Frame 993 (1).png" alt=""><figcaption></figcaption></figure>

To enable your user to provide this Mapping, you can use the Connect Portal to provide a User Setting that displays each field of a Task (Title, Description, Completed) and prompts them to select a matching field of a Salesforce Task.

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

Once this Mapping is completed, you're able to use the Mapping like any other User Setting in the [Workflow Editor](field-mapping.md#usage-in-workflows) to transform objects in either direction (from Application Object to Integration Object _or_ from Integration Object to Application Object).

## Supported Integrations

Field Mapping settings are supported for all CRM integrations and a select number of other integrations, including:

* [Salesforce](../resources/integrations/salesforce.md)
* [HubSpot](../resources/integrations/hubspot.md)
* [Jira](../resources/integrations/jira.md)
* [Dynamics 365 Sales](../resources/integrations/microsoft-dynamics-365.md)
* [Pipedrive](../resources/integrations/pipedrive.md)
* [Marketo](../resources/integrations/marketo.md)
* [Sage Intacct](../resources/integrations/sage-intacct.md)
* [Sharepoint](../resources/integrations/sharepoint.md)

## Adding to the Connect Portal

Field Mapping settings can be added by visiting the "Customize Connect Portal" screen from a supported integration in your project, under the [User Settings](workflow-user-settings.md) section.

Select **Field Mapping** as the type for the User Setting:

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

You should give this setting a descriptive name that explains what this Mapping represents for your integration. For example, if Contacts is your intended Application Object to be mapped to a Salesforce Object, you might title this input "_Map Contacts to this object_".

Finally, **add a label for each property that should be mapped from your Application Object to a Salesforce Object**. Using the example above, you might add labels for "First Name", "Last Name", and "Email", if the schema for contacts in your app includes these properties.

In your Connect Portal, your users will be prompted to select an object from their Salesforce instance when enabling this workflow. For each of the object properties you labeled, your users will be prompted to select which object field that property should be mapped to.

## Dynamic Fields

{% hint style="info" %}
**Dynamic Field Mapping is available for Paragon Enterprise customers only.** To learn more, contact your Customer Success Manager or [sales@useparagon.com](mailto:sales@useparagon.com).
{% endhint %}

If your Application Fields may vary between your users for a particular Mapping, you are able to provide those options from your frontend application, through the SDK, using **Dynamic Fields**.

### Configuring your Field Mapping setting

You can configure a Dynamic Field Mapping by adding a Field Mapping input to your Connect Portal as described above.

<figure><img src="../.gitbook/assets/Frame 1 (20).png" alt=""><figcaption></figcaption></figure>

1. To set up Dynamic Field Mapping, toggle on the "Use dynamic fields" (<img src="../.gitbook/assets/image (40).png" alt="" data-size="line">) option in your Field Mapping setting configuration.
2. Once you've toggled this on, provide an Object Name that represents the name of your Application Object. This name will be used as an identifier to provide dynamic fields through the SDK, as demonstrated in the code example to `paragon.connect`.
3. _(Optionally)_ Edit the example fields included in the code snippet to represent realistic values that will be passed from your application. This will not affect the live configuration for your users, since values must be passed from your frontend application through the SDK, but you might find this useful to test example field values while building workflows.
4. Click **Save** to apply your changes.

### Passing Dynamic Fields through the SDK

After configuring your Field Mapping input to use Dynamic Fields, you can modify your call to `paragon.connect` to include fields to be dynamically rendered in the Connect Portal.

You can pass these fields by specifying the `mapObjectFields` option, with an object keyed by the name you specified in the "Object Name" field when configuring your setting:

```typescript
paragon.connect("salesforce", {
  mapObjectFields: {
    "Task": [
      { label: "Title", value: "title" },
      { label: "Description", value: "description" },
      { label: "Completed?", value: "isCompleted" }
    ]
  }
});
```

For each field passed, two values are specified:

* `label`: The human-readable description for the field. This will be shown to the user in the Field Mapping input.
* `value`: The field key used by the object as it exists in your application. _This key does not yet support nested properties._

Calling the above would result in the Connect Portal appearing like below:

<figure><img src="../.gitbook/assets/Frame 1 (17).png" alt=""><figcaption></figcaption></figure>

#### User-Configurable Mappings

If your use case requires it, you can allow users to control the _number_ of Field Mappings that are set by adding the `userCanRemoveMappings` option to your `paragon.connect` call.

```typescript
paragon.connect("salesforce", {
  mapObjectFields: {
    // Replace "Task" with your Application Object Name as specified in
    // Field Mapping input options
    "Task": {
      fields: [
        { label: "Title", value: "title" },
        { label: "Description", value: "description" },
        { label: "Completed?", value: "isCompleted" }
      ],
      userCanRemoveMappings: true
  }
});
```

Setting this option will result in the Connect Portal appearing like below:

<figure><img src="../.gitbook/assets/Frame 1 (19).png" alt=""><figcaption></figcaption></figure>

With this option, your users will be able to remove, re-add, and change any of the Mappings that are passed through `fields`. This option can be combined with the `defaultFields` option to achieve different display configurations:

<div>

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption><p><code>{ userCanRemoveMappings: true, defaultFields: [] }</code></p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p><code>{ userCanRemoveMappings: true,</code><br><code>defaultFields: ["title"] }</code></p></figcaption></figure>

</div>

`defaultFields` is an array of strings matching the `value` property of your `fields`. Any fields with matching `value` keys will be included in the initial list of Field Mappings that your user sees, when viewing the Connect Portal for the first time.

If `defaultFields` is unspecified, _all_ fields specified in the `fields` property will appear in the initial list of Field Mappings.

#### User-Creatable Fields

If your Application Object supports freeform fields or a flexible schema, you can allow users to create their own fields in the Field Mapping input.

```typescript
paragon.connect("salesforce", {
  mapObjectFields: {
    // Replace "Task" with your Application Object Name as specified in
    // Field Mapping input options
    "Task": {
      fields: [
        { label: "Title", value: "title" },
        { label: "Description", value: "description" },
        { label: "Completed?", value: "isCompleted" }
      ],
      defaultFields: [],
      userCanCreateFields: true
  }
});
```

If this option is specified, the Connect Portal will appear with an option for users to create their own fields, if the field is not available in the list populated by `fields`:

<figure><img src="../.gitbook/assets/Frame 1 (18).png" alt=""><figcaption></figcaption></figure>

## Usage in Workflows

After your user specifies their desired mapping in the Connect Portal, you can use their chosen values within workflow actions.

A Field Mapping contains 2 pieces of information:

* The selected Integration Object type (for example, a Salesforce Task).
* The field-level mappings between your Application Object and the selected Integration Object type (for example, Title ⇄ Salesforce Task Subject, Description ⇄ Salesforce Task Description.

You can use the **"Apply field mapping"** option to transform Application Objects (from App Events or Request triggers) to Integration objects and vice versa.

### Transforming from Application Object -> Integration Object

If you receive an Application Object in an App Event or Request payload, you can transform it into an Integration Object by selecting the **Field Mapping Object Type** in the "**Apply field mapping**" option for your App Event or Request trigger.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Once set, you will see the trigger output data update to show two objects:

* `originalPayload`: This is the original App Event or Request payload received by the trigger.
* `mappedIntegrationObject`: This is the Integration Object that was mapped based on the Field Mapping configured in the Connect Portal.&#x20;

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:** The mapped Integration Object only applies to the **root** of the original payload. If your field exists within a nested JSON, it will not work as expected.
{% endhint %}

In the Workflow Editor, the mapping is applied based on what is configured for the Test User. You can update the Mapping for the Test User by clicking the Preview button (<img src="../.gitbook/assets/image (50).png" alt="" data-size="line">) in the top right navigation from a workflow.

{% hint style="info" %}
**Note for testing Request Triggers:**

If you use a Request trigger, you will need to select "Detect parameters by sending a test request" for the option "How do you want to define test data for this step?"

Click **Test Step** ( <img src="../.gitbook/assets/image (32).png" alt="" data-size="line">) and send an example Request payload to the displayed URL to test the mapping from your Request payload to an Integration Object, using the mapping in the Connect Portal.
{% endhint %}

### Transforming from Integration Object -> Application Object

When receiving an Integration Object in an Integration trigger (for example, a Salesforce "New Record" trigger), you can transform it into an Application Object using the Field Mapping specified by your user.

In the trigger settings for your workflow, select the **Field Mapping Object Type** in the "**Apply field mapping**" option.

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Once set, you will see the trigger output data update to show two objects:

* `originalPayload`: This is the original Integration Object received by the trigger.
* `mappedApplicationObject`: This is the Application Object that was mapped based on the field mapping configured in the Connect Portal.

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

