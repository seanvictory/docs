---
description: Quickly view a timeline and status of previous workflow executions.
---

# Viewing Task History

## Overview

Task History keeps track of your workflow executions and lives on the left side of the dashboard. It serves as a timeline and an easy way to navigate through your workflow history, revisit any failed workflows, and get a step-by-step breakdown of the executed tasks in each one.&#x20;

![](<../.gitbook/assets/Viewing Task History in Paragon Connect.png>)

Under Task History, you can find information about each workflow:

* **Status** (e.g. Success or Errored)
* **Trigger method** (e.g. every 5 minutes or via an App Event)
* **Integration** (e.g. Salesforce)
* **User** who triggered the workflow
* **Time and date** your workflow ran

Clicking anywhere on a workflow provides you with a detailed view of the status of each step related to that workflow. By default, Paragon stores workflow executions for up to 90 days. This number can be configured for users on [on-premise installations](broken-reference).

{% hint style="success" %}
**Want this data in an API?**

[**Task History API**](../api/task-history.md) **is available.** To learn more, contact your Customer Success Manager or [sales@useparagon.com](mailto:sales@useparagon.com).
{% endhint %}

## Detailed task execution

Each workflow in your Task History includes a step-by-step breakdown of the tasks related to the workflow. In this view, the Task History also shows:

* How long it took your workflow to run
* Number of tasks executed
* List of each executed step

![](<../.gitbook/assets/Viewing a Paragon Connect workflow execution.png>)

## Following your workflow <a href="#following-your-workflow" id="following-your-workflow"></a>

Paragon also allows you to visualize the flow of data throughout each workflow execution, making it easy for teams to track and debug. A **blue path** indicates the path taken by your workflow while running. A **grey path** indicates the path exists in the workflow but was not taken during this execution.

![](https://gblobscdn.gitbook.com/assets%2F-MCJwlyhqtCdBfCLUO0d%2F-MCNcV5-7xwbNryBslGB%2F-MCNciZkbDBTPg4EBUXT%2FFollowing%20workflow%20execution.png?alt=media\&token=3d1189a4-7ce2-4153-97d3-dd551fa63d39)

## Editing and replaying

![](<../.gitbook/assets/Editing and Replaying Tasks in Paragon Connect.png>)

* **Editing the Workflow:** Pressing the "Edit Workflow" button allows you to make changes to your workflow.
* **Replaying the Workflow:** Pressing the "Replay" button re-runs your currently deployed workflow. This is useful if you want to replay a workflow that initially failed.

{% hint style="info" %}
**Replaying a workflow**

This replays your workflow in its **execution state** with the original input data.
{% endhint %}

## Filtering

Filtering your Task History allows you to view the history of specific workflows that meet the criteria you specify while hiding the others.

![](<../.gitbook/assets/Filtering workflow executions in Paragon Connect.png>)

You can filter your Task History by:

* **User ID**
* **Status**
  * Success
  * Errored
  * Waiting
  * Running
  * Paused
  * Cancelled
* **Workflow name**
* **Integration name**
* **Date range**

## Debugging <a href="#debugging" id="debugging"></a>

Paragon provides a detailed breakdown of the data input and output of each step. Click on any step to view its status and data. You can make changes to a step by clicking the "Edit Step" button. Doing so will open the workflow editor and display the related step, where you can update it as needed.

<figure><img src="../.gitbook/assets/Debugging a Salesforce Workflow in Paragon Connect.png" alt=""><figcaption></figcaption></figure>
