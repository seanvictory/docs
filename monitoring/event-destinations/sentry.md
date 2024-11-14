---
description: Send notifications from your Paragon project into Sentry.
---

# Sending Events to Sentry

You can configure a Webhook Destination with a preconfigured payload to send messages into Sentry when events, like workflow failures, occur in your Paragon project.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Webhook Destinations are available for Paragon customers on Pro and Enterprise plans.** To learn more, contact your Customer Success Manager or [sales@useparagon.com](mailto:sales@useparagon.com).
{% endhint %}

## Configure Sentry

To send notifications to Sentry, you will need to make note of your Sentry Public Key and Sentry Ingest URL.

1.  From your Sentry Project, click the Settings gear icon on the top right.

    <figure><img src="../../.gitbook/assets/Screen Shot 2022-11-15 at 4.04.06 PM.png" alt=""><figcaption></figcaption></figure>
2. Under the **SDK Setup** section, click **Client Keys (DSN)**.
3.  Copy your DSN. You will need to extract your Sentry Public Key and Sentry Ingest URL from this value:

    <figure><img src="../../.gitbook/assets/Frame 1 (12).png" alt=""><figcaption></figcaption></figure>

    Once you identify the Sentry Base URL, perform the following steps to get your Sentry Ingest URL:

    1. Prefix the base URL with **"https://"**
    2. After ".sentry.io/" and before the Project ID path, add **"api/"** to the URL. For example, with the above DSN, this would become: `https://o535635.ingest.sentry.io/api/4504082601017344`
    3. At the end of the URL, add **"/store/"**. The final Sentry Ingest URL should look like: `https://o535635.ingest.sentry.io/api/4504082601017344/store/`
    4. Save this value to use as your Sentry Ingest URL.

## Create Event Destination

_To create an Event Destination with Sentry, you will need to have followed the above steps to obtain a **Sentry Public Key and Sentry Ingest URL.**_

1. From the Settings > Monitoring page, click the **Add Destination** button at the top right.
2. In the **Type** field, select **Webhook (HTTP Request).**
3. Click "Select Template" next to **Request Payload** and select **Sentry.**
4. In the **URL** field, paste your **Sentry Ingest URL.**
5. In the **Request Headers** table, replace `<Sentry Key>` with your **Sentry Public Key**.
6. Click **Test Webhook** to verify that an error can be sent successfully to your Sentry project.
7. Click **Save** to create and enable the Event Destination.
