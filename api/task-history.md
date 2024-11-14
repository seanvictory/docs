# Task History API

## Introduction

The Task History API allows you to query your users' usage of integration workflows and access data from historical workflow executions.

{% hint style="info" %}
**Task History API is available for Paragon customers on Enterprise plans.** To learn more, contact your Customer Success Manager or [sales@useparagon.com](mailto:sales@useparagon.com).
{% endhint %}

### When to use the Task History API

The Task History API can be used to analyze integration usage or pull information about historical workflow executions into your application. For example, you can use the Task History API to:

* Query the number of workflow executions that ran last week for the Salesforce integration
* Query all failed workflow executions for a specific user
* Export all tasks that occurred in a specific month into Google BigQuery

You can find example queries in the request format below.

### Generating API Keys

The Task History API authorizes with a project-level API Key, instead of the Paragon User Token.

API Keys provide access to _all Connected Users_ in the project they are created in and can be rotated or deleted after being generated.

<figure><img src="../.gitbook/assets/image (60).png" alt="API Keys screen in Paragon dashboard"><figcaption></figcaption></figure>

To generate a new project-level API Key:

1. Visit your Project's Settings > API Keys.
2. Click "**Create API Key**". Provide a meaningful name for the API Key for your reference.
3. The API Key will appear on a one-time basis for you to save in a secure place.

## Examples

### Querying Salesforce workflow executions run during a week's time period

{% tabs %}
{% tab title="REST API" %}
{% code overflow="wrap" %}
```
GET /projects/<Paragon Project ID>/task-history/workflow-executions?integration=salesforce&afterDate=2023-02-16T00:00:00&beforeDate=2023-02-23T00:00:00

Authorization: Bearer <Paragon API Key>
```
{% endcode %}

**Response example:**

```json
{
    "workflowExecutions": [
        {
            "id": "c70cafa5-4f80-45c7-b5b3-71454f6d638d",
            "userId": "d1f142cd-1dfe-4d76-ab4c-8f64901a9c5c",
            "taskCount": 1,
            "runDuration": 1477,
            "workflowId": "c395c170-4541-499c-afd1-0eccfaae49c9",
            "status": "SUCCEEDED",
            "dateEnded": "2023-02-20T06:21:43.751Z",
            "dateStarted": "2023-02-20T06:21:42.274Z"
        },
        ...
    ],
    "nextLink": "https://zeus.useparagon.com/projects/d1f142cd-1dfe-4d76-ab4c-8f64901a9c5c/task-history/workflow-executions?integration=salesforce&afterDate=2023-02-16T00:00:00&beforeDate=2023-02-23T00:00:00&sortBy=ASC&offset=100",
    "total": 14295
}
```
{% endtab %}
{% endtabs %}

### Querying failed workflow executions for a user

{% tabs %}
{% tab title="REST API" %}
{% code overflow="wrap" %}
```
GET /projects/<Paragon Project ID>/task-history/workflow-executions?userId=test@example.com&status=FAILED

Authorization: Bearer <Paragon API Key>
```
{% endcode %}

**Response example:**

```json
{
    "workflowExecutions": [
        {
            "id": "317a396c-7dc8-4a1f-8ceb-b39d5ad845da",
            "userId": "123456",
            "taskCount": 0,
            "runDuration": 3847,
            "workflowId": "24cf377b-c7f5-40e7-9b10-6cc5d811266a",
            "status": "FAILED",
            "dateEnded": "2023-03-01T11:15:04.051Z",
            "dateStarted": "2023-03-01T11:15:00.204Z"
        },
        ...
    ],
    "nextLink": "https://zeus.useparagon.com/projects/d1f142cd-1dfe-4d76-ab4c-8f64901a9c5c/task-history/workflow-executions?userId=test@example.com&status=FAILED&sortBy=ASC&offset=100",
    "total": 180
}
```
{% endtab %}
{% endtabs %}

## Endpoint Reference

### Base URL

The Base URL of the Task History API endpoints begin with the same origin as the [Connect](making-api-requests.md) and [Users APIs](users.md).

* For cloud customers who sign in to `dashboard.useparagon.com`, the Base URL is **https://api.useparagon.com/projects/\<Project ID>/task-history**
* For on-premise customers who sign in to `dashboard.<On-Premise URL>`, the base URL is **https://zeus.\<On-Premise URL>/projects/\<Project ID>/task-history**

### Authorization

Requests to the Task History API must provide an API Key as a Bearer-type `Authorization` header in the request:

```
GET /projects/<Paragon Project ID>/task-history/workflow-executions

Authorization: Bearer <Paragon API Key>
```

### Pagination

API responses that include multiple objects will be provided in page size of 100. In the case that there are additional pages of data available, the API response will include a URL to get the next 100 records.

### Rate Limits

The Task History API has a rate limit of 1,000 requests per 10 minutes. If you need higher rate limits, please reach out to our team at [support@useparagon.com](mailto:support@useparagon.com)

## API Methods

### Get workflow executions

<mark style="color:blue;">`GET`</mark> `[Base URL]/workflow-executions`

Search through historical workflow executions with the below filtering options as query parameters.

#### Query Parameters

| Name        | Type          | Description                                                                                                                                                                                             |
| ----------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| userId      | String        | Filter executions by a specific Connected User ID.                                                                                                                                                      |
| workflowId  | UUID          | Filter executions for a specific workflow ID.                                                                                                                                                           |
| integration | String        | Filter executions for a specific integration, for example, `salesforce`. The integration name is in the same format as provided to [`paragon.connect`](api-reference/#.connect-integrationtype-string). |
| status      | String        | <p>Filter executions by a status:</p><p><code>EXECUTING</code> | <code>FAILED</code> | <code>SUCCEEDED</code> | <code>DELAYED</code></p>                                                                |
| beforeDate  | String (Date) | Filter executions that began before a certain timestamp, in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO\_8601) (for example, `2023-02-22`)                                                      |
| afterDate   | String (Date) | Filter executions that began after a certain timestamp, in ISO 8601 format                                                                                                                              |
| offset      | Number        | Offset results by a fixed number of records.                                                                                                                                                            |
| sortBy      | String        | Sort by execution time: `ASC` \| `DESC`. Defaults to `DESC`.                                                                                                                                            |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    "workflowExecutions": [
        {
            "id": "c70cafa5-4f80-45c7-b5b3-71454f6d638d",
            "userId": "d1f142cd-1dfe-4d76-ab4c-8f64901a9c5c",
            "taskCount": 1,
            "runDuration": 1477,
            "workflowId": "c395c170-4541-499c-afd1-0eccfaae49c9",
            "status": "SUCCEEDED",
            "dateEnded": "2023-02-20T06:21:43.751Z",
            "dateStarted": "2023-02-20T06:21:42.274Z"
        },
        // ...
    ],
    // nextLink is `null` if there are no more results
    "nextLink": "https://zeus.useparagon.com/projects/d1f142cd-1dfe-4d76-ab4c-8f64901a9c5c/task-history/workflow-executions?integration=salesforce&afterDate=2023-02-16T00:00:00&beforeDate=2023-02-23T00:00:00&sortBy=ASC&offset=100",
    "total": 14295
}
```
{% endtab %}
{% endtabs %}

### Get workflow execution by ID

<mark style="color:blue;">`GET`</mark> `[Base URL]/workflow-executions/:executionID`

Get details for a specific workflow execution by its Execution ID.

#### Path Parameters

| Name                                          | Type | Description                                 |
| --------------------------------------------- | ---- | ------------------------------------------- |
| executionID<mark style="color:red;">\*</mark> | UUID | The ID of the execution to get details for. |

#### Query Parameters

| Name        | Type          | Description                                                                                                                                                                                             |
| ----------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| userId      | String        | Filter executions by a specific Connected User ID.                                                                                                                                                      |
| workflowId  | UUID          | Filter executions for a specific workflow ID.                                                                                                                                                           |
| integration | String        | Filter executions for a specific integration, for example, `salesforce`. The integration name is in the same format as provided to [`paragon.connect`](api-reference/#.connect-integrationtype-string). |
| status      | String        | <p>Filter executions by a status:</p><p><code>EXECUTING</code> | <code>FAILED</code> | <code>SUCCEEDED</code> | <code>DELAYED</code></p>                                                                |
| beforeDate  | String (Date) | Filter executions that began before a certain timestamp, in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO\_8601) (for example, `2023-02-22`)                                                      |
| afterDate   | String (Date) | Filter executions that began after a certain timestamp, in ISO 8601 format                                                                                                                              |
| offset      | Number        | Offset results by a fixed number of records.                                                                                                                                                            |
| sortBy      | String        | Sort by execution time: `ASC` \| `DESC`. Defaults to `DESC`.                                                                                                                                            |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    "id": "daff08e3-c299-4005-9799-be69090ebae1",
    "userId": "test",
    "taskCount": 1,
    "runDuration": 8,
    "workflowId": "88d20d69-e585-4eea-aac4-5b7aea0521e8",
    "status": "FAILED",
    "dateEnded": "2022-11-25T22:15:07.987Z",
    "dateStarted": "2022-11-25T22:15:00.038Z",
    "stepExecutions": [
        {
            "id": "5fec7d78-7e10-4b4a-bdfc-292f629774bf",
            "stepId": "0f7cce44-d292-4555-bae8-5b904a0c4ac9",
            "workflowExecutionId": "daff08e3-c299-4005-9799-be69090ebae1",
            "status": "SUCCEEDED",
            "type": "TRIGGER/CRON",
            "start": "2022-11-25T22:15:00.075Z",
            "end": "2022-11-25T22:15:00.084Z",
            "next": [
                "29e675eb-0910-4d5c-8a5c-a4a4c1895605"
            ],
            "prev": null,
            "inputSize": "220",
            "outputSize": "76"
        },
        {
            "id": "29e675eb-0910-4d5c-8a5c-a4a4c1895605",
            "stepId": "7459bbf5-e55b-49e8-9390-084cf86752e5",
            "workflowExecutionId": "daff08e3-c299-4005-9799-be69090ebae1",
            "status": "FAILED",
            "type": "ACTION/REQUEST",
            "start": "2022-11-25T22:15:07.850Z",
            "end": "2022-11-25T22:15:07.873Z",
            "next": [],
            "prev": "5fec7d78-7e10-4b4a-bdfc-292f629774bf",
            "inputSize": "712",
            "outputSize": "824"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Get details for step of workflow execution

<mark style="color:blue;">`GET`</mark> `[Base URL]/workflow-executions/:executionID/step-executions/:stepExecutionID`

Get details for a specific step of a workflow execution, by its Execution ID _and_ Step Execution ID. These details include step input/output and run duration for the specific step.

#### Path Parameters

| Name                                              | Type | Description                                     |
| ------------------------------------------------- | ---- | ----------------------------------------------- |
| executionID<mark style="color:red;">\*</mark>     | UUID | The ID of the execution to get details for.     |
| stepExecutionID<mark style="color:red;">\*</mark> | UUID | The ID of the step execution to get details for |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    "isLargeInput": false,
    "isLargeOutput": false,
    "input": {},
    "output": "Error: no auth mechanism defined"
}
```
{% endtab %}
{% endtabs %}

### Replay workflow execution

<mark style="color:green;">`POST`</mark> `[Base URL]/workflow-executions/:executionID/replay`

Replay a specific workflow execution, using the same version of the workflow that the execution originally ran with.

_This endpoint is in beta and may not be suitable for use in your production application. Please send any feedback you have about this endpoint to_ [_support@useparagon.com_](mailto:support@useparagon.com)_!_

#### Path Parameters

| Name                                          | Type | Description                                 |
| --------------------------------------------- | ---- | ------------------------------------------- |
| executionID<mark style="color:red;">\*</mark> | UUID | The ID of the execution to get details for. |

{% tabs %}
{% tab title="201: Created" %}
```javascript
{
    "id": "fad76415-78a0-4fa0-9590-6c0f8d0b1501",
    "userId": "74174185285246519745612784512874512",
    "workflowId": "9024fa58-982a-45d3-8573-b6a9eae4d769",
    "status": "EXECUTING",
    "dateStarted": "2023-04-21T16:30:00.060Z"
}
```
{% endtab %}
{% endtabs %}
