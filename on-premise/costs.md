# On-Premise Costs

{% hint style="info" %}
**Summary:** Generally, you should expect to pay up to $2,000 / month in infrastructure costs for volumes of up to 20 million requests/month.

This could increase or decrease depending on the cloud provider, request volumes (increases server and ingress/egress costs), redundancy and resiliency requirements (increases database costs), and size of data flowing through the system (increases blob storage, cache, and ingress/egress costs).

For low volumes (under 10 million requests/month) running on single region deployments with spot instances, costs can be as low as $900/month.
{% endhint %}

## Overview

To run Paragon’s software on your own cloud, you’ll need at a minimum:

* Kubernetes cluster
* PostgreSQL database
* Redis instance
* SendGrid account

While we are constantly optimizing resources and finding ways to cut costs for cloud and on-premise, **costs equal to or below $1,000/month are our current benchmark when adding or refactoring services for installations with request volumes of 0 - 100 million requests/month.**

Costs can be affected by several factors including cloud provider, request volumes (increases server and ingress/egress costs), redundancy and resiliency requirements (increases database costs), and size of data flowing through the system (increases blob storage, cache, and ingress/egress costs).

We’ve been able to reduce several Managed On-Premise instances to under $500/month and provide cost optimization for our managed customers at no additional cost. If cloud spend is a concern, consider using our [Managed On-Premise option](choosing-a-hosting-solution.md#managed-on-premise).

## Resources

### Kubernetes

The Kubernetes cluster runs the microservices. Depending on the number of requests flowing through the system, more servers may need to be instantiated to meet the demand. Services typically autoscale based on horizontal pod autoscalers listening to CPU and memory.

Prices on compute instances can be found below:

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">AWS</td><td></td><td><a href="https://aws.amazon.com/ec2/pricing/on-demand/">https://aws.amazon.com/ec2/pricing/on-demand/</a></td><td></td></tr><tr><td></td><td align="center">Azure</td><td></td><td><a href="https://azureprice.net/">https://azureprice.net/</a></td><td></td></tr><tr><td></td><td align="center">GCP</td><td></td><td><a href="https://cloud.google.com/compute/all-pricing">https://cloud.google.com/compute/all-pricing</a></td><td></td></tr></tbody></table>

Additionally, some of the clouds charge a base price per month for Kubernetes (e.g. AWS EKS charges $72 / mo).

#### Spot Instances

Kubernetes pricing can be optimized by using spot instances, which can cut costs by as much as 90%. AWS, Azure, and GCP all offer spot instances, which you can learn more about [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html).

Installations can be configured to use a certain percentage of spot instances (0 - 100%).

#### Reserved Pricing

You can save on compute costs by reserving server instances and paying for so many months or years up front. AWS, Azure and GCP all offer this.

#### Pricing Chart

Here are our recommended settings for request volumes of up to 100 million requests/month.

<table><thead><tr><th width="109">Cloud</th><th width="110">Instance</th><th width="116">Instances</th><th width="106.33333333333331" align="right">$ / Hour</th><th align="right">$ / Hour (Spot)</th><th align="right">$ / Month</th><th align="right">$ / Month (Spot)</th></tr></thead><tbody><tr><td><strong>AWS</strong>*</td><td>t3a.small</td><td>16</td><td align="right">0.0188</td><td align="right">0.0056</td><td align="right">$216.58</td><td align="right">$64.51</td></tr><tr><td><strong>Azure</strong></td><td>B1s</td><td>32</td><td align="right">0.0104</td><td align="right"></td><td align="right">$239.62</td><td align="right">$0.00</td></tr><tr><td><strong>Azure</strong></td><td>D2as v5</td><td>8</td><td align="right">0.086</td><td align="right">0.0086</td><td align="right">$495.36</td><td align="right">$49.54</td></tr><tr><td><strong>GCP</strong></td><td>e2-small</td><td>16</td><td align="right">0.016751</td><td align="right">0.016751</td><td align="right">$192.97</td><td align="right">$57.89</td></tr></tbody></table>

{% hint style="info" %}
For AWS, add $72 / mo to run the EKS cluster.
{% endhint %}

### Postgres

Postgres is the primary datastore used for saving data in Paragon. A single server is needed, and several databases are provisioned within it. The costs are generally determined by CPU and memory.

<table><thead><tr><th width="110">Instance</th><th width="110">Cloud</th><th data-type="number">vCPU</th><th>Memory (GB)</th><th width="106.33333333333331" align="right">$ / Hour</th><th align="right">$ / Month</th><th align="right">$ / Month (Multi-AZ)</th></tr></thead><tbody><tr><td>db.t3.micro</td><td>AWS</td><td>2</td><td>1</td><td align="right">0.018</td><td align="right">$12.96</td><td align="right">$25.92</td></tr><tr><td>db.t3.medium</td><td>AWS</td><td>2</td><td>4</td><td align="right">0.072</td><td align="right">$51.84</td><td align="right">$103.68</td></tr><tr><td>GP_Gen5_2</td><td>Azure</td><td>2</td><td>10</td><td align="right">0.176</td><td align="right">$126.72</td><td align="right">$253.44</td></tr><tr><td>db-f1-micro</td><td>GCP</td><td>null</td><td>0.6</td><td align="right">0.0105</td><td align="right">$7.56</td><td align="right">$15.12</td></tr><tr><td>db-n1-standard-2</td><td>GCP</td><td>2</td><td></td><td align="right">0.0826</td><td align="right">$59.47</td><td align="right">$118.94</td></tr></tbody></table>

{% hint style="info" %}
GCP also charges for storage and networking. Learn more [here](https://cloud.google.com/sql/docs/postgres/pricing).
{% endhint %}

#### Reserved Pricing

You can save on Postgres costs by paying for 1 - 3 years upfront. AWS, Azure, and GCP all offer this.

### Redis

Redis is used as a cache and worker queue. A single Redis instance is needed. Pricing is typically determined based on cost and memory.

<table><thead><tr><th width="195">Instance</th><th width="110">Cloud</th><th width="76" data-type="number">vCPU</th><th width="96">Memory (GB)</th><th width="105.33333333333331" align="right">$ / Hour</th><th width="110" align="right">$ / Month</th><th align="right">$ / Month (Multi-AZ)</th></tr></thead><tbody><tr><td>cache.m6g.xlarge</td><td>AWS</td><td>4</td><td>12.93</td><td align="right">0.297</td><td align="right">$213.84</td><td align="right">$427.68</td></tr><tr><td>cache.r4.xlarge</td><td>AWS</td><td>4</td><td>25.05</td><td align="right">0.455</td><td align="right">$327.60</td><td align="right">$655.20</td></tr><tr><td>P1</td><td>Azure</td><td>0</td><td>6</td><td align="right">0.554</td><td align="right">$398.88</td><td align="right">$797.76</td></tr><tr><td>P3</td><td>Azure</td><td>null</td><td>26</td><td align="right">2.218</td><td align="right">$1,596.96</td><td align="right">$3,193.92</td></tr><tr><td>Standard</td><td>GCP</td><td>0</td><td>10</td><td align="right">0.54</td><td align="right">$388.80</td><td align="right">$777.60</td></tr><tr><td>Standard</td><td>GCP</td><td>null</td><td>25</td><td align="right">1.15</td><td align="right">$828.00</td><td align="right">$1,656.00</td></tr></tbody></table>

You can find more about Redis pricing below.

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td align="center">AWS</td><td></td><td><a href="https://aws.amazon.com/elasticache/pricing/">https://aws.amazon.com/elasticache/pricing/</a></td></tr><tr><td></td><td align="center">Azure</td><td></td><td><a href="https://azure.microsoft.com/en-in/pricing/details/cache/#pricing">https://azure.microsoft.com/en-in/pricing/details/cache/#pricing</a></td></tr><tr><td></td><td align="center">GCP</td><td></td><td><a href="https://cloud.google.com/memorystore/docs/redis/pricing">https://cloud.google.com/memorystore/docs/redis/pricing</a></td></tr></tbody></table>

### SendGrid

SendGrid is used to send emails including:

* invite team member
* reset password
* failed workflow notifications

Assuming you’re sending less than 100 emails a day, you can get by on the free tier. On the **Essentials** tier, you can send as much as 1,500 / day and pay $19.95 / mo.

{% embed url="https://sendgrid.com/pricing/" %}
