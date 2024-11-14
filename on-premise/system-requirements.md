# System Requirements

## Getting Started

To run Paragon on-premise, you’ll need:

* A Paragon license
* A major cloud provider account (e.g. AWS, Azure, or GCP)
* A Terraform account
* A SendGrid account
* A domain name

### Paragon License

Paragon authenticates its license to our cloud at boot and periodically to ensure the license is valid and the system can run.

If you don't already have a license, please contact [**sales@useparagon.com**](mailto:sales@useparagon.com), and we’ll get you connected.

### Major cloud provider account

Paragon comes bundled with a set of docker images, meaning you can run it on AWS, GCP, Azure, or any other server or cloud that supports Docker and has internet connectivity. It’s most resilient when running in Kubernetes. We have first class support for AWS, Azure and GCP.

For [Managed On-Premise installations](choosing-a-hosting-solution.md), you’ll need to provide credentials to provision your account. Here are links to instructions for the AWS, Azure, and GCP:

{% content-ref url="configure/aws.md" %}
[aws.md](configure/aws.md)
{% endcontent-ref %}

{% content-ref url="configure/azure.md" %}
[azure.md](configure/azure.md)
{% endcontent-ref %}

{% content-ref url="configure/gcp.md" %}
[gcp.md](configure/gcp.md)
{% endcontent-ref %}

### Terraform Account

The infrastructure state is managed within [Terraform](https://terraform.io/), a tool for managing infrastructure as code. For single-tenant or managed on-premise, we’ll use our own Terraform account.

### SendGrid Account

[SendGrid](https://sendgrid.com/) is used for sending emails from your Paragon instance. This includes:

* Failed workflow emails
* Inviting team members
* Resetting passwords

You’ll need an API key and an email that has been approved from the SendGrid dashboard to send emails.

### Domain name

A domain name is used to create a zone and CNAMEs for the microservices. You can purchase a domain name on [Namecheap](https://namecheap.com/) or provide a subdomain for an existing domain and we’ll create CNAMEs under that subdomain.

## Infrastructure Components

You will need some additional infrastructure components including:

* Kubernetes cluster
* Postgres database
* Redis database
* S3-compliant object store

You can learn more about these on the [Infrastructure Architecture](infrastructure-architecture.md) page. To see how to configure these components for AWS using Terraform, reference the AWS on-premise repo [here](https://github.com/useparagon/aws-on-prem).
