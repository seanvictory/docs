---
description: Workflows connect data between your users' apps and your application
---

# Building Workflows

## Introduction

Once your users have connected their third-party app accounts in the Connect Portal, you can build workflows that connect data between your application and your users' apps. Paragon's visual workflow builder allows you to create custom integrations that your users can activate in their integrations.

Workflows are durable, retriable jobs that can be [triggered](triggers/) by your application or by events in your user's connected accounts. Workflows can be used to build out logic for your integration in Paragon's scalable, high-availability runtime.

![](<../.gitbook/assets/Using the workflow editor in Paragon.png>)

Here are some common step types that can get you started building workflows:&#x20;

* [**Integration Actions**](integration-actions.md)**:** Perform an action in your users' connected app account, like sending a Slack message or querying contacts from Salesforce
* [**Requests**](requests/): Make a request to any API, such as sending data to your application
* [**Functions**](functions.md): Write custom JavaScript to transform data or perform custom business logic, using [npm libraries](../resources/javascript-libraries.md) as supported
* [**Conditionals**](using-conditionals.md)**:** Add conditional branching logic
* [**Fan Out**](using-fan-out.md)**:** Iterate in parallel over a list of data and reduce results in downstream steps

Along with the [**Connect API**](../api/making-api-requests.md), Workflows are one of two primary ways to build integrations with Paragon.

## When to use Workflows

In general, Workflows are the way that most integrations are built with Paragon. When deciding when to use Workflows or the [**Connect API**](../api/making-api-requests.md), Workflows are often best suited for common use cases including:

* Pushing data from your application to your users' apps
* Receiving new or updated data from your users' apps (Webhooks)
* Allowing your users to configure integration options with custom fields
* Enabling non-engineering teams (e.g. Product or Client Services teams) to configure integrations without writing code

Here are examples of Workflows for a few common integrations:

* **Slack:** Send notifications from your application to Slack
* **Salesforce:** Sync contacts from your application to Salesforce
* **HubSpot:** Sync contacts HubSpot to your application
* **Google Calendar:** Create Google Calendar events from events in your application

## Creating Workflows

You can create a Workflow by selecting an integration and clicking **Create Workflow.**

<figure><img src="../.gitbook/assets/Create Workflow.png" alt=""><figcaption></figcaption></figure>

**Naming your workflow**

The Workflow Editor will appear and allow you to name your new workflow (click in the workflow title "New Workflow" and type to rename).

<figure><img src="../.gitbook/assets/Workflow Editor Navbar - Rename (1).png" alt=""><figcaption></figcaption></figure>

**Selecting a trigger**

Every workflow begins with a trigger. Select a trigger that matches how this workflow should begin its execution.

Workflows can only have one type of trigger. If you need to create a two-way sync between an integration and your application, you would create two workflows: one workflow to push updates from Integration -> Your App and another workflow to push updates from Your App -> Integration.

See the page below for full information on defining and using triggers:

{% content-ref url="triggers/" %}
[triggers](triggers/)
{% endcontent-ref %}

**Adding steps**

Beneath a trigger, you can build out your workflow logic as a series of steps. Steps can represent [**Integration Actions**](integration-actions.md), [**API requests**](requests/), [**custom functions**](functions.md), or other control flow elements in your workflow.

Click the "**+**" button <img src="../.gitbook/assets/add-step.svg.png" alt="" data-size="line"> underneath any step to add a new step. You can also right-click any step to add a step immediately downstream of the step, duplicate the step, or remove the step from the workflow.

<figure><img src="../.gitbook/assets/Step Editor context menu.png" alt=""><figcaption></figcaption></figure>

Requests, Integration Actions, and Function Steps can be configured to "Continue workflow if step fails" or to use [**Auto-Retries**](auto-retries.md).

#### Using Dynamic Data

You can insert data from any upstream step in the Workflow Editor with the [Dynamic Variable Menu](using-dynamic-variables.md). To access the Dynamic Variable Menu, click into any text input box, type two left curly braces `{{`, then select the desired step and specific reference to pull data from.

<figure><img src="../.gitbook/assets/Accessing the Dynamic Variable Menu in Paragon Connect.gif" alt=""><figcaption></figcaption></figure>

## Testing Workflows

Individual steps in a workflow can be tested as you build them. Each step has a Test Step button (<img src="../.gitbook/assets/Test Step button.png" alt="" data-size="line">) in the sidebar that executes the step as the Preview User (the user connected in the Preview page of your integration).

You can use the Test Workflow button (<img src="../.gitbook/assets/test-workflow.png" alt="" data-size="line">) when you want to test a workflow with all steps to completion.

{% hint style="info" %}
**Note:** When testing steps or workflows from the Workflow Editor, the data output returned is partial.

Here are some limitations to the test data displayed in the Workflow Editor:

* Arrays are truncated to 20 items maximum
* Paginated requests will only send 3 requests maximum
{% endhint %}

The above limitations improve the performance of the Workflow Editor as you build your workflow and reference variables between steps.

To test the workflow without these limitations, use a live Connected User to [connect an integration in the Connect Portal](../getting-started/displaying-the-connect-portal.md) and enable the workflow. Once you trigger the workflow for this user, the execution will appear in [Task History](../monitoring/viewing-task-history.md), where you can monitor the results and view the full input and output data.

## Deploying Workflows

You can push workflows live to your customers by pressing the purple Deploy button in the top-right corner of the Workflow Editor.&#x20;

<figure><img src="../.gitbook/assets/Deploying a workflow in Paragon (1).png" alt=""><figcaption></figcaption></figure>

## Editing Workflows

You can edit deployed workflows by making changes directly to the Workflow Editor. The changes will not affect the live workflow changes until you redeploy the workflow.

## Undeploying Workflows

To pull deployed workflows from your customers, click the purple “Deploy” button in the top-right corner of the Workflow Editor, then select “Undeploy”.

## Workflows and the Connect Portal

Workflows that you've deployed for an integration will appear in that integration's Connect Portal under the Configuration tab.&#x20;

There, your users can choose which workflows they want to activate for that integration. You can also provide options for your users to configure their workflow settings. For example, if you have a Slack workflow that sends notifications to your users' workspaces, you may want to provide them the option of which Slack channel they want to send notifications to.&#x20;

![](<../.gitbook/assets/Screen Shot 2021-02-11 at 11.37.03 AM.png>)

See [**Workflow User Settings**](../connect-portal/workflow-user-settings.md) for an overview of how to provide user-facing options for your users to configure their workflow settings.

## What's Next

Throughout the articles in this section, we'll provide a detailed overview of how to start building your own Workflows in Paragon.
