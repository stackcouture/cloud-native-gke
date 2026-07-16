## Platform Overview

This Platform Engineering Portfolio demonstrates a **production-inspired cloud-native platform** built on **Google Kubernetes Engine (GKE)** using modern **Platform Engineering**, **GitOps**, and **Infrastructure as Code (IaC)** practices.

Rather than focusing solely on deploying an application, the portfolio showcases how a reusable Kubernetes platform can be designed, provisioned, secured, operated, and maintained using a modular **multi-repository architecture**. Each repository has a well-defined responsibility, enabling independent development, versioning, and lifecycle management while reflecting practices commonly adopted by engineering teams managing production Kubernetes environments.

---
### Repository Organization

The platform is organized into four repositories:

| Repository                        | Description                                                                                                                                                                 |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **platform-infra**                | Provisions Google Cloud infrastructure and Kubernetes platform services using Terraform.                                                                                    |
| **gitops-microservices-platform** | GitOps repository containing Kubernetes manifests, Kustomize overlays, Argo CD Applications, platform services, security policies, and environment-specific configurations. |
| **voting-app**                    | Microservices application source code, Dockerfiles, automated testing, and GitHub Actions CI pipelines.                                                                     |
| **platform-automation**           | Python-based automation for platform validation, health reporting, scheduled maintenance, and day-2 operational tasks.                                                      |

This separation of responsibilities establishes clear ownership boundaries between infrastructure provisioning, platform configuration, application development, and operational automation. It enables infrastructure changes, application releases, and platform operations to evolve independently while maintaining a consistent GitOps workflow.

---
### Platform Capabilities

The portfolio demonstrates the following Platform Engineering capabilities:

* Infrastructure provisioning with **Terraform**
* Google Kubernetes Engine (**GKE**) cluster management
* GitOps continuous delivery using **Argo CD**
* Kubernetes application management with **Kustomize**
* Progressive delivery using **Argo Rollouts**
* Platform security with **Kyverno** and **Falco**
* Secret management using **External Secrets Operator** and **HashiCorp Vault**
* Traffic management using **Gateway API** and **NGINX Gateway Fabric**
* Monitoring and observability with **Prometheus**, **Grafana**, and **Alertmanager**
* Event-driven autoscaling using **KEDA**
* Automated TLS management with **cert-manager**
* Backup and disaster recovery using **Velero**
* Cost monitoring using **Kubecost**
* Continuous Integration using **GitHub Actions**
* Day-2 platform operations using **Python-based automation**

The overall repository organization reflects production-oriented Platform Engineering principles by separating infrastructure, platform services, GitOps configuration, application source code, and operational tooling into dedicated repositories. This modular approach improves maintainability, promotes reusability, simplifies collaboration, and provides a scalable foundation for managing cloud-native platforms across multiple environments.


---
## Repository Organization

The platform follows a **multi-repository architecture** that separates infrastructure provisioning, GitOps configuration, application development, and operational automation into independent repositories. This separation enables each repository to have a clear ownership boundary, independent versioning, dedicated CI/CD workflows, and a well-defined lifecycle while supporting collaboration across platform and application teams.

| Repository                        | Purpose                                                                                                                                                                                                         |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **platform-infra**                | Provisions Google Cloud infrastructure and Kubernetes platform services using Terraform, including networking, GKE, IAM, Cloud SQL, Artifact Registry, and shared platform components.                          |
| **gitops-microservices-platform** | Serves as the GitOps repository containing Kubernetes manifests, Kustomize overlays, Argo CD Applications, platform services, security policies, governance resources, and environment-specific configurations. |
| **voting-app**                    | Contains the source code for the Vote, Result, and Worker microservices, along with Dockerfiles, unit tests, and GitHub Actions CI pipelines for building, testing, scanning, and publishing container images.  |
| **platform-automation**           | Provides Python-based automation for day-2 platform operations, including health validation, operational reporting, scheduled maintenance, and infrastructure validation tasks.                                 |

This repository organization promotes modularity, improves maintainability, simplifies change management, and aligns with production Platform Engineering practices where infrastructure, platform services, application code, and operational tooling evolve independently while remaining integrated through GitOps workflows.

---