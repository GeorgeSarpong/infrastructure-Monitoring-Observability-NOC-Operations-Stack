# Infrastructure Monitoring & Observability — NOC Operations Stack

![NOC Operations](https://img.shields.io/badge/Domain-NOC%20Operations-blue)
![Prometheus](https://img.shields.io/badge/Tool-Prometheus-orange)
![Grafana](https://img.shields.io/badge/Tool-Grafana-orange)
![Datadog](https://img.shields.io/badge/Tool-Datadog-purple)
![CloudWatch](https://img.shields.io/badge/Tool-CloudWatch-yellow)
![ITIL](https://img.shields.io/badge/Framework-ITIL%20v4-green)

---

## Project Overview

This project deploys and documents a comprehensive Network Operations Center (NOC) monitoring stack replicating real-world enterprise infrastructure visibility across cloud and on-premises environments.

Built to demonstrate operational readiness for:
- ✅ NOC Engineer roles
- ✅ Infrastructure Monitoring Engineer roles
- ✅ Data Center Operations Engineer roles
- ✅ Site Reliability Engineer roles

---

## Real World Foundation

This monitoring framework is informed by hands-on operational experience managing:

- **Production rack infrastructure** — Dell PowerEdge servers supporting nationwide operations
- **24/7 monitoring operations** coordinating with remote engineering teams internationally
- **Industrial control system monitoring** across mission-critical production environments
- **Incident response** managing production-impacting outages in high-availability environments

---

## Repository Structure
---

## Monitoring Stack Architecture
---

## Monitoring Coverage

| Infrastructure Component | Tool | Metrics Monitored |
|---|---|---|
| Linux Servers | Prometheus + Node Exporter | CPU, Memory, Disk, Network |
| AWS EC2 | CloudWatch | CPU, Network, Status Checks |
| AWS RDS | CloudWatch | Connections, IOPS, Storage |
| Kubernetes Clusters | Prometheus + kube-state-metrics | Pod health, Node status |
| Application Performance | Datadog APM | Latency, Error rate, Throughput |
| Log Aggregation | Grafana Loki | Error logs, Security events |
| UPS & Power Systems | DCIM Integration | Load, Battery, Runtime |
| Cooling Systems | DCIM Integration | Temperature, Humidity |

---

##  Alert Thresholds & Configurations

### CPU Utilization
| Severity | Threshold | Duration | Action |
|---|---|---|---|
| Warning | Above 70% | 5 minutes | Notify on-call |
| Critical | Above 90% | 2 minutes | Page on-call immediately |

### Memory Utilization
| Severity | Threshold | Duration | Action |
|---|---|---|---|
| Warning | Above 75% | 5 minutes | Notify on-call |
| Critical | Above 90% | 2 minutes | Page on-call immediately |

### Disk Utilization
| Severity | Threshold | Duration | Action |
|---|---|---|---|
| Warning | Above 75% | 10 minutes | Notify on-call |
| Critical | Above 90% | 5 minutes | Page on-call immediately |

### Network Latency
| Severity | Threshold | Duration | Action |
|---|---|---|---|
| Warning | Above 100ms | 5 minutes | Notify on-call |
| Critical | Above 500ms | 2 minutes | Page on-call immediately |

---

## NOC Alert Triage Procedure

### Step 1 — Alert Receipt (0–1 minute)
1. Acknowledge alert in monitoring platform
2. Create incident ticket with timestamp
3. Identify affected system and severity level
4. Check monitoring dashboard for related alerts

### Step 2 — Initial Assessment (1–5 minutes)
1. Verify alert is not a false positive
2. Check system health across all monitoring tools
3. Review recent changes in change management log
4. Assess business impact of the alert
5. Determine if escalation is required

### Step 3 — Response & Resolution (5–30 minutes)
1. Follow relevant runbook for alert type
2. Apply known fix if available
3. Document all actions with timestamps
4. Update incident ticket throughout
5. Notify stakeholders per communication plan

### Step 4 — Post-Incident (Within 24 hours)
1. Complete post-incident review
2. Document root cause analysis
3. Identify preventive measures
4. Update runbooks if gaps identified
5. Close incident ticket with full documentation

---

## SLA Targets

| Service Tier | Availability Target | Max Downtime/Month | Response Time |
|---|---|---|---|
| Tier 1 — Critical | 99.99% | 4.3 minutes | Immediate |
| Tier 2 — High | 99.9% | 43.8 minutes | 15 minutes |
| Tier 3 — Standard | 99.5% | 3.6 hours | 1 hour |
| Tier 4 — Low | 99.0% | 7.3 hours | 4 hours |

---

## Prometheus Configuration Example

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

alerting:
  alertmanagers:
    - static_configs:
        - targets: ['alertmanager:9093']

rule_files:
  - "alert_rules.yml"

scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']

  - job_name: 'kubernetes'
    kubernetes_sd_configs:
      - role: pod
```

---

## Prometheus Alert Rules Example

```yaml
groups:
  - name: infrastructure_alerts
    rules:
      - alert: HighCPUUsage
        expr: 100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 90
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "High CPU usage detected"
          description: "CPU usage above 90% for 2 minutes on {{ $labels.instance }}"

      - alert: HighMemoryUsage
        expr: (node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100 > 90
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "High memory usage detected"
          description: "Memory usage above 90% on {{ $labels.instance }}"

      - alert: DiskSpaceLow
        expr: (node_filesystem_size_bytes - node_filesystem_free_bytes) / node_filesystem_size_bytes * 100 > 90
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Disk space critically low"
          description: "Disk usage above 90% on {{ $labels.instance }}"
```

---

##  Standards & Frameworks Referenced

- **ITIL v4** — Incident, problem, and change management
- **Prometheus** — Open source monitoring and alerting
- **Grafana** — Observability and dashboard platform
- **Datadog** — Cloud monitoring and analytics
- **AWS CloudWatch** — Native AWS monitoring service
- **PagerDuty** — Incident response and on-call management

---

## Tools & Technologies

![Prometheus](https://img.shields.io/badge/Prometheus-PCA%20Certified-orange)
![Grafana](https://img.shields.io/badge/Grafana-Loki-orange)
![Datadog](https://img.shields.io/badge/Datadog-Applied-purple)
![CloudWatch](https://img.shields.io/badge/AWS-CloudWatch-yellow)
![ITIL](https://img.shields.io/badge/ITIL%20v4-Foundation-green)
![Python](https://img.shields.io/badge/Python-Automation-blue)

---

## Author

**George Amankwaa Sarpong**
NOC Engineer | Infrastructure Monitoring & Data Center Operations
📍 Accra, Ghana 
🔗 [LinkedIn](https://linkedin.com/in/georgesarpong)
🌐 [GitHub Portfolio](https://github.com/GeorgeSarpong)

---

*This project is part of a broader portfolio demonstrating readiness for NOC Engineer, Infrastructure Monitoring, and Data Center Operations roles in the US and Global market.*
