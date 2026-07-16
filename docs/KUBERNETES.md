## ☸️ Kubernetes Cluster Design

### Overview

This document describes the Kubernetes cluster architecture used in the **Production-Inspired Platform Engineering on Google Kubernetes Engine (GKE)** project.

The platform is designed to provide secure, scalable, and isolated environments for platform services, applications, and stateful workloads while following cloud-native and GitOps best practices.

---
## Design Goals

The Kubernetes platform was designed with the following objectives:

* Secure workload isolation
* High availability
* Declarative infrastructure
* GitOps-based operations
* Scalable application deployments
* Platform observability
* Event-driven autoscaling
* Policy-based governance

---
## Cluster Architecture

```text
Google Kubernetes Engine (Private Cluster)
│
├── System Node Pool
│     ├── Argo CD
│     ├── Kyverno
│     ├── cert-manager
│     ├── External Secrets
│     ├── Gateway API
│     ├── Prometheus
│     ├── Grafana
│     └── Kubecost
│
├── Application Node Pool
│     ├── Vote
│     ├── Result
│     └── Worker
│
└── Data Node Pool
      ├── Redis
      └── PostgreSQL
```

---
## Node Pools

The cluster separates workloads into dedicated node pools to improve resource isolation and operational efficiency.

| Node Pool        | Purpose                                        |
| ---------------- | ---------------------------------------------- |
| System Pool      | Platform services and Kubernetes controllers   |
| Application Pool | Stateless application workloads                |
| Data Pool        | Stateful services such as Redis and PostgreSQL |

---
## Namespace Design

Namespaces provide logical separation between workloads.

| Namespace        | Purpose                                     |
| ---------------- | ------------------------------------------- |
| argocd           | GitOps controller                           |
| gateway          | Gateway API and NGINX Gateway Fabric        |
| monitoring       | Prometheus, Grafana, Alertmanager, Kubecost |
| external-secrets | Secret synchronization                      |
| cert-manager     | TLS certificate management                  |
| vote             | Vote application                            |
| result           | Result application                          |
| worker           | Background worker                           |
| redis            | Redis database                              |
| postgres         | PostgreSQL database                         |

---
## Scheduling Strategy

Dedicated node pools are used together with Kubernetes scheduling features.

### Node Labels

```yaml
workload: system
workload: app
workload: data
```

---
### Taints

```yaml
workload=system:NoSchedule
workload=app:NoSchedule
workload=data:NoSchedule
```

---
### Tolerations

Platform and application workloads include matching tolerations to allow scheduling onto the appropriate node pools.

---
### Node Affinity

Node affinity ensures workloads are deployed only on their intended nodes.

Example:

* Platform services → System Pool
* Applications → Application Pool
* Databases → Data Pool

---
## Resource Management

Each workload defines resource requests and limits.

Example:

```yaml
resources:
  requests:
    cpu: "250m"
    memory: "256Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

This improves scheduling efficiency and prevents resource contention.

---
## Security Model

Security is enforced using multiple Kubernetes-native mechanisms.

### RBAC

Role-Based Access Control restricts access to cluster resources based on service accounts and roles.

---
### Namespaces

Applications and platform services are isolated into dedicated namespaces.

---
### Kyverno Policies

Cluster-wide policies enforce standards such as:

* Required labels
* Resource requests and limits
* Liveness probes
* Readiness probes
* Non-root containers
* Approved container registries

---
### Secret Management

Sensitive configuration is not stored in Git.

Secrets are synchronized from **Google Secret Manager** using **External Secrets Operator**.

---
## Networking

External traffic enters the cluster through the Gateway API.

```text
Internet
      │
Cloudflare DNS
      │
Gateway API
      │
Application Services
      │
Pods
```

The Gateway API provides:

* HTTP routing
* HTTPS termination
* Load balancing
* Traffic management

---
## Service Discovery

Applications communicate internally using Kubernetes Services.

Examples:

* vote-service
* result-service
* worker-service
* redis
* postgres

Service discovery relies on Kubernetes DNS.

---
## Storage

Stateful workloads use Persistent Volumes backed by Google Cloud persistent disks.

| Workload   | Storage           |
| ---------- | ----------------- |
| Redis      | Persistent Volume |
| PostgreSQL | Persistent Volume |

Persistent Volume Claims are used to decouple workloads from storage implementation.

---
## Autoscaling

The platform supports multiple autoscaling mechanisms.

### Horizontal Pod Autoscaler

Application pods scale automatically based on CPU utilization.

---
### KEDA

Worker services scale based on Redis queue length, enabling event-driven autoscaling.

---
## Observability

The cluster includes a complete monitoring stack.

Components include:

* Prometheus
* Grafana
* Alertmanager
* ServiceMonitor
* PrometheusRule

These services collect application and cluster metrics, visualize dashboards, and generate alerts.

---
## GitOps Deployment Model

All Kubernetes resources are managed declaratively.

```text
Git Repository
      │
      ▼
Argo CD
      │
      ▼
Google Kubernetes Engine
```

Argo CD continuously synchronizes the cluster with the desired state stored in Git.

---
## High Availability

The platform is designed to improve availability through:

* Multiple node pools
* Replica-based deployments
* Kubernetes self-healing
* Readiness and liveness probes
* Rolling and canary deployments
* Event-driven autoscaling

---
## Platform Components

The cluster hosts several platform services.

| Component            | Purpose                    |
| -------------------- | -------------------------- |
| Argo CD              | GitOps Continuous Delivery |
| Kyverno              | Policy enforcement         |
| cert-manager         | TLS certificate automation |
| External Secrets     | Secret synchronization     |
| Gateway API          | Traffic routing            |
| NGINX Gateway Fabric | Gateway implementation     |
| Prometheus           | Metrics collection         |
| Grafana              | Dashboards                 |
| Alertmanager         | Alert routing              |
| Kubecost             | Kubernetes cost monitoring |
| KEDA                 | Event-driven autoscaling   |
| Argo Rollouts        | Progressive delivery       |

---
## Design Principles

The Kubernetes platform follows these principles:

* Infrastructure as Code
* GitOps-first operations
* Immutable deployments
* Namespace isolation
* Least-privilege access
* Declarative configuration
* Automated reconciliation
* Production-inspired architecture
* Secure-by-default platform
* Cloud-native operational practices

---