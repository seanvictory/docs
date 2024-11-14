---
description: Assign roles to team members working together on Paragon.
---

# Role-Based Access Control

Role-Based Access Control allows you to give team members different levels of visibility to your Paragon projects. For example, you can:

* Assign support team members with **Support** roles for access to the Connected Users and Task History pages _only_
* Designate specific users with **Admin** roles to manage global settings, including team member access and billing information

We recommend giving team members the minimal level of access they need, according to the principle of least privilege.

{% hint style="info" %}
**Role-Based Access Control is available for Paragon customers on Enterprise plans.** To learn more, contact your Customer Success Manager or [sales@useparagon.com](mailto:sales@useparagon.com).

_Admin and Member roles are available for customers on all plans. See_ [teams.md](teams.md "mention") for more information.
{% endhint %}

## Managing Roles

Roles are managed on an organizational/global level. When a role is assigned, that role will apply across all projects.

Roles can be managed from the dashboard by visiting **Settings** > **Team Members** page for any Project.

<figure><img src="../.gitbook/assets/Team Members with RBAC view.png" alt=""><figcaption></figcaption></figure>

You can select any existing team member to change their role. New team members can also be invited with a specific role selected.

<figure><img src="../.gitbook/assets/Adding Team Members to Paragon Connect.png" alt=""><figcaption></figcaption></figure>

## Role Types

### Admin

**Admins have full read/write access to Paragon projects**. Admins can also exclusively invite new team members and view billing details.

### Members

Members are allowed to modify integrations and deploy workflows, but they cannot create new Event Destinations or modify existing Environment Secrets.

| ✔ Members are allowed to:                                                                                                                                                   | ✘ Members are not allowed to:                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <ul><li>Create, delete, activate, or deactivate Integrations</li><li>Create, modify, and deploy Workflows</li><li>Update SDK Setup options, including Signing Key</li></ul> | <ul><li>View or update Event Destinations</li><li>Update existing Environment Secret values</li><li>Manage API Keys</li><li>Invite new team members</li><li>View or modify billing details</li></ul> |

### Support

Support members are only allowed to view the Connected Users and Task History pages of the dashboard. Using these pages, they can provide support and error information to integration users.

| ✔ Support members are allowed to:                                                                                                                                                             | ✘ Support members are not allowed to:                                                                                                                              |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <ul><li>View and manage Connected Users, their integrations, and their metadata</li><li>View Task History for Workflows</li><li>Replay failed Workflow Executions from Task History</li></ul> | <ul><li>Create new Projects</li><li>Modify any project details (including Integrations or Workflows)</li><li>View Client IDs or Secrets for Integrations</li></ul> |

