# Project 1: Monitoring & Logging with Prometheus and Grafana

Rhombix Technologies DevOps Internship - Task 1

## Architecture

| Service | Port | Kaam |
|---|---|---|
| Prometheus | 9090 | Metrics collect aur alert rules evaluate karta hai |
| Node Exporter | 9100 | Host (server) ke CPU, memory, disk metrics |
| cAdvisor | 8080 | Docker containers ke metrics |
| Alertmanager | 9093 | Alerts receive aur manage karta hai |
| Grafana | 3000 | Dashboards aur visualization |

## Setup

Requirements: Docker aur Docker Compose.

```bash
cd project1-monitoring
docker compose up -d
docker compose ps
```

## Access

- Prometheus: http://localhost:9090 (Status -> Targets mein sab UP hon)
- Alertmanager: http://localhost:9093
- Grafana: http://localhost:3000 (user: `admin`, password: `admin123`)

Grafana mein Prometheus data source pehle se provision hota hai.

## Grafana dashboards

Dashboards -> New -> Import:
- **1860**: Node Exporter Full (server metrics)
- **14282**: cAdvisor (container metrics)

## Alerts

`prometheus/alert.rules.yml` mein ye alerts hain:

- HighCPUUsage (CPU > 80% for 1m)
- HighMemoryUsage (Memory > 80% for 1m)
- HighDiskUsage (Disk > 85% for 2m)
- InstanceDown (koi target down for 30s)

### Alert test

```bash
docker run --rm -it progrium/stress --cpu 4 --timeout 180s
```

Phir Prometheus -> Alerts page par `HighCPUUsage` firing dikhega.

## Screenshots

(Yahan apne screenshots add karein: targets, Grafana dashboard, firing alert)

## Band karna

```bash
docker compose down
```
