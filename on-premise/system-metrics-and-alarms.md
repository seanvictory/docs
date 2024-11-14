# System Metrics and Alarms

For managed environments (cloud, single-tenant and managed on-premise), Grafana, Prometheus, and several exporters are deployed to the environment to aggregate system metrics, render them in custom dashboards and send alerts when deviations or dangerous values are detected.

Some of the systems that are monitored include:

* Load balancer
* Redis
* Postgres
* Postgres worker queue
* Redis worker queue
* Workflow executions
* Connect Proxy Requests
* Microservices

### Load balancer

Metrics and alarms include:

* Request count / response time
* HTTP response codes
* Connection count
* Bytes processed
* TLS errors

<figure><img src="../.gitbook/assets/Load Balancer Metrics Dashboard.png" alt=""><figcaption></figcaption></figure>

### Redis

Metrics and alarms include:

* Uptime
* Clients
* Memory usage
* Commands executed/second
* Hits/misses per second
* Total items per database
* Network I/O
* Expiring vs non-expiring keys
* Expired/evicted
* Command calls/second

<figure><img src="../.gitbook/assets/Redis Metrics Dashboard.png" alt=""><figcaption></figcaption></figure>

### Postgres

Metrics and alarms include:

* CPU usage
* Memory usage
* Transactions
* Locks
* Conflicts/deadlocks
* Cache hit rate

<figure><img src="../.gitbook/assets/Postgres Metrics Dashboard.png" alt=""><figcaption></figcaption></figure>

### Postgres Worker Queue

Metrics and alarms include:

* Workers
* Throughput
* Average wait
* Job statuses
* Job duration
* Error rate
* Average wait per queue
* Workers per queue

### Redis Worker Queue

Metrics and alarms include:

* Queue length
* Queue states
* Failures by queue
* Job duration

<figure><img src="../.gitbook/assets/Redis Worker Queue Metrics Dashboard.png" alt=""><figcaption></figcaption></figure>

### Workflow Executions

Metrics and alarms include:

* Workflow executions
* Step executions
* Workflow completion rate

<figure><img src="../.gitbook/assets/Workflow Executions Metrics Dashboard.png" alt=""><figcaption></figcaption></figure>

### Connect Proxy Requests

Metrics and alarms include:

* Total request count
* Latency
* Open requests
* Status code
* Status code by integration
* Status code by credential

<figure><img src="../.gitbook/assets/Connect Proxy Requests Metrics Dashboard.png" alt=""><figcaption></figcaption></figure>

### Microservices

Metrics and alarms include:

* Requests
* Apdex score
* Error rate
* Event loop lag
* CPU
* Heap
* Request duration
