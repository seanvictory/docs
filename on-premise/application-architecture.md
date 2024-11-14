# Application Architecture

## Overview

Paragon is composed of multiple microservices running within Kubernetes or Docker. While there are over 30 packages and microservices, the microservices can generally be grouped into two groups:

* Configuration
* Execution

The read-and-write patterns and volumes for each often differ significantly, so the services and their dependencies are decoupled so they can run independently.

### Configuration

When you log into Paragon, you can add team members, create workflows, configure steps, add and edit secrets, and more. All of these actions and their data fall under the **Configuration** category and are persisted in real-time to Postgres. Postgres acts as the source of truth, and when you are editing your configurations, they’re generally immediately persisted into Postgres.

### Execution

When workflows or connect proxy requests are triggered, they use cached versions of the configurations (e.g. workflows and steps, credentials, etc). Request volumes can be in the tens or hundreds of millions which require reads and writes in the microsecond-millisecond range. Generally, executions rely on cached data in Redis built from configurations stored in Postgres. Logs/results are flushed to Postgres periodically in batches to reduce the load on servers.

## Datastores

A diagram of where data is stored can be found below.

<figure><img src="../.gitbook/assets/Paragon Data Flow Diagram.png" alt=""><figcaption></figcaption></figure>

## Microservice Communication

Microservices communicate with each other in one of two methods:

* [Event-based (Redis)](application-architecture.md#event-based-communication-redis)
* [HTTP](application-architecture.md#http-based-communication)

### Event-based Communication (Redis)

Requests that fall in the **Execution** category (e.g. executing live workflows, Connect proxy requests, etc) and may happen in large volumes are queued in Redis as jobs. This allows the services to dynamically scale to meet the volume without losing data, retry failed jobs, and provide metrics on throughput, failure rates, and job metadata.

### HTTP-based Communication

Requests that fall in the **Configuration** category (e.g. editing workflows, adding team members, etc) that usually occur in low volumes are typically handled via HTTP calls over the private network. Custom tooling is used to add retry logic based on response codes, provided distributed tracing, validate payloads, and more.

## Queuing Retry Logic

Requests that fall in the **Execution** category (e.g. executing live workflows, Connect proxy requests, etc) have sophisticated logic around retries, some configurable and some automatic.

### Configurable step retries

Auto-retries can be enabled in the sidebar next to your steps. This will retry steps with jitter and exponential backoff upon failure. This is useful for when rate limits may be hit or other faulty APIs.

<figure><img src="../.gitbook/assets/Step Retries in a Paragon Workflow.png" alt=""><figcaption></figcaption></figure>

### System retries

When system errors are detected, like internal network errors or memory issues, the jobs will automatically retry.

### Automatic failures

In some cases, Paragon won’t attempt a request and automatically fail it if it knows the request won’t succeed. An example of this would include expired credentials - if Paragon isn’t able to refresh a credential, then other requests with the authenticated credential will fail.

## Back pressure and autoscaling

Requests that fall in the **Execution** category (e.g. executing live workflows, Connect proxy requests, etc) are queued in Redis to prevent data loss in case of large volumes of requests. This allows Paragon to autoscale to handle large volumes.

### Dedicated Queues

When a customer has a large volume of requests, a dedicated queue is created to process their jobs, and workers are autoscaled immediately to process the new queue. This prevents one customer from flooding primary queues and preventing requests from other customers from being processed.

### Autoscaling workers

The workers use a distributed leader election mechanism to determine the distribution of workers to queues. As soon as new queues are registered, a worker is provisioned in milliseconds to process that queue. Workers report health checks with the queue they’re working on. If a worker stops reporting that it’s working on a queue and a queue still has jobs to process, another worker will pick up the work within seconds.

Additionally, workers self-monitor and shut themselves down if there are no jobs to process in their queue.

The combination of distributed leader election, queue → worker provisioning, health checks, and self-monitoring allow Paragon to handle work across thousands of queues.

## Encryption of credentials

For all credentials and secrets, we use a custom distributed encrypted vault where each value has a unique key generated for encrypting it. The encrypted values and their keys are stored in a separate database and accessed by independent microservices, are decrypted only at execution time, and are only referenced by UUID or other non-sensitive values when represented in workflows. Additionally, the databases are all encrypted at rest, all in-memory caches also encrypt their values using separate rotating expiring keys, and data is encrypted in transit.
