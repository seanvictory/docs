# @useparagon/core

## Triggers

### CronStep

Use `CronStep` to start the workflow on a periodic schedule. [#scheduler](../../workflows/triggers/#scheduler "mention")

**Inputs**

<table><thead><tr><th width="218">Parameter</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>cron</code></td><td>string*</td><td>The cron expression of the schedule for this trigger, from seconds to weeks.<br><br><strong>Example</strong>: <code>0 0 9 * * *</code> (every day at 9:00 AM)</td></tr><tr><td><code>timezone</code></td><td>string</td><td>The timezone to use for the cron expression, expressed as an IANA timezone string. Defaults to <code>America/Los_Angeles</code>.<br><br><strong>Example</strong>: <code>Etc/Universal</code> (UTC)</td></tr></tbody></table>

**Outputs**

The CronStep does not produce any usable output.

### EndpointStep

Use `EndpointStep` to trigger this workflow via an HTTP request. [#request](../../workflows/triggers/#request "mention")

**Inputs**

<table><thead><tr><th width="210">Parameter</th><th width="173">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>allowArbitraryPayload</code></td><td>boolean*</td><td>If true, this Request trigger will accept any type of request.<br><br>If false, this Request trigger will require <code>headerValidations</code>, <code>bodyValidations</code>, and <code>paramValidations</code> to be defined.</td></tr><tr><td><code>headerValidations</code></td><td>HeaderValidation[]</td><td>An array of validations to use on the headers for requests to this Request trigger. This can be used to validate the presence of required headers to inbound requests.<br><br><strong>Example</strong>:<br><code>[{ key: "X-Tasklab-Id", required: true }]</code></td></tr><tr><td><code>bodyValidations</code></td><td>BodyValidation[]</td><td>An array of validations to use on body fields for requests to this Request trigger. This can be used to validate the presence or type of data in the body of inbound requests.<br><br><strong>Example:</strong><br><code>[{ key: "userId", dataType: "STRING", required: true }]</code></td></tr><tr><td><code>paramValidations</code></td><td>ParamValidation[]</td><td>An array of validations to use on the URL parameters for requests to this Request trigger. This can be used to validate the presence of required parameters to inbound requests.<br><br><strong>Example</strong>:<br><code>[{ key: "query", required: true }]</code></td></tr></tbody></table>

**Outputs**

Access the output of a Request trigger with `requestTrigger.output.request`. The below fields are fields of the `.request` property.

<table><thead><tr><th width="221">Field</th><th width="173">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>headers</code></td><td>object</td><td>An object of the HTTP headers received in the request.<br><br>Access these properties in lowercased format, e.g. <code>requestTrigger.output.request.headers['content-type']</code> .</td></tr><tr><td><code>body</code></td><td>any</td><td>An object or string of the HTTP body received in the request.<br><br>The <code>body</code> will be an object when the Content-Type is <code>application/json</code>, <code>multipart/form-data</code>, or <code>application/x-www-form-urlencoded</code>.<br><br>Otherwise, it will be attempted to be parsed as a string or File (see below).</td></tr><tr><td><code>params</code></td><td>object</td><td>An object of the URL parameters received in the request.</td></tr><tr><td><code>file</code></td><td>FileValue | undefined</td><td>If the HTTP body refers to a file, the file contents will be available as a <code>FileValue</code> object. Otherwise, this property will resolve to undefined.</td></tr></tbody></table>

### EventStep

Use `EventStep` to trigger this workflow with an [App Event](../../workflows/triggers/#app-events).

**Inputs**

To construct an App Event Trigger, first import your App Event into the Workflow:

```typescript
import taskCreated from '../../../events/newTask';
```

Then, pass this import to the constructor of `EventStep`:

```typescript
const trigger = new EventStep(taskCreated);
```

Because App Events can be shared across different workflows and integrations, they are required to be defined in the `src/events` folder of your Paragraph project.

**Outputs**

Access the output of an App Event trigger with `appEventTrigger.output`. The output will match the schema of the App Event that this trigger uses.

### IntegrationEnabledStep

Use `IntegrationEnabledStep` to trigger this workflow when a user enables the integration.

**Inputs**

This trigger does not use any parameters.

**Outputs**

The IntegrationEnabledStep does not produce any usable output.

## Steps

### ConditionalStep

A Conditional branching step to allow for control flow in Workflows.

**Inputs**

<table><thead><tr><th width="218">Parameter</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>if</code></td><td>ConditionalInput*</td><td>The condition to evaluate for determining whether or not to proceed into the "true" or "false" branch beneath this step.<br><br>Learn more about defining ConditionalInputs: <a data-mention href="../defining-workflows.md#conditional-logic">#conditional-logic</a></td></tr></tbody></table>

**Outputs**

<table><thead><tr><th width="218">Parameter</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>selectedChoice</code></td><td><code>"Yes" | "No"</code></td><td>The branch that was chosen when this ConditionalStep was evaluated.</td></tr></tbody></table>

### DelayStep

A step to pause the workflow for a fixed amount of time.

**Inputs**

<table><thead><tr><th width="218">Parameter</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>value</code></td><td>number*</td><td>How long to pause the workflow for, measured by the <code>unit</code> parameter.</td></tr><tr><td><code>unit</code></td><td><code>"SECONDS"</code><br><code>| "MINUTES"</code><br><code>| "HOURS"</code><br><code>| "DAYS"</code></td><td>The unit of time to use when delaying the workflow. Defaults to <code>"MINUTES"</code>.</td></tr></tbody></table>

**Outputs**

The DelayStep does not produce any usable output.

### FanOutStep

A step to map over a set (array) of data in parallel, for e.g. data transformation or batch uploads.

**Inputs**

<table><thead><tr><th width="218">Parameter</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>iterator</code></td><td>any[]</td><td>A set of data to iterate over in the Fan Out.</td></tr></tbody></table>

**Outputs**

Access one instance of a Fan Out step with `fanOutStep.output.instance`. This can only be used by steps that are in this Fan Out's branch (see: [#fan-out-branches](../defining-workflows.md#fan-out-branches "mention")).

<table><thead><tr><th width="218">Field</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>instance</code></td><td>any</td><td>An item of the <code>iterator</code> property that is being processed in this branch. </td></tr></tbody></table>

### FunctionStep

A JavaScript function step.

**Inputs**

<table><thead><tr><th width="218">Parameter</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>code</code></td><td>Function*</td><td>The function to run.<br><br>This function must have the signature<br><code>function(parameters, libraries)</code> and must be <em>self-contained</em>, meaning that it cannot reference JavaScript values outside of the function body.<br><br>To pass execution data through this step, use the <code>parameters</code> object.<br><br>The list of <code>libraries</code> can be found in: <a data-mention href="../../resources/javascript-libraries.md">javascript-libraries.md</a></td></tr><tr><td><code>parameters</code></td><td>object*</td><td>Parameters from other step outputs to inject into the function.</td></tr></tbody></table>

**Outputs**

Access the result of an Function step with `functionStep.output.result`.

<table><thead><tr><th width="218">Field</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>result</code></td><td>any</td><td>The return result of <code>code</code> after evaluation with <code>parameters</code>.<br><br>Note: if <code>code</code> returns a <code>Promise</code>, the Function step will automatically await this Promise and return the unwrapped result.</td></tr></tbody></table>

### IntegrationRequestStep

A step to send a custom request to the integration's API, without needing to provide auth details.

**Inputs**

<table><thead><tr><th width="149">Parameter</th><th width="217">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>method</code></td><td><code>"GET"</code><br><code>| "POST"</code><br><code>| "PATCH"</code><br><code>| "PUT"</code><br><code>| "DELETE"</code>*</td><td>The HTTP method to use for this API request.<br><br>If you select <code>POST</code>, <code>PUT</code>, or <code>PATCH</code> methods, the <code>body</code> and <code>bodyType</code> parameters will be required.</td></tr><tr><td><code>url</code></td><td>string*</td><td>The relative path of the API request, with respect to the base URL provided by the integration.<br><br>Specifying a full URL is also supported.</td></tr><tr><td><code>bodyType</code></td><td><code>"json"</code><br><code>| "form-data"</code><br><code>| "x-www-form-urlencoded"</code><br><code>| "xml"</code><br><code>| "raw"</code></td><td>Select the type of request body that should be sent.<br><br>Paragon will automatically encode the payload and set the correct <code>Content-Type</code> headers.</td></tr><tr><td><code>body</code></td><td>object | string | <code>(pageToken: string) => object | string)</code></td><td>An object or string representing the request body to be sent.<br><br>If using <a href="../../workflows/requests/request-pagination.md">Request Step Pagination</a>, you can specify a function that returns the body of the request with respect to the Page Token.</td></tr><tr><td><code>headers</code></td><td>object | <code>(pageToken: string) => object</code></td><td>An object of the HTTP headers sent in the request. Integration Request Steps will automatically include the user's authentication details for the request.</td></tr><tr><td><code>params</code></td><td>object | <code>(pageToken: string) => object</code></td><td>An object of the URL parameters sent in the request. Parameters can be specified in either here or the <code>url</code> property.</td></tr><tr><td><code>pagination</code></td><td><code>(step) => PaginationOptions</code></td><td><p>If using <a href="../../workflows/requests/request-pagination.md">Request Step Pagination</a>, you can define the options used in this function.<br><br>Use the <code>step</code> parameter of the <code>pagination</code> function to access the output in <br><br><strong>Example</strong>:</p><pre class="language-typescript"><code class="lang-typescript">new IntegrationRequestStep({
  method: "GET",
  url: "/opportunities",
  params: (pageToken) => ({
    pageToken
  }),
  pagination: (step) => {
    return {
      outputPath: step.output.response.body.data,
      pageToken: step.output.response.body.nextPageToken,
      stopCondition: Operators.Or(
        Operators.And(
          Operators.DoesNotExist(step.output.response.body.nextPageToken)
        )
      )
    }
  },
});
</code></pre></td></tr></tbody></table>

**Outputs**

Access the output of an Integration Request step with `requestStep.output.response`.

<table><thead><tr><th width="221">Field</th><th width="173">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>headers</code></td><td>object</td><td>An object of the HTTP headers received in the response.</td></tr><tr><td><code>body</code></td><td>any</td><td>An object or string of the HTTP body received in the response.</td></tr><tr><td><code>statusCode</code></td><td>number</td><td>The HTTP status code of the response.</td></tr></tbody></table>

### RequestStep

A step to send an HTTP request from a workflow.

**Inputs**

<table><thead><tr><th width="149">Parameter</th><th width="217">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>method</code></td><td><code>"GET"</code><br><code>| "POST"</code><br><code>| "PATCH"</code><br><code>| "PUT"</code><br><code>| "DELETE"</code>*</td><td>The HTTP method to use for this API request.<br><br>If you select <code>POST</code>, <code>PUT</code>, or <code>PATCH</code> methods, the <code>body</code> and <code>bodyType</code> parameters will be required.</td></tr><tr><td><code>url</code></td><td>string*</td><td>The full URL of the HTTP request to send.</td></tr><tr><td><code>bodyType</code></td><td><code>"json"</code><br><code>| "form-data"</code><br><code>| "x-www-form-urlencoded"</code><br><code>| "xml"</code><br><code>| "raw"</code></td><td>Select the type of request body that should be sent.<br><br>Paragon will automatically encode the payload and set the correct <code>Content-Type</code> headers.</td></tr><tr><td><code>body</code></td><td>object | string</td><td>An object or string representing the request body to be sent.</td></tr><tr><td><code>headers</code></td><td>object</td><td>An object of the HTTP headers sent in the request.</td></tr><tr><td><code>params</code></td><td>object</td><td>An object of the URL parameters sent in the request. Parameters can be specified in either here or the <code>url</code> property.</td></tr><tr><td><code>authorization</code></td><td>AuthorizationConfig</td><td><p>Choose between Basic authentication, Bearer token authentication, and OAuth 2.0 Client Credentials for handling the authorization of this request.<br><br><strong>Example:</strong></p><pre class="language-typescript"><code class="lang-typescript">new RequestStep({
  method: 'GET',
  url: 'https://myapp.io/api',
  authorization: {
    type: 'basic',
    username: 'paragon-user',
    password: context.getEnvironmentSecret("API_SECRET"),
  },
});
</code></pre></td></tr></tbody></table>

**Outputs**

Access the output of a Request step with `requestStep.output.response`.

<table><thead><tr><th width="221">Field</th><th width="173">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>headers</code></td><td>object</td><td>An object of the HTTP headers received in the response.</td></tr><tr><td><code>body</code></td><td>any</td><td>An object or string of the HTTP body received in the response.</td></tr><tr><td><code>statusCode</code></td><td>number</td><td>The HTTP status code of the response.</td></tr></tbody></table>

### ResponseStep

A step (_for use in Request-triggered workflows only_) to send an HTTP response from a workflow.

**Inputs**

<table><thead><tr><th width="218">Parameter</th><th width="168">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>responseType</code></td><td><code>"JSON" | "FILE"</code>*</td><td>The type of Response to send to the HTTP Request that triggered the workflow. Choose between a JSON-encoded response or a raw File type.</td></tr><tr><td><code>body</code></td><td><code>object | FileValue</code>*</td><td>If using a JSON <code>responseType</code>, provide an object to send in the response.<br><br>If using a File <code>responseType</code>, provide a <code>FileValue</code> to send in the respnose.</td></tr><tr><td><code>statusCode</code></td><td><code>number</code>*</td><td>The status code to send in the Response to the HTTP Request that triggered the workflow.</td></tr></tbody></table>

