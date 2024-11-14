---
description: Learn how tasks are counted in Paragon.
---

# Task Usage

A task is a unit of work that occurs in the Paragon platform on behalf of your Connected User.

* In [Broken link](broken-reference "mention"), each successful Action, Request, and Function are counted as tasks. You can see which steps succeeded in the workflow execution view of the [Task History](broken-reference) page (see screenshot below).
* All [making-api-requests.md](../api/making-api-requests.md "mention") requests are counted as tasks.

![](<../.gitbook/assets/Viewing Steps in Paragon Workflow.png>)

## How workflow steps count towards tasks

The following steps count as tasks:

* [Integrations](../resources/integrations/) (e.g. Salesforce, Slack, Google Sheets)
* [Request](../workflows/requests/)
* [Function](../workflows/functions.md)

The following steps **do not** count as tasks:

* [Triggers](../workflows/triggers/)
* [Conditional](../workflows/using-conditionals.md)
* [Fan Out](../workflows/using-fan-out.md)
* Response
* Delay

{% hint style="info" %}
**Note:** While the Fan Out itself doesn't count as a task, the contents within Fan Outs count as tasks per iteration.
{% endhint %}

## Task limits

The task limit is the maximum number of tasks you can run before your workflows stop executing during the current billing cycle.

## How task usage resets

Task usage resets at the beginning of your billing period each month. Unused tasks will not roll over to the next billing period.

### What happens if I reach my task limit?

If you are on a legacy plan that bills by task usage, you'll receive notification emails from Paragon as you get closer to your task limit.

We'll send an email notifying you that your workflows have stopped executing. Users on any of our [paid plans](https://www.useparagon.com/pricing) have a five-day grace period to upgrade before workflows stop executing.

Any unfinished tasks will show up in your [Task History](../monitoring/viewing-task-history.md) as a failed workflow. You can [replay stopped workflows](../monitoring/viewing-task-history.md#editing-and-replaying) when your billing cycle restarts or you upgrade your plan.

{% hint style="success" %}
Need more tasks? Upgrade to a [paid plan](https://useparagon.com/pricing) today!
{% endhint %}
