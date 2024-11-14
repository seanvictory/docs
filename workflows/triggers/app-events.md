# App Events

App Events are custom events that are sent programmatically from your application via the Paragon SDK or API to trigger Workflows. In general, App Events are useful for triggering workflows that map data from your application to your users' apps.

For example, you might send a "Contact Created" App Event from your application to trigger a Workflow that creates a matching contact in your users' Salesforce CRM.

**Once defined, an App Event can be used to trigger multiple workflows.** This is useful in cases where you may want the same event to trigger similar workflows across different integrations.

For example, the same "Contact Created" event in the above example could trigger one workflow that creates a contact in Salesforce, and another workflow that creates a contact in HubSpot. This allows you to easily provide the same integration functionality across different providers without any additional engineering.

![](<../../.gitbook/assets/Using an App Event for multiple workflows in Paragon.png>)

### Creating an App Event

To create an App event, select the **App Event** trigger type in the Workflow editor and choose "Create new app event" in the menu under **Choose an App Event**.

Next, enter the name and event schema of your App Event. The **event schema** that you enter here should be an example payload sent from your application to Paragon. The event schema defined here will be used as test data for any workflows triggered by this App Event.

{% hint style="info" %}
The **event schema** must be a valid JSON object, and can contain any arbitrary JSON.
{% endhint %}

![](<../../.gitbook/assets/Screen Shot 2021-02-15 at 12.51.29 PM.png>)

### Sending an App Event

App Events can be sent from your application using the Paragon SDK or REST API. In both cases, you must pass two parameters:

* **name** - the event name defined in your App Event
* **payload** - the event payload that should match the event schema defined in your App Event

See the code examples below for how to send App Events using the Paragon SDK or API.

{% tabs %}
{% tab title="JavaScript SDK" %}
```javascript
var eventName = "Contact Created";
var eventPayload = { "name": "Brandon", "email": "b@useparagon.com" };

// Called once during your user's session 
paragon.authenticate("project-id", <Paragon User Token>)

// Trigger the "Contact Created" App Event
paragon.event(eventName, eventPayload)
```
{% endtab %}

{% tab title="REST API" %}
```http
// Trigger the "Contact Created" App Event
POST https://api.useparagon.com/projects/<Paragon Project ID>/sdk/events/trigger

Authorization: Bearer <Paragon User Token>
Content-Type: application/json

// Body
{ 
    "name": "Contact Created", 
    "payload": { 
        "name": "Brandon", 
        "email": "b@useparagon.com" 
    } 
}
```

{% hint style="info" %}
**Note:** You'll receive a `201` response code as confirmation that your event has been successfully received. This is due to the one-to-many nature of these triggers, which means Paragon cannot simultaneously provide all potential responses from the various workflows your event may initiate.
{% endhint %}
{% endtab %}
{% endtabs %}

Paragon sends a `201` response and does not validate event payloads against the defined schema when your application sends live events, regardless of whether they trigger any workflows.

### Managing App Events

If you need to edit your App Events' name or event schema, you can visit the App Events tab in your Paragon dashboard to view and manage your app events.

![](<../../.gitbook/assets/Managing App Events in Paragon.png>)
