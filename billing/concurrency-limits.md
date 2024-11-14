---
description: Learn how concurrency is calculated in Paragon.
---

# Concurrency SLA

Paragon's concurrency SLA is the number of [workflow executions](../monitoring/viewing-task-history.md) that can run at a given time across all of your [Connected Users](connected-users.md). For example, if you have a concurrency SLA of 20, you can have up to 20 workflow executions running in the background at a given time.

<figure><img src="../.gitbook/assets/Viewing Task History in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

### Concurrency Levels

Our Concurrency SLA for our standard plans is as follows:

<table><thead><tr><th width="151">Plan</th><th>Concurrency SLA</th></tr></thead><tbody><tr><td><strong>Trial</strong></td><td><strong>5</strong> workflow executions</td></tr><tr><td><strong>Pro</strong></td><td><strong>20</strong> workflow executions</td></tr><tr><td><strong>Enterprise</strong></td><td><strong>50</strong> workflow executions</td></tr></tbody></table>

If you have any other questions regarding your concurrency SLA, please contact your Customer Success Manager.

### What happens if I reach my Concurrency SLA?

When you exceed this SLA, new workflow executions will be queued up for execution. Paragon accepts and stores all executions and will only execute them once the concurrent workflows drop below the SLA limit.

{% hint style="success" %}
To upgrade your Paragon subscription to a higher usage tier for concurrent workflows, [contact Sales](mailto:sales@useparagon.com) or reach out to your Customer Success Manager.
{% endhint %}
