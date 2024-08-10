# Notes:

## Prometheus 

1. ***Prometheus Server***

+ Example: Prometheus is set up to scrape metrics from an application running on http://localhost:8080/metrics. It collects data every 15 seconds.

2. ***Prometheus Data Model***

+ Example: An application exposes a metric ```http_requests_total with labels method="GET"``` and status="200". Prometheus stores the data as ```http_requests_total{method="GET",status="200"}.```

3. ***Prometheus Query Language (PromQL)***

+ Example: To find the total number of successful GET requests, you could use:

```promql
sum(http_requests_total{method="GET",status="200"})
```
+ This query sums up all ```http_requests_total metrics with method="GET" and status="200".```

4. Data Scraping

+ Example: Prometheus is configured to scrape metrics from a web server every 30 seconds. The server’s /metrics endpoint provides the following data:

```lua
http_requests_total{method="GET",status="200"} 1024
http_requests_total{method="POST",status="500"} 3
```
+ Prometheus scrapes this data and stores it in its database.

5. Alertmanager

+ Example: If the number of http_requests_total{status="500"} exceeds 5 in the last 5 minutes, an alert is triggered:
```yaml
alert: HighErrorRate
expr: sum(http_requests_total{status="500"}) > 5
for: 5m
labels:
  severity: critical
annotations:
  summary: "High error rate detected"
  description: "More than 5 HTTP 500 errors in the last 5 minutes."
```
+ Alertmanager routes this alert to Slack or email.

6. Exporters

+ Example: The node_exporter is a common exporter that exposes system metrics like CPU usage and memory. After running node_exporter on a server, Prometheus scrapes metrics from http://localhost:9100/metrics.

7. Pushgateway
+ Example: A batch job that processes data might push its metrics to the Pushgateway:
```bash
echo 'batch_jobs_processed_total 42' | curl --data-binary @- http://localhost:9091/metrics/job/batch_job
```
+ Prometheus scrapes the metrics from Pushgateway.


8. Prometheus UI

+ Example: In the Prometheus web UI, you can use the query:

```promql
rate(http_requests_total[5m])
```

+ This query visualizes the rate of HTTP requests over the past 5 minutes.

9. Integration with Grafana
+ Example: In Grafana, you create a dashboard panel that visualizes the total number of HTTP requests with:

```promql
sum(http_requests_total)
```
+ You can create various graphs and charts to visualize this data in real-time.

10. Service Discovery

+ Example: In a Kubernetes environment, Prometheus automatically discovers new pods with the following configuration:

```yaml
scrape_configs:
  - job_name: 'kubernetes-pods'
    kubernetes_sd_configs:
      - role: pod
```

11. Configuration
+ Example: A basic Prometheus configuration file (prometheus.yml) might look like:

```yaml
global:
  scrape_interval: 15s
scrape_configs:
  - job_name: 'my_application'
    static_configs:
      - targets: ['localhost:8080']
```
12. Alerting Rules

+ Example: An alert rule for high CPU usage:

```yaml
groups:
  - name: cpu_alerts
    rules:
      - alert: HighCpuUsage
        expr: avg(rate(node_cpu_seconds_total{mode="user"}[5m])) by (instance) > 0.9
        for: 2m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage on {{ $labels.instance }}"
          description: "CPU usage is over 90% for the last 2 minute."
```
+ Each of these examples showcases a basic usage scenario for different components of Prometheus, illustrating how it can be applied in practical monitoring and alerting setups.



