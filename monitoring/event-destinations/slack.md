---
description: Send notifications from your Paragon project into Slack.
---

# Sending Events to Slack

You can configure a Webhook Destination with a preconfigured payload to send messages into Slack when events, like workflow failures, occur in your Paragon project.

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Webhook Destinations are available for Paragon customers on Pro and Enterprise plans.** To learn more, contact your Customer Success Manager or [sales@useparagon.com](mailto:sales@useparagon.com).
{% endhint %}

## Configure Slack

To send notifications to Slack, you will need to create a Slack App and add it to your workspace with an Incoming Webhook:

1. Visit the [Slack API Center](https://api.slack.com/) and **Create an app.**
2. When prompted to create a new app, click "From scratch". Enter a recognizable name like "Paragon" for the App Name and select your Slack Workspace.
3. Under **Features**, navigate to **Incoming Webhooks**. Turn on "Activate Incoming Webhooks".
4. Once Incoming Webhooks is activated, scroll to the bottom and click "Add New Webhook to Workspace".
5. When prompted, select a channel to send your Slack notifications to. We recommend creating a new channel for Paragon notifications. Click **Allow**.
6. Once the webhook is created, click **Copy** in the Webhook URL and save this value to add to Paragon. The value will begin with "https://hooks.slack.com/..."

## Create Event Destination

_To create an Event Destination with Slack, you will need to have followed the above steps to obtain a **Slack Webhook URL.**_

1. From the Settings > Monitoring page, click the **Add Destination** button at the top right.
2. In the **Type** field, select **Webhook (HTTP Request).**
3. Click "Select Template" next to **Request Payload** and select **Slack**.
4. In the **URL** field, paste the Webhook URL you copied in the previous steps.
5. Click **Test Webhook** to verify that a message gets sent into the Slack channel you selected earlier.
6. Click **Save** to create and enable the Event Destination.

