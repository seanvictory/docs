---
description: >-
  Send notifications from your Paragon project into your logging, analytics, and
  APM services.
---

# Managing Event Destinations

{% hint style="info" %}
**Note:** This feature is only available to **Admin** users. [Learn more](../../managing-account/teams.md#managing-roles-and-permissions).
{% endhint %}

Event Destinations allow you to configure notifications for events that occur in your Paragon project.

For example, if you'd like to add another email to be notified by email when a workflow fails, you can add an Email Destination. If you prefer notifications via Slack, you can configure a Webhook Destination to a Slack incoming webhook.

You can find your project's Event Destinations by navigating to the global **Settings** tab in the left sidebar and selecting **Monitoring** under your Project Settings.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

From this Monitoring page, you can take any of the following actions for any Event Destination:

* Update the configuration of the Event Destination (such as changing the email address or webhook URL)
* Disable the Event Destination, which temporarily pauses notifications sent to this destination
* Delete the Event Destination

## Email Destinations

By default, your project will include an Email Destination for Workflow Failure events, using the email address of the user that created the project.

<figure><img src="../../.gitbook/assets/Frame 1 (14).png" alt=""><figcaption></figcaption></figure>

You can set up additional Email Destinations by following these steps:

1. From the Settings > Monitoring page, click the **Add Destination** button at the top right.
2. In the **Type** field, select **Email.**
3. In the **To** field, enter the desired email to be notified.
4. Optionally, send a test email with the **Test Email** button at the bottom left.
5. Click **Save** to create and enable the new destination.

## Webhook Destinations

{% hint style="info" %}
**Webhook Destinations are available for Paragon customers on paid plans.** To learn more, contact our team at [sales@useparagon.com](mailto:sales@useparagon.com).
{% endhint %}

Webhook Destinations allow you to receive event notifications from your Paragon project via HTTP requests. Webhook Destinations will receive a POST request when the event occurs, with configurable request headers and body contents.

<figure><img src="../../.gitbook/assets/Frame 1 (15).png" alt=""><figcaption></figcaption></figure>

### Setup from template

If you use Slack, Datadog, New Relic, or Sentry, you can configure a Webhook Destination by clicking "Select Template" under **Request Payload** and following the guide to configure below:

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><a href="slack.md"><strong>Slack</strong></a></td><td>Send events as messages in Slack</td><td></td></tr><tr><td><a href="datadog.md"><strong>Datadog</strong></a></td><td>Send events as logs in Datadog</td><td></td></tr><tr><td><a href="new-relic.md"><strong>New Relic</strong></a></td><td>Send events as logs in New Relic</td><td></td></tr><tr><td><a href="sentry.md"><strong>Sentry</strong></a></td><td>Send events as issues in Sentry</td><td></td></tr></tbody></table>

### Setup manually

You can set up a Webhook Destination by following these steps:

1. From the Settings > Monitoring page, click the **Add Destination** button at the top right.
2. In the **Type** field, select **Webhook (HTTP Request).**
3. In the **URL** field, enter the desired URL to receive the event payload.
4. Optionally, in the **Request Payload** field, you can change the format of the payload. By default, the webhook will receive the full event object (`$.event`). Use `{{` to specify a part of the event data to use in the request payload.\
   ![](<../../.gitbook/assets/Kapture 2022-11-15 at 17.35.15.gif>)
5. Optionally, additional request headers can be specified by expanding "Show more request options".
6. Send a test request to your Webhook Destination by clicking **Test Webhook** button at the bottom left.
7. Click **Save** to create and enable the new destination.

{% hint style="info" %}
**Note:** Your Webhook Destination may be automatically disabled if your webhook responds with too many non-2xx status codes for consecutive events.
{% endhint %}

## Supported Events

At this time, the following events can be sent from your Paragon project:

* **Workflow Failure**
* **Credential Failure**

We are working on adding support for more events. Have a request for other events you'd like to send from your Paragon project? [Let us know](mailto:team@useparagon.com).

