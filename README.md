## Project Overview

This Platform Engineering Portfolio demonstrates the design, provisioning, deployment, security, and operation of a production-ready cloud-native application platform on Google Cloud Platform (GCP). The project follows modern Platform Engineering principles by separating infrastructure provisioning, platform services, application delivery, and operational automation into dedicated repositories.

The platform is built using Infrastructure as Code (Terraform) to provision cloud resources such as Virtual Private Cloud (VPC), Google Kubernetes Engine (GKE), Cloud SQL, Artifact Registry, Identity and Access Management (IAM), and Cloud Storage. Shared Kubernetes platform services including ArgoCD, External Secrets, Kyverno, Cert-Manager, Prometheus, Grafana, Kubecost, Falco, KEDA, Velero, and Gateway API are deployed as reusable platform components.

Application delivery follows a GitOps workflow using ArgoCD and Kustomize, enabling declarative, version-controlled deployments across multiple environments. CI pipelines are implemented with GitHub Actions to automate source code validation, testing, container image builds, vulnerability scanning, SBOM generation, image signing, and deployment updates.

Security is integrated throughout the platform using policy enforcement, runtime security, secrets management, network segmentation, and container image verification. Observability is provided through centralized monitoring, metrics collection, alerting, and cost visibility.

The portfolio demonstrates a complete Platform Engineering lifecycle, covering infrastructure provisioning, platform management, application deployment, security, observability, automation, and progressive delivery using production-oriented engineering practices.

---
## Solution Architecture

The following architecture illustrates the complete platform deployment on GCP.
![Architecture Diagram](docs/images/platform_engineering_architecture.png "Platform Architecture")


This platform is built on a layered architecture that cleanly separates infrastructure provisioning, platform services, application delivery, and operations. Each layer owns a single responsibility, which keeps the system modular, independently scalable, and easier to secure and maintain as it grows.

The entire stack runs on Google Cloud Platform (GCP) and is built around modern Platform Engineering and GitOps principles — infrastructure, Kubernetes platform services, application deployments, security, and observability are all automated rather than manually operated.

Architecture at a glance

| Layer | Responsibility | Key Technologies |
|-------|----------------|------------------|
| **Infrastructure** | Cloud foundation and networking | Terraform, Google Cloud Platform (GCP), VPC, GKE, Cloud SQL, Artifact Registry |
| **Platform** | Shared Kubernetes platform services | ArgoCD, Argo Rollouts, Gateway API, Kyverno, Falco |
| **GitOps** | Declarative, version-controlled application delivery | ArgoCD, Kustomize |
| **Application** | Cloud-native microservices | Vote Service, Result Service, Worker Service, PostgreSQL, Redis |
| **CI/CD** | Build, test, secure, and deploy applications | GitHub Actions, Trivy, Cosign, SBOM, Artifact Registry |
| **Security** | Defense-in-depth and policy enforcement | Kyverno, Kubernetes RBAC, Workload Identity, Falco |
| **Observability** | Monitoring, dashboards, and alerting | Prometheus, Grafana, Alertmanager |
| **Platform Automation** | Operational automation and self-healing | Python-based automation services |


## Platform Layers

### 1. Infrastructure Layer

The **Infrastructure Layer** is fully provisioned using **Terraform**, providing the cloud foundation required to operate the platform.

It provisions:

- VPC 
- Cloud Router and Cloud NAT for controlled outbound access
- Firewall rules
- IAM roles and Workload Identity Federation
- Google Kubernetes Engine (GKE)
- Cloud SQL (PostgreSQL)
- Artifact Registry
- Cloud Storage
- Service Accounts

Infrastructure is organized into reusable Terraform modules, enabling consistent deployments across **Development** and **Production** environments by reusing the same modules with environment-specific variables.

---

### 2. Platform Layer

After the Kubernetes cluster is provisioned, the **Platform Layer** installs the shared services required by application teams.

Platform components include:

- ArgoCD
- Argo Rollouts
- Gateway API
- NGINX Gateway Fabric
- Cert-Manager
- External Secrets Operator
- Kyverno
- Falco
- Prometheus
- Grafana
- Alertmanager
- Kubecost
- KEDA
- Velero
- Reloader

These services transform a standard Kubernetes cluster into a production-ready Internal Developer Platform (IDP).

---

### 3. GitOps Layer

Application delivery follows a **GitOps** workflow where all deployment changes are managed through Git. Direct deployments to the Kubernetes cluster are not permitted.

**ArgoCD** continuously reconciles the desired state stored in Git with the live cluster state.

#### GitOps Capabilities

- Declarative, version-controlled deployments
- Automatic synchronization and drift detection
- One-command rollback
- Environment promotion using Kustomize overlays

---

### 4. Application Layer

The platform hosts a cloud-native microservices application consisting of:

- Vote Service
- Result Service
- Worker Service
- PostgreSQL
- Redis

Application manifests are managed using **Kustomize**, with separate overlays for each environment.

Progressive delivery is implemented using **Argo Rollouts**, supporting:

- Canary Deployments
- Blue-Green Deployments

---

### 5. CI/CD Layer

Continuous Integration is implemented using **GitHub Actions**.

The pipeline performs:

1. Source code checkout
2. Dependency installation
3. Unit testing
4. Docker image build
5. Trivy vulnerability scanning
6. SBOM generation
7. Cosign image signing
8. Push image to Artifact Registry
9. Update GitOps manifests automatically

Once the GitOps repository is updated, **ArgoCD** automatically synchronizes the cluster with the latest application version.

---

### 6. Security Layer

Security is integrated throughout the platform using a DevSecOps approach.

Key security capabilities include:

- Kyverno policy enforcement
- Pod Security Standards (PSS)
- Kubernetes Network Policies
- Role-Based Access Control (RBAC)
- External Secrets Operator
- Workload Identity Federation
- Trivy image vulnerability scanning
- Software Bill of Materials (SBOM)
- Cosign container image signing
- Falco runtime threat detection

These controls ensure workloads comply with organizational security policies before reaching production.

---

### 7. Observability Layer

Platform observability is powered by:

- Prometheus
- Grafana
- Alertmanager

Monitoring includes:

- Kubernetes cluster metrics
- Application metrics
- Redis exporter metrics
- PostgreSQL exporter metrics
- ServiceMonitors
- Alerting rules
- Grafana dashboards

This provides comprehensive visibility into platform health, application performance, and infrastructure utilization.

---

### 8. Platform Automation Layer

Operational tasks are automated using Python-based services.

Automation includes:

- Daily platform health reports
- Cluster health validation
- Infrastructure reporting
- Scheduled maintenance tasks
- Operational self-healing workflows

These automation services reduce manual effort, improve platform reliability, and streamline day-to-day operations.
---


## Technology Stack

| Category | Technologies |
|----------|--------------|
| **Cloud Platform** | Google Cloud Platform (GCP), Virtual Private Cloud (VPC), Cloud Router, Cloud NAT, Cloud Storage, Cloud SQL (PostgreSQL), Artifact Registry |
| **Infrastructure as Code** | Terraform |
| **Container Platform** | Docker, Google Kubernetes Engine (GKE) |
| **GitOps & Continuous Delivery** | ArgoCD, Argo Rollouts, Kustomize |
| **CI/CD** | GitHub Actions |
| **Traffic Management** | Gateway API, NGINX Gateway Fabric |
| **Security** | Kyverno, Falco, Workload Identity Federation, Kubernetes RBAC, Pod Security Standards (PSS), External Secrets Operator, Cosign, Trivy, SBOM |
| **Secrets & Certificates** | Vault, External Secrets Operator, Google Secret Manager, Cert-Manager, Let's Encrypt |
| **Observability** | Prometheus, Grafana, Alertmanager |
| **Autoscaling** | KEDA, Horizontal Pod Autoscaler (HPA), Cluster Autoscaler |
| **Cost Management** | Kubecost |
| **Backup & Disaster Recovery** | Velero |
| **Configuration Management** | Reloader |
| **Databases & Messaging** | PostgreSQL (Cloud SQL), Redis |
| **Programming Languages** | Python, YAML, Bash |
| **Version Control** | Git, GitHub |
---
