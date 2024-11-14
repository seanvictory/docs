# Integration Actions

**Integration Actions, or just Actions, are the main building blocks of Paragon Workflows.** Paragon's workflow builder provides Actions for each integration provider that allow you to perform operations in your users' apps.

For example, common Actions include:

* Create a Salesforce contact
* Send a Slack message
* Update a Hubspot account
* List Google Calendar events

Paragon provides a simple-to-use UI for configuring and mapping data into each Action - making it easy to use Actions without any prior knowledge of an integration provider's API.

<figure><img src="../.gitbook/assets/Viewing a Slack Workflow in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Workflow User Settings

In some cases, you may want to provide your users the option to configure certain workflow settings. For example, if you have a Slack workflow that sends notifications to your users' workspaces, you may want to provide them the option of which Slack channel they want to send notifications to.

![](<../.gitbook/assets/Choosing a Slack channel in your Paragon Connect Portal.png>)

Actions in Paragon will indicate when they accept User Settings as an input parameter. In these cases, you should add the respective User Settings in the Connect Portal Editor, then use the **variable menu** by typing two left curly braces `{{` to reference that User Setting in the Action sidebar.

![](<../.gitbook/assets/Choosing a Slack channel to send notifications to in Paragon.gif>)

See [Workflow User Settings](../connect-portal/workflow-user-settings.md) for an in-depth overview of how to configure User Settings and use them in tandem with Actions.&#x20;

{% content-ref url="../connect-portal/workflow-user-settings.md" %}
[workflow-user-settings.md](../connect-portal/workflow-user-settings.md)
{% endcontent-ref %}

## Using Actions

For a complete list of all Actions supported by each Integration Provider, see our [Integrations Provider section](../resources/integrations/).

{% content-ref url="../resources/integrations/" %}
[integrations](../resources/integrations/)
{% endcontent-ref %}
