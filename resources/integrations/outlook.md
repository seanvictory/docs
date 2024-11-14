# Microsoft Outlook

## Setup Guide

You can find your Microsoft Outlook application credentials by visiting your Microsoft Azure Portal.

You'll need the following information to set up your Microsoft Outlook app with Paragon Connect:

* Client ID
* Client Secret
* Scopes Requested

### Prerequisites

* A [Microsoft Azure](https://azure.microsoft.com/) account

### Add the Redirect URL to your Microsoft Outlook app

Paragon provides a redirect URL to send information to your app. To add the redirect URL to your Microsoft Outlook app:

1\. Copy the link under "**Redirect URL**" in your integration settings in Paragon. The Redirect URL is:

```
https://passport.useparagon.com/oauth
```

2\. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/) using your Microsoft account.

3\. Navigate to **All Services > App Registrations** and select your application.

4\. Select **Authentication** from the sidebar.

5\. Under **Platform configurations**, press the  **"Add a platform"** button.

6\. Select the **Web** platform.

7\. Paste the Redirect URL from Step 1 under Redirect URIs.

8\. Press the **Save** button at the top of the page.

### Generate a Client Secret

Since Microsoft Outlook does not automatically provide you with a Client Secret for your application, we'll need to make one. To get your Client Secret:

1\. Navigate to **Manage > Certificates & secrets** in the sidebar.

2\. Under **Client Secrets**, press the **+ New client secret** button.&#x20;

3\. Name your client credentials and select an expiry that works best for your application. Press **Add** to create your credentials.

4\. Copy the displayed Client Secret under the **Value** column.

{% hint style="info" %}
**Note:** You will need to periodically create new and update your Client Secret as they expire for all Microsoft integrations.
{% endhint %}

### Enable Multi-tenancy to your Outlook app

To allow Microsoft users from outside of your organization to connect to your Outlook application, you must specify this as an option within the Outlook application registration.

1. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/) using your Microsoft account.
2. Navigate to **All Services > App Registrations** and select your application.
3. Select **Authentication** from the sidebar.
4. Under **Supported account types**, press the  **"Accounts in any organizational directory"** option.
5. Click Save.

### Add your Microsoft Outlook app to Paragon

1\. Select **Microsoft Outlook** from the **Integrations Catalog**.

2\. Under **Integrations > Connected Integrations > **_**{YOUR\_APP}**_** >** **Settings**, fill out your credentials from the end of [Step 1](outlook.md#add-the-redirect-url-to-your-microsoft-outlook-app) in their respective sections:

* **Client ID:** Found under **Essentials > Application (client) ID** on your Microsoft Azure Portal app page.
* **Client Secret:**
  1. Log in to the [Microsoft Azure Portal](https://azure.microsoft.com/).
  2. Navigate to **Manage > Certificates & secrets** in the sidebar.
  3. Under **Client Secrets**, press the **+ New client secret** button.&#x20;
  4. Name your client credentials and select an expiry that works best for your application.
  5. Press **Add** to create your credentials.
  6. Copy the displayed Client Secret under the **Value** column.
* **Permissions:** Select the scopes you've requested for your application.

Press the blue "**Connect**" button to save your credentials.

{% hint style="info" %}
**Note:** You should only add the scopes you've requested in your application page to Paragon.
{% endhint %}

![](<../../.gitbook/assets/Connecting a Microsoft Outlook application to Paragon Connect.png>)

## Connecting to Microsoft Outlook

Once your users have connected their Microsoft Outlook account, you can use the Paragon SDK to access the Microsoft Outlook API on behalf of connected users.

See the Microsoft Outlook [REST API documentation](https://docs.microsoft.com/en-us/graph/api/resources/calendar?view=graph-rest-1.0) for their full API reference.

Any Microsoft Outlook API endpoints can be accessed with the Paragon SDK as shown in this example:

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);

// Get user's calendar events
await paragon.request("outlook", "/me/calendar/events", { 
  method: "GET",
});

// Get messages in user’s mailbox
await paragon.request("outlook", "/me/messages", {
  method: "GET",
});

// Create a calendar event
await paragon.request("outlook", "/me/calendar/events", {
  method: "POST",
  body: {
    "subject": "Let's go for lunch",
    "body": {
      "contentType": "HTML",
      "content": "Does mid month work for you?"
    },
    "start": {
      "dateTime": "2019-03-15T12:00:00",
      "timeZone": "Pacific Standard Time"
    },
    "end": {
      "dateTime": "2019-03-15T14:00:00",
      "timeZone": "Pacific Standard Time"
    },
    "location":{
      "displayName":"Harry's Bar"
    },
    "attendees": [
      {
        "emailAddress": {
          "address":"adelev@contoso.onmicrosoft.com",
          "name": "Adele Vance"
        },
      "type": "required"
      }
    ]
}
});

```

## Building Microsoft Outlook workflows

Once your Microsoft Outlook account is connected, you can add steps to perform the following actions:

* Create Event
* Update Event
* Get Event by ID
* Get Events
* Delete Event
* Get Messages
* Send Message

When creating or updating events in Microsoft Outlook, you can reference data from previous steps by typing `{{` to invoke the variable menu.

![](<../../.gitbook/assets/Creating a Microsoft Outlook workflow in Paragon Connect.png>)

## Using Webhook Triggers

Webhook triggers can be used to run workflows based on events in your users' Microsoft Outlook accounts. For example, you might want to trigger a workflow whenever new events are created Microsoft Outlook to sync your users' Microsoft Outlook events to your application in real-time.

![](<../../.gitbook/assets/Microsoft Outlook triggers in Paragon Connect.png>)

You can find the full list of Webhook Triggers for Microsoft Outlook below:

* **Event Created**
* **Event Updated**
* **New Message**
