# Data Access & Controls

## Frequently Asked Questions

### Who has access to your data on the Paragon side?

For unmanaged installations, your data never leaves your installation and no one in Paragon has access to any of your data besides the billing contact information associated with the subscription.

For managed installations, your data never leaves your installation, and a Paragon support engineer can get limited access to perform maintenance or support tasks such as viewing application logs or debugging a workflow. Temporary access is granted upon request, logged and approved internally, and an audit trail of commands executed is automatically tracked. Sensitive data, like credentials, are never accessible.

### What type of access is required for managed installations?

The Paragon installer needs credentials to provision application resources via Terraform. Because the credentials are sandboxed to the tenant / organization / subscription, the installer cannot access any other resources on the AWS / Azure / GCP account. These credentials aren’t shared with any Paragon engineers.

Paragon support engineers are granted temporary access to application logs via ElasticSearch or limited database access via [Teleport](https://goteleport.com/) to perform routine support duties requested by customers.

### How is access limited to support engineers?

Each managed installation is only accessible from a list of whitelisted IP addresses modified on demand and additionally protected by SSH keys.

### Is there an audit trail for access?

Access requests are logged and approved internally. SSH access is automatically logged to an S3 bucket with all commands executed.
