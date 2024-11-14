---
description: Learn how Workflows automatically recover from integration API rate limits.
---

# Smart Rate Limits

## Overview

While building integration logic, you may encounter rate limit errors from upstream APIs if you consume requests faster than the integration provider supports.

Rate limits can be enforced by integration providers for either the requesting user or the requesting application (or both). They can be applied with different schedules (requests per minute, per hour, or per day).

Paragon provides automatic protection from rate limit errors in the form of Smart Rate Limits, adapting to known rate liimts from supported providers or rate limiting errors encountered during Workflow executions.

**Example: HubSpot rate limit**

```
429 Too Many Requests

{
  "status": "error",
  "message": "You have reached your daily limit.",
  "errorType": "RATE_LIMIT"
}
```

## Usage

All Workflows for [supported integrations](handling-rate-limits.md#supported-integrations) will automatically use Smart Rate Limits. No action is required to enable Smart Rate Limits on your account or Workflows.

## How it works

Smart Rate Limits automatically limit the pressure of all requests sent to an API by your Workflows, backing off and retrying when a rate limit is exceeded.

When a Smart Rate Limit is enforced, your workflow will be paused until it is safe to proceed with additional requests.

<figure><img src="../.gitbook/assets/Task History_ Execution View (1).png" alt=""><figcaption></figcaption></figure>

You can see the status of your paused workflow in Task History, along with the scheduled resumption time. When the workflow resumes, it will retry the last request that was suspended or failed.

### Supported integrations

The following integrations have Smart Rate Limits built-in and will respect known rate limits for their APIs. We are actively expanding support for Smart Rate Limits across our complete integrations catalog.

* Salesforce
* HubSpot (currently not available for `Search Records` or `Get All Records` actions)
* NetSuite
* Zendesk
