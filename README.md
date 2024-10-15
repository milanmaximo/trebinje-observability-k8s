# Kubernetes Observability Stack

A comprehensive observability platform for Kubernetes running on Linode Kubernetes Engine (LKE), featuring metrics, logs, and alerting capabilities with secure HTTPS access.

## Architecture Overview

This stack provides full-stack observability for Kubernetes clusters:

- **Prometheus**: Time-series metrics collection and storage (30-day retention)
- **Loki**: Distributed log aggregation and querying (30-day retention)
- **Grafana**: Unified visualization and dashboarding
- **Alertmanager**: Alert routing and notification management
- **cert-manager**: Automated TLS certificate management via Let's Encrypt
- **NGINX Ingress Controller**: Secure HTTPS ingress with SSL termination

## Components

### Monitoring Stack

| Component | Version | Purpose |
|-----------|---------|---------|
| Prometheus | v2.53.1 | Metrics collection, storage, and querying |
| Loki | Latest | Log aggregation and storage |
| Grafana | v11.1.0 | Visualization and dashboards |
| Alertmanager | Latest | Alert management and routing |

### Infrastructure

- **Namespace**: `monitoring`
- **Storage**: Linode Block Storage with retain policy
- **Ingress**: NGINX with TLS termination
- **DNS**: trebinje.online domain
- **Certificates**: Let's Encrypt production certificates

## Access Points

- **Grafana**: https://grafana.trebinje.online
- **Prometheus**: https://prometheus.trebinje.online/prometheus
- **Alertmanager**: https://alertmanager.trebinje.online
- **Loki**: https://loki.trebinje.online

## Storage Configuration

### Prometheus
- **Retention**: 30 days
- **Storage**: 50Gi persistent volume
- **WAL Compression**: Enabled
- **Resource Limits**: 2 CPU / 4Gi Memory

### Loki
- **Retention**: 30 days (720h)
- **Storage**: 20Gi persistent volume
- **Ingestion Rate**: 10MB/s (burst: 20MB/s)
- **Per-stream Limit**: 3MB/s (burst: 15MB/s)

### Grafana
- **Storage**: 10Gi persistent volume
- **Datasources**: Prometheus (default), Loki

## Deployment

### Prerequisites

- Kubernetes cluster (LKE or similar)
- kubectl configured with cluster access
- DNS records pointing to cluster ingress IP
- Linode Block Storage CSI driver installed

### Install Order

1. Install NGINX Ingress Controller
2. Install cert-manager
3. Apply monitoring namespace and RBAC
4. Deploy Prometheus with alerts
5. Deploy Loki
6. Deploy Grafana with datasources
7. Configure TLS and Ingress

For detailed deployment instructions, see DEPLOYMENT.md
