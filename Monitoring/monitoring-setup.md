# Monitoring Setup

## Overview
MON01 runs a Grafana and Prometheus stack to monitor all VMs in the homelab.
Metrics are scraped from each host using the Prometheus Node Exporter (Linux)
and Windows Exporter (Windows). Alerts are configured for critical thresholds.

---

## Stack

| Component | Purpose | Port |
|---|---|---|
| Prometheus | Metrics collection and storage | 9090 |
| Grafana | Dashboards and visualization | 3000 |
| Node Exporter | Linux metrics agent | 9100 |
| Windows Exporter | Windows metrics agent | 9182 |

---

## Monitored Hosts

| Host | OS | Exporter | IP |
|---|---|---|---|
| DC01 | Windows Server 2022 | Windows Exporter | 10.0.20.10 |
| FS01 | Windows Server 2022 | Windows Exporter | 10.0.20.11 |
| MON01 | Ubuntu 22.04 | Node Exporter | 10.0.20.12 |
| BACKUP01 | Windows Server 2022 | Windows Exporter | 10.0.20.13 |

---

## Prometheus Configuration

    scrape_configs:
      - job_name: 'windows'
        static_configs:
          - targets:
            - '10.0.20.10:9182'
            - '10.0.20.11:9182'
            - '10.0.20.13:9182'

      - job_name: 'linux'
        static_configs:
          - targets:
            - '10.0.20.12:9100'

---

## Grafana Dashboards

| Dashboard | Purpose |
|---|---|
| Windows Host Overview | CPU, RAM, disk, network per Windows VM |
| Linux Host Overview | CPU, RAM, disk, network for MON01 |
| Disk Space Tracker | Free disk % across all VMs with warning threshold |
| Uptime Overview | Last reboot and uptime per host |

---

## Alerting Rules

| Alert | Condition | Severity |
|---|---|---|
| High CPU | CPU > 90% for 5 minutes | Warning |
| Low Disk Space | Free disk < 20% | Warning |
| Host Down | Host unreachable for 2 minutes | Critical |
| High Memory | RAM > 85% for 5 minutes | Warning |

---

## Alert Notifications

- Alerts are routed through Grafana Alerting
- Notifications sent to admin email on Warning and Critical
- Critical alerts also trigger a desktop notification via Pushover

---

## Access

- Grafana UI: http://10.0.20.12:3000
- Prometheus UI: http://10.0.20.12:9090
- Both accessible from Management VLAN only