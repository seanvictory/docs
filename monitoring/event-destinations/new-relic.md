---
description: Send notifications from your Paragon project into New Relic.
---

# Sending Events to New Relic

You can configure a Webhook Destination with a preconfigured payload to send messages into New Relic when events, like workflow failures, occur in your Paragon project.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Webhook Destinations are available for Paragon customers on Pro and Enterprise plans.** To learn more, contact your Customer Success Manager or [sales@useparagon.com](mailto:sales@useparagon.com).
{% endhint %}

## Configure New Relic

To send notifications to New Relic, you will need to add an API Key to your New Relic project:

1.  In the bottom right menu of your New Relic account, navigate to **API Keys.**

    <figure><img src="../../.gitbook/assets/Frame 1 (11).png" alt=""><figcaption></figcaption></figure>


2. Click **Create Key** and specify "Ingest - License" for the key type. Name the key something recognizable, like "Paragon".
3. Click the "..." menu next to the new key and click **Copy Key**. You will need this value to add the Event Destination below.

## Create Event Destination

_To create an Event Destination with New Relic, you will need to have followed the above steps to obtain a **New Relic API Key.**_

1. From the Settings > Monitoring page, click the **Add Destination** button at the top right.
2. In the **Type** field, select **Webhook (HTTP Request).**
3. Click "Select Template" next to **Request Payload** and select **New Relic**.
4. In the **Request Headers** table, replace `<New Relic API Key>` with your **New Relic API Key**.
5. Click **Test Webhook** to verify that a log can be sent successfully to your New Relic instance.
6. Click **Save** to create and enable the Event Destination.
