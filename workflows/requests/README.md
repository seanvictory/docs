---
description: Making HTTP requests with Paragon
---

# Making API Requests

## Overview

You can make requests to any HTTP API using Paragon's Request step. This is useful for connecting workflows to your application's internal API, or with any REST APIs in general.

To provide a common use case, let's say you want to receive real-time data (webhooks) from your users' apps - for example, whenever new Salesforce contacts are created. You can accomplish this with a Workflow that's triggered by new records in Salesforce, then using a Request step to POST the new Salesforce records to your application's API.

![](<../../.gitbook/assets/image (39).png>)

## Making a Request

To add a request to your workflow, click the "+" button in the workflow canvas and choose the Request step from the sidebar. You can follow familiar specifications to setup requests in Paragon:

* URL&#x20;
* Request type
  * `POST`
  * `GET`
  * `PATCH`
  * `PUT`
  * `DELETE`
* Request data
  * Query parameters
  * Headers
  * Body parameters
    * `JSON`
    * `multipart/form-data`
    * `x-www-form-urlencoded`
    * `Raw`
  * Authorization
    * `Bearer Token`
    * `Basic Auth`

### Configuring your Request URL

You can enter the request URL in the input under "**Request URL"**. You can also include parameters as part of the URL by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Including parameters in a URL request in Paragon.png>)

The **variable menu** allows you to reference data from upstream steps in your request URL. For example, we can pass a `userId` from the Trigger into the request URL, which is represented as: `/users/{{1.event.userId}}`

### Sending data in a request

Query parameters, headers, and body parameters can be included in the request by adding them in the key-value table under their respective heading.

![](<../../.gitbook/assets/Sending a JSON request in Paragon.gif>)

When using the key-value table, you can type in **static values** or **reference variables** from upstream steps by invoking the variable menu using the dropdown button.

### Sending JSON in a request

You can easily send JSON in a request by choosing `Raw` in the dropdown to the right of Body. When creating the raw JSON body, you can type in **static values** or **reference variables** from upstream steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Sending nested JSON through a Request step in Paragon.png>)

### Sending File Data in a request

You can send file data in a request by adding a `X-Paragon-Encoding` header. The encoding should be set to encoding used in the file, like `hex`.&#x20;

<figure><img src="../../.gitbook/assets/Sending files to your application in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

### Handling request failures

You can choose whether or not the workflow should continue to the next step if the request fails under "Continue workflow if request fails". This option is useful if you want to conditionally handle request failures. You can do this by adding a Conditional step after the Request step, then referencing the request's response status code in the Conditional.

![](<../../.gitbook/assets/Handling request failures with a conditional step in Paragon.png>)

## Making an Integration Request

Like the Request step, the **Integration Request** is a per-integration step that allows you to make HTTP calls to any endpoint the integration supports. This means you can access actions that aren't yet supported natively by Paragon.

<figure><img src="../../.gitbook/assets/Using the Integration Request step for Slack in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

### Configuring the Authentication

We've got you covered! You can leave out the authentication piece to connect to your integration's API since you've connected using Paragon. We prefix the URL of each integration, so you only have to enter the API endpoint and any parameters.&#x20;

### Replacing the Base URL

If you need to overwrite the default base URL Paragon provides for any request you make to the integration provider, you can do so by typing `https://` in the input followed by the rest of the URL.

<figure><img src="../../.gitbook/assets/Replacing the Base URL for an integration in Paragon Connect.gif" alt=""><figcaption></figcaption></figure>
