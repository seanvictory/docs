---
description: Run a sequence of steps over each object in an array.
---

# Using Fan Out

## Overview

Fan Out allows you to run the same sequence of steps over each object in an array (or list) of objects. For example, you might want to query a segment of users from your database and send each user a message.&#x20;

To add a Fan Out to your workflow, click the "+" button in the Workflow Editor and choose Fan Out from the sidebar. Then, click the dropdown button under "Fan out which array?" to invoke the dynamic variable menu and choose the array you want to fan out.

<figure><img src="../.gitbook/assets/Using a Fan Out in Paragon Connect.gif" alt=""><figcaption></figcaption></figure>

## Referencing data within a Fan Out

Any steps you add within a Fan Out will run for each object in the array passed into the Fan Out. To reference the object in the array from within a Fan Out, you can reference the Fan Out's `instance` object from the variable menu.

{% hint style="info" %}
**Note:** Iterations within a Fan Out are executed in parallel, although your workflow will wait for all iterations to finish before proceeding to steps after the Fan Out.
{% endhint %}
