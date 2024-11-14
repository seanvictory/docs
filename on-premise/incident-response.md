# Incident Response

## Overview

For managed installations, we have hundreds of metrics being constantly collected with alarms configured to alert Paragon’s support team upon deviations or when dangerous values are detected. You can learn more [here](system-metrics-and-alarms.md).

{% content-ref url="system-metrics-and-alarms.md" %}
[system-metrics-and-alarms.md](system-metrics-and-alarms.md)
{% endcontent-ref %}

We proactively respond to deviations and often remediate misconfigurations, and errors, and optimize costs before customers or their users are made aware.

If you detect issues with your environment, please contact our team, and we’ll prioritize fixing and patching your environment as soon as possible.

### Underutilization of resources

When resources are consistently underutilized, we’ll handle the downsizing of resources (e.g. Postgres, Redis, etc) to save you money on your monthly bill.

### More resources needed

When not enough resources are available (e.g. servers, database memory or CPU, etc), there are several courses of action that we take. In almost every case, we’re notified within seconds of a lack of resources within a managed installation. In most of those cases, we have autoscaling enabled within predefined limits to meet the demand. If we need to resize a service that would materially affect monthly costs, we’ll notify your team and request approval to update the configuration for your installer to update your system.

### High error rates

When high error rates are detected, we’ll immediately investigate the source of error rates and take the appropriate action. In many cases, it’s a new workflow that’s being tested or misconfigured, and no action is needed.

Generally, releases are tested in our cloud environment and confirmed to be stable before deploying to enterprise environments, so rollbacks due to high error rates in on-premise environments rarely happen.

### Hacks / Exploited Systems

If an exploit has been detected by our team, your team will be notified immediately and a Paragon response team will be formed. If you become aware of an exploit, please notify us immediately, and we’ll take care of patching and updating your system immediately.

### System downtime

Every microservice is configured with horizontal pod scalers, services, and health checks to enforce uptime. If services are regularly going offline due to high load or a lack of resources, please report it to the support team, and we’ll make sure to investigate and optimize your installation.

### General bugs

If you find a bug or regression within your installation, please report it to the support team, and we’ll prioritize patching and updating your system as soon as possible.
