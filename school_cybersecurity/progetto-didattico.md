# 📊 Monitoring Dashboard

Version: **v1.0**

---

# Descrizione

La **Monitoring Dashboard** è la seconda dashboard ufficiale del progetto **CyberSentinel**.

Il suo obiettivo è monitorare l'infrastruttura di osservabilità stessa, verificando che Prometheus, Grafana, Node Exporter e cAdvisor siano operativi e che la raccolta delle metriche avvenga correttamente.

Questa dashboard rappresenta il secondo livello della suite di dashboard CyberSentinel.

```text
Infrastructure
        │
        ▼
Monitoring
        │
        ▼
Logging
        │
        ▼
Security
        │
        ▼
SOC Overview
```

---

# Obiettivi

La dashboard permette di rispondere rapidamente alle seguenti domande:

- Prometheus è operativo?
- Grafana è raggiungibile?
- Gli exporter rispondono correttamente?
- Tutti i target risultano UP?
- Prometheus sta acquisendo metriche?
- Il database TSDB è in salute?
- Sono presenti alert attivi?

---

# Datasource

**Prometheus**

---

# Layout

## Services

| Pannello | Tipo |
|----------|------|
| Prometheus Status | Stat |
| Grafana Status | Stat / Text |
| Node Exporter Status | Stat |
| cAdvisor Status | Stat |

---

## Prometheus

| Pannello | Tipo |
|----------|------|
| Targets UP | Stat |
| Targets DOWN | Stat |
| Scrape Duration | Time Series |
| Samples Scraped | Time Series |

---

## Database

| Pannello | Tipo |
|----------|------|
| TSDB Series | Stat |
| TSDB Chunks | Stat |
| TSDB WAL | Time Series |

---

## Alerts

| Pannello | Tipo |
|----------|------|
| Active Alerts | Stat |

---

# Query utilizzate

## Prometheus Status

```promql
up{job="prometheus"}
```

---

## Node Exporter Status

```promql
up{job="node-exporter"}
```

---

## cAdvisor Status

```promql
up{job="cadvisor"}
```

---

## Targets UP

```promql
sum(up)
```

---

## Targets DOWN

```promql
count(up)-sum(up)
```

---

## Scrape Duration

```promql
prometheus_target_interval_length_seconds
```

---

## Samples Scraped

```promql
rate(prometheus_tsdb_head_samples_appended_total[5m])
```

---

## TSDB Series

```promql
prometheus_tsdb_head_series
```

---

## TSDB Chunks

```promql
prometheus_tsdb_head_chunks
```

---

## TSDB WAL

```promql
prometheus_tsdb_wal_completed_pages_total
```

---

## Active Alerts

```promql
ALERTS
```

---

# Componenti monitorati

- Grafana
- Prometheus
- Node Exporter
- cAdvisor

---

# Prerequisiti

- Docker Engine
- Prometheus
- Grafana
- Node Exporter
- cAdvisor

---

# Versione

| Versione | Stato |
|-----------|--------|
| v1.0 | ✅ Stable |

---

# Roadmap

## Versione 1.1

- Datasources Status
- Prometheus Build Info
- Prometheus Configuration Reload
- Target Labels

---

## Versione 1.2

- Alertmanager
- Recording Rules
- Rule Evaluation
- Alert Statistics

---

## Versione 2.0

- Loki
- Promtail
- Log Health
- Correlazione Metrics + Logs

---

# File

```text
templates/
└── grafana/
    └── dashboards/
        ├── Monitoring-v1.0.json
        ├── Monitoring-README.md
        └── screenshots/
            └── monitoring-v1.0.png
```

---

# CyberSentinel Dashboard Suite

- 🖥️ Infrastructure
- 📊 Monitoring
- 📜 Logging *(planned)*
- 🔐 Security *(planned)*
- 🛡️ SOC Overview *(planned)*

---

**CyberSentinel Monitoring Dashboard** è parte integrante della suite di dashboard del progetto CyberSentinel ed è progettata per monitorare la salute della piattaforma di osservabilità prima ancora dell'infrastruttura monitorata.
