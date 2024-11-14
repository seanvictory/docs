---
description: Add conditional branching logic to your workflows
---

# Using Conditionals

## Overview

You can add conditional logic to workflows in Paragon using our Conditional step. Conditionals allow you to define rules to determine which of two paths your workflow should execute.

To add a conditional to your workflow, click the "+" button in the workflow canvas and choose the Conditional step from the sidebar.

<figure><img src="../.gitbook/assets/Using Conditionals in a Paragon Connect workflow.gif" alt=""><figcaption></figcaption></figure>

## Conditional rules

To add a rule to your conditional, click the dropdown menu in the 'select from step' input to choose a value that you want to evaluate. In the input to the right, you can choose a conditional operator (e.g. is true, equals, greater than).&#x20;

{% hint style="info" %}
**Note:** Operators depend on the value's type - for example, "greater than" only works for numbers, "exactly matches" only works for strings, etc.
{% endhint %}

### Conditional operators

* Contains: `string`
* Does not contain: `string`
* Exactly matches: `string`
* Does not exactly match: `string`
* Is in: `string`
* Is not in: `string`
* Starts with: `string`
* Does not start with: `string`
* Ends with: `string`
* Does not end with: `string`
* Greater than: `integer`
* Less than: `integer`
* Equals: `integer`
* Does not equal: `integer`
* After: `date/time`
* Before: `date/time`
* Equals: `date/time`
* Is true: `boolean`
* Is false: `boolean`
* Is Not Null
* Is Null
* Exists
* Does not exist
* Is empty: `Array`
* Is not empty: `Array`

If you choose a relational operator, another input will appear where you can type or choose or a second value to compare to.

You can combine multiple rules using **"and"** and **"or"** operators.
