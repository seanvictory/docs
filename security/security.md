---
description: Paragon's Security and Change Management Procedures.
---

# Security

## Overview

This document outlines some of​ ​[Paragon's​](https://www.useparagon.com/) security practices and architecture.

### Contact

* **Chief Technology Officer:** ​ Ishmael Samuel ([ishmael@useparagon.com](mailto:ishmael@useparagon.com))
* **Data Protection Officer:** ​ Ishmael Samuel ([ishmael@useparagon.com](mailto:ishmael@useparagon.com))
* **Support:** ​ [support@useparagon.com](mailto:support@useparagon.com)
* **Privacy:** ​ [privacy@useparagon.com](mailto:privacy@useparagon.com)

### Other Resources

* [Privacy Policy](https://www.useparagon.com/privacy)
* [Terms of Service](https://www.useparagon.com/terms-of-service)

## Policy Compliance

### Data Protection Agreement

We have a Data Protection Agreement (DPA) that can be requested and signed as a formal agreement between us and customers that require it. It outlines our obligations and procedures. It is reviewed once a quarter and updated as needed.

Our appointed Data Protection Officer is responsible for reviewing that it is up to date and its procedures are followed. Any customer can request a copy of the document by emailing privacy@useparagon.com. This is outlined in [our​ ​GDPR documentation](gdpr.md).

### Policy Coverage

* Third-Party Connectivity
* Data Privacy
* Access Control
* Encryption Standards

## Security

### Physical and Environment Security

We do not manage any physical servers or data centers. Our data is stored in AWS Cloud. Logs are maintained for access to data and stored in AWS CloudWatch. AWS was selected for our cloud provider due to their large foothold in the market. All incoming traffic is logged.

### Access to Data

We have separate AWS accounts for our sandbox and live environments. The sandbox environment is available to all of our engineers (with authentication) while the live environment requires separate logins and additionally requires connecting from a whitelisted IP.

Any engineer needing to connect to the live environment must request access with a reason and their IP address to be temporarily allowed into the live environment.

### Data Storage & Encryption

Our customers' security is top priority. Third-party credentials for integrations are stored in a distributed vault with encryption keys and encrypted values stored separately. Flow logs are stored independently and secure information is redacted. Emails and password are never logged.

### Security and Staff Training

When onboarding new employees, we follow the principle of least privileged access and manually provision only the necessary logins with the least amount of access possible to conduct their job. We explain what they have access to, why, and the valid use cases to use each service.

We run through our security tools (password vaults, network security, etc) and discuss best practices for information security (storing, retrieving, and sharing secure information, 2FA, etc).

Once familiar with our tooling and procedures, they're brought up to speed on our incident response plan and their role in it in a separate session.

## Change Management

Changes to our environments are done via an automated continuous delivery system. Every change runs through a suite of thousands of unit, integration, and end-to-end tests. We do manual quality assurance, and our CTO code reviews and manually approves each outgoing deployment that goes to the production environment.

Our infrastructure is represented in code and updated through a version-controlled continuous deployment system.

All changes are logged with the author, reviewer, and date-time.

## Incident Management

### Incident Response

We have a rotating support engineer to handle or delegate issues to the necessary parties. Our CTO is responsible for overseeing disaster recovery, and all incidents are documented in our ticket management system with large incidents documented via a formal Post Mortem.

### Security Incidents

When a security incident is detected, we immediately notify the entire engineering and management team and prioritize it as a Priority 0 (meaning once assigned, a responsible engineer drops whatever they're doing and immediately begins work on resolution).

Once the engineering team is notified, an engineer claims it or is assigned it by management and becomes the responsible engineer. The response time to date from detection to assignment for all P0s to date has been < 5 minutes.

The first step the responsible engineer takes is to determine the cause of the issue, a preliminary scope of impacted services and users, and the threat level. If one or more users are actively unable to use the service or at risk of secure information being leaked, then work continues and any other necessary parties are notified to help resolve the issue if needed.

Once the preliminary scope and severity has been assessed, a plan for containment and resolution is proposed, shared with the engineering team for any asynchronous feedback and work begins immediately. Our continuous integration & deployment system allows the responsible engineer to build, test and deploy their changes to test environments, and the CTO manually code reviews and approves all changes before they're sent to our live servers.

After resolution, a more thorough assessment of impacted services and users is conducted and a Post Mortem is written with a brief overview, the cause of the issue, impacted services and users, duration of the event, how we resolved it, and steps being taken to prevent the issue from happening again.

If one or more users are impacted by downtime or a breach, the Post Mortem is made public and sent to all parties affected within 1 business day (usually same day). All business and enterprise users share a Slack channel with us, so they're usually notified at the start of an event and updated throughout the process. Naturally, no enterprise users have had a security breach to date by nature of running Paragon in their own network.

## Whitelisting IPs

If needed, you can whitelist the following Paragon IP addresses to ensure requests to your platform are only being made from Paragon.

* `18.205.92.162`
* `18.215.215.164`
* `34.225.59.94`
* `44.210.155.28`
* `52.45.12.206`
* `54.235.127.238`
