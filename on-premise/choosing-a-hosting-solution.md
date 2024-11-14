# Choosing a Hosting Solution

Paragon offers several hosting solutions including:

* [**Cloud**](choosing-a-hosting-solution.md#cloud)
* [**Single Tenant**](choosing-a-hosting-solution.md#single-tenant)
* [**Managed On-Premise**](choosing-a-hosting-solution.md#managed-on-premise)
* [**Unmanaged On-Premise**](choosing-a-hosting-solution.md#unmanaged-on-premise)

## Cloud

Paragon’s cloud hosting is completely managed by Paragon and offered as a standard SaaS solution. It has the most up-to-date features and bug fixes and usually has updates several times a week. We take full responsibility for releases, patch management, security, incident response, and other standard development procedures.

This product is hosted on AWS in servers located in the United States and Europe. It is SOC2 Type 2 certified. For more information on SOC2 Type 2 certification, please visit our [Trust Center](https://security.useparagon.com/overview/eb093a6a-24dd-4fda-ad2b-6ea89cc01a75/soc-2).

You can get started in minutes by visiting the web application [here](https://dashboard.useparagon.com/signup).

#### What are the benefits?

* Get started in minutes
* Frequent releases (usually several each week)
* Fast support times

#### Who is this for?

This solution is the best for most companies. You should use it if you:

* Don’t have any legal obligations to host your data in a certain location
* Don’t have requirements to host your data alongside other customers
* Have expected volumes in the low - moderate usage of upto 10 million requests / month
* Don’t want to manage your own infrastructure

#### Who is this not for?

You should not use this solution if you:

* Need to host your data or servers in a certain country or region outside of the United States or Europe
* Expect more than 10 million requests/month
* Expect individual requests to take longer than 1 minute
* Expect to send and work with data in requests larger than 100 MB

## Single-Tenant

The single-tenant hosting solution is very similar to Paragon’s cloud hosting option except that it runs with completely dedicated resources (VPC, networks, databases, servers, etc).

This product is also hosted on AWS though in any country or region of your choosing. Releases, patch management, and infrastructure is completely managed by Paragon. This hosting solution is also [SOC2 Type 2 certified](https://www.useparagon.com/blog/soc-2-type-2).

#### What are the benefits?

* Choose a country and region to host servers and data
* Data is completely segregated from all customers
* More fault tolerant than the cloud offering
* Branded domains
* Service completely managed

#### Who is this for?

You should use this if you:

* Need your data or servers in a certain country or region
* Need your data segregated from all other customers
* Expect large volumes of traffic (over 10 million requests/month)
* Don’t want to manage your own infrastructure

#### Who is this not for?

You should not use this solution if you:

* Want to run on Azure or GCP instead of AWS

## Managed On-Premise

Managed on-premise is a hybrid offering used by almost all of our enterprise on-premise customers. It provides the security, isolation, and performance of on-premise with the ease of a cloud product.

In this offering, you will provide AWS, Azure, or GCP credentials with restricted access, and Paragon will deploy and manage the account for you. The data lives entirely in your own infrastructure and tooling.

To learn more about the access provided to the generated credentials, navigate to the docs for your cloud provider.

{% content-ref url="configure/aws.md" %}
[aws.md](configure/aws.md)
{% endcontent-ref %}

{% content-ref url="configure/azure.md" %}
[azure.md](configure/azure.md)
{% endcontent-ref %}

{% content-ref url="configure/gcp.md" %}
[gcp.md](configure/gcp.md)
{% endcontent-ref %}

#### What are the benefits?

* Choose a country and region to host servers and data
* Data is completely segregated from all customers
* Service completely managed
* Branded domains
* Unrestricted volume access

#### Who is this for?

You should use this if you:

* Need your data or servers in a certain country or region
* Need your data segregated from all other customers
* Expect large volumes of traffic (over 10 million requests / month)
* Have a dedicated devops team to configure and manage your infrastructure

#### Who is this not for?

You should not use this solution if you:

* Need to be HIPAA compliant

## Unmanaged On-Premise

Unmanaged on-premise is a do-it-yourself version which means you deploy, configure, update and manage your Paragon installation on your cloud. In this offering, you can deploy Paragon to your own AWS, Azure or GCP cloud. It provides the highest amount of security but the largest lift in terms of engineering time required to deploy and manage.

#### What are the benefits?

* Choose a country and region to host servers and data
* Data is completely segregated from all customers
* Reuse existing infrastructure (e.g. kubernetes cluster, Postgres server, etc)

#### Who is this for?

You should use this if you:

* Have strict compliance requirements (.e.g HIPAA)
* Have a dedicated devops team to configure, deploy and manage your installation

#### Who is this not for?

You should not use this solution if you:

* Don’t want to dedicate engineering resources to managing your infrastructure
* Need fast turnaround times for infrastructure-level issues
* Don’t have experience managing Kubernetes, Postgres, or Redis

We have an example repo for deploying Paragon to your own AWS account. You can find it [here](https://github.com/useparagon/aws-on-prem).
