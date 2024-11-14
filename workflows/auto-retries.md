---
description: Automatically retry failed step executions.
---

# Auto-Retries

## Overview

When auto-retry is enabled on a step, the step automatically retries if the step execution fails. This is useful for ensuring your workflows run successfully when encountering intermittent errors, such as API rate limits.

Auto-retry is available on the following step types:

* [Integrations](../resources/integrations/) (e.g. Salesforce, Slack, Jira)
* [Request](requests/#overview)
* [Function](functions.md)

If a step with auto-retry enabled fails, Paragon will perform several retries, waiting after each failed execution before performing the next attempt. All attempts will only count as **one** [**task**](../billing/tasks.md) used.

The timing of retry attempts is as follows:

* **1st retry:** around `10 seconds` after initial attempt
* **2nd retry:** around `20 seconds` after 1st retry
* **3rd retry:** around `30 seconds` after 2nd retry
* **4th retry:** around `50 seconds` after 3rd retry
* **5th retry:** around `80 seconds`  after 4th retry

### Enabling Auto-Retry

To enable auto-retry for a step, click on the step, scroll to the bottom of the sidebar, and toggle auto-retry.

![](<../.gitbook/assets/Enabling Auto Retries in a Paragon workflow (1).gif>)

{% hint style="info" %}
**Note:** Enabling auto-retry only retries the **specific step**, not your entire workflow.
{% endhint %}

## How Auto-Retry works

**Deployed Workflows:** Paragon attempts to run your step **up to five times** with an exponential back-off. Retried steps appear as "Running" in [Task History](../monitoring/viewing-task-history.md#overview).

**Test Workflow** or **Test Step:** Paragon does not retry step executions.

While auto-retry is enabled, no error emails for the workflow will be sent during the auto-retry window. If Paragon fails to retry the step after the last attempt, we will send you an email indicating the error, and workflow execution in your [Task History](../monitoring/viewing-task-history.md#editing-and-replaying).
