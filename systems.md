# Prod ready Systems

Some things a prod ready system should have:

1. unit test
2. integration tests
3. continuous integration
4. continuous deployment
5. monitoring and alerts
6. logging
7. health dashboards
8. software hygiene monitors (package security checks, code static analysis, security probes/scanning)

Some notes on subtopics:

## Monitoring

Base monitoring coverage:

1. Latency - all APIs/processes measure latency and made available to monitoring. Percentiles, monitored at p99 or p99.9
2. Error rates - success/failures rates, monitored at 99% and above
3. Latency of dependencies - monitored at or below SLAs
4. Min call rates / time since last periodic process - (alert if process/workflow X hasn't run in last X minutes/hours/days)
5. Max call rates - total system and throttling per client
6. Percentage utilization rates - API quoatas, system resources (CPU, Memory, Disk, Network bandwidth)
7. Number of available instances running/not running (hosts, containers, batch instances). Capacity available if dynamically scaled.
8. Distributed system health - Queue length/backpressure/age, replication lag/percentage, backlog tasks, etc.
9. Any other system invariants that must be maintained. (Application level or system/platform level).

