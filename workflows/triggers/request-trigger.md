# Request Trigger

The Request trigger can be used to run workflows by sending it an **HTTP request or webhook**. Request triggers allow passing data from the incoming HTTP request into the workflow.

* **Example:** when a lead is created in your app, send lead data to your customer's CRM and provide a custom response upon success.

Request triggers can also be used to create API Endpoints that send synchronous results back to your app. For more about sending results, see [#sending-a-response](request-trigger.md#sending-a-response "mention").

* **Example:** expose an endpoint that gets called by your app to pull contacts from their CRM.

![](<../../.gitbook/assets/Using the Request Trigger in Paragon Connect.png>)

Request-triggered workflows can be triggered by sending an HTTP `POST` request to their unique URL. You can manually enter the expected query parameters (Params), headers (Headers), and body parameters (Body) to use as variables by other steps in the workflow.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
// Called once during your user's session 
paragon.authenticate("project-id", <Paragon User Token>)

// Trigger the "Lead Created" workflow
await paragon.workflow("<workflow_id>", {
  "query": {
    },
  "headers": {
    "Content-Type": "application/json"
  },
  "body": {
    "email": "bowie@useparagon.com",
    "first_name": "Bowie",
    "last_name": "Foo"
  }
});
```
{% endtab %}

{% tab title="REST API" %}
```
// Trigger the "Lead Created" Workflow
POST https://zeus.useparagon.com/projects/<Paragon Project ID>/sdk/triggers/<Workflow ID>

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Body
{
  "email": "bowie@useparagon.com",
  "first_name": "Bowie",
  "last_name": "Foo
}
```
{% endtab %}
{% endtabs %}

### Defining Test Data

There are two ways to define what data you expect to be sent by incoming requests to the workflow:

* **Manually entering the expected request data**
* **Automatically detecting data by sending a test request**

**Manually entering request data** is usually the best option if you know what data will be sent by the incoming request (e.g. you're sending it from your own app). This option allows you to manually enter the expected query parameters (Params), headers (Headers), and body parameters (Body). Any data entered here can be used as variables by other steps in the workflow.

![](<../../.gitbook/assets/Manually Entering Request Data in Paragon.gif>)

You can also choose to validate the incoming request data. For example, you can enforce that query parameters should be required, that headers should match an expected value, or that body parameters should match an expected type. If the incoming request doesn't meet your workflow's validation rules, the workflow will automatically return an error response.

**Automatically detecting data from a test request** is usually the best option if you have a large amount of data to pass through. When you choose this option, the test shelf will appear and display a test URL at the bottom of the step sidebar. By sending a request to the test URL, Paragon will automatically detect data from the request and display it in the test shelf. Here, it'll be saved as test data that can be used as variables by other steps in the workflow.&#x20;

![](<../../.gitbook/assets/Testing a trigger in Paragon.gif>)

Once you're ready to start using a Request workflow in production, click the "Deploy" button in the top-right of the screen to deploy the workflow. This will set the workflow's endpoint URL live and make it available for requests to be sent to.

## Sending a Response

Request-triggered workflows support sending a custom response to the original HTTP request that triggered the workflow.

{% hint style="info" %}
**Note**:

* If your Request-triggered workflow does not require a custom response, your workflow will respond immediately upon request with 202 Accepted.
* When using a custom response, your workflow will have a limit of 55 seconds to reach the Response step. If your workflow may potentially run longer, you will need to handle timeout errors. See [#response-time-limitations](request-trigger.md#response-time-limitations "mention") below for more details.
{% endhint %}

To add a response to your workflow, click the "+" button in the workflow canvas and choose the Response step in the sidebar.

![](<../../.gitbook/assets/Using Responses in Paragon Connect.png>)

### Defining response data

There are two components to a Response: its status code and its data.

In general, you should send the `200: OK` status code if the workflow ran successfully, you can choose from other commonly used status codes for more specific cases (e.g. if a Request failed, send an error response).

You can choose what data to send the response body using the key-value table to reference data from previous steps in the workflow.

### Sending files in responses

You can use the Response step to send files to your application. To do so, select "File" as the Response Type and reference a File object from a previous step.

File objects are returned from file-related Integration Actions and Request steps which include a file in the response.

<figure><img src="../../.gitbook/assets/[Paragon] 2024-09-24 at 11.58.04 AM@2x.png" alt=""><figcaption></figcaption></figure>

A File Response will be returned to the original HTTP request with the `Content-Type` of the file's MIME type and the raw bytes of the underlying file.

### Response time limitations

When using a custom response, your workflow will have a limit of 55 seconds to reach the Response step. If your workflow does not reach the Response step in that time, the HTTP request will respond with a **542 status code** to indicate a response timeout.

A 542 status code _does not indicate_ that your workflow was unsuccessful; your workflow may still be running, but the results were not processed in time to provide a synchronous response. The timeout response will be returned as a JSON body which includes the workflow execution ID for your reference.

You can use this ID to retrieve results using the [Task History API](../../api/task-history.md) or to view results in the dashboard's [Task History view](../../monitoring/viewing-task-history.md).

* Link to view execution in Task History: `https://dashboard.useparagon.com/connect/projects/[Project ID]/history/workflows/[Workflow ID]/executions/[Workflow Execution ID]`

**Example timeout response**

```json
{
    "message": "Workflow has been enqueued but has not completed.",
    "dateSubmitted": "2024-09-24T01:07:13.658Z",
    "projectId": "...",
    "workflowId": "...",
    "executionId": "..."
}
```
