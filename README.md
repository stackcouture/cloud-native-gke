# Platform Engineering Portfolio

A production-ready Platform Engineering portfolio demonstrating the design, automation, deployment, and operation of a cloud-native application platform on Google Cloud Platform (GCP).

This portfolio showcases modern Platform Engineering practices including Infrastructure as Code, GitOps, Kubernetes, Continuous Integration and Delivery (CI/CD), DevSecOps, observability, policy enforcement, and cost optimization.

## Key Capabilities

- Infrastructure provisioning with Terraform
- Google Kubernetes Engine (GKE)
- GitOps deployments using ArgoCD
- GitHub Actions CI/CD pipelines
- Google Artifact Registry
- Workload Identity Federation (OIDC)
- Cloud SQL for PostgreSQL
- Redis
- Kyverno policy enforcement
- Cert-manager with Let's Encrypt
- External Secrets Operator
- Gateway API
- Prometheus & Grafana
- Kubecost
- Trivy vulnerability scanning
- Cosign image signing
- SBOM generation and attestation
- Kustomize
- Blue-Green and Canary deployments with Argo Rollouts 
- Production-grade Kubernetes architecture

This repository serves as the entry point for the complete Platform Engineering ecosystem and links to the individual repositories that implement each layer of the platform.

---
### Recommended Repository Structure

Platform Engineering Portfolio
│
├── platform-infra
│     Infrastructure as Code
│     
├───.github
│   ├───actions
│   │   └───gcp-auth
│   └───workflows
└───terraform
    ├───environments
    │   ├───dev
    │   │   ├───cloud-sql
    │   │   ├───gke
    │   │   ├───iam
    │   │   ├───networking
    │   │   ├───platform
    │   │   │   ├───argo-rollouts
    │   │   │   ├───argocd
    │   │   │   ├───cert-manager
    │   │   │   ├───external-secrets
    │   │   │   ├───falco
    │   │   │   ├───ingress
    │   │   │   ├───keda
    │   │   │   ├───kubecost
    │   │   │   ├───kyverno
    │   │   │   ├───monitoring
    │   │   │   ├───nginx-gateway
    │   │   │   ├───reloader
    │   │   │   ├───storage-classes
    │   │   │   ├───vault
    │   │   │   └───velero
    │   │   │       
    │   │   └───storage
    │   │       ├───artifact-registry
    │   │       │ 
    │   │       └───cloud-storage
    │   │           
    │   └───prod
    └───modules
        ├───cloud-sql
        ├───gke
        ├───iam
        ├───networking
        ├───platform
        │   ├───argo-rollouts
        │   ├───argocd
        │   ├───cert-manager
        │   ├───external-secrets
        │   ├───falco
        │   ├───ingress
        │   ├───istio
        │   ├───keda
        │   ├───kubecost
        │   ├───kyverno
        │   ├───monitoring
        │   ├───nginx-gateway
        │   ├───reloader
        │   ├───storage-classes
        │   ├───vault
        │   └───velero
        └───storage
            ├───artifact-registry
            └───cloud-storage

gitops-microservices-platform/
├── apps/                        # Business applications
│   ├── vote/
│   │   ├── base/
│   │   └── overlays/
│   │       ├── dev/
│   │       └── prod/
│   ├── result/
│   │   ├── base/
│   │   └── overlays/
│   │       ├── dev/
│   │       └── prod/
│   └── worker/
│       ├── base/
│       └── overlays/
│           ├── dev/
│           └── prod/
│
├── infrastructure/             # Stateful infrastructure (Postgres, Redis, PgAdmin)
│   ├── postgres/
│   ├── redis/
│   ├── pgadmin/
│   └── external-secrets-sa/
│
├── platform/					# Shared platform services
│   ├── namespaces/
│   ├── gateway-api/
│   ├── ingress/
│   ├── clusterissuer/
│   ├── cluster-secrets/
│   ├── monitoring/
│   │   ├── postgres-exporter/
│   │   └── redis-exporter/
│   └── velero/
│	
├── security/					# Security policies & runtime protection
│   ├── kyverno/
│   ├── falco/
│   └── network-policies/
│
├── governance/					# Resource quotas & namespace governance
│   ├── argocd/
│   ├── cert-manager/
│   ├── monitoring/
│   ├── postgres/
│   ├── redis/
│   └── vote/
│
├── automation/					# CronJobs & platform automation
│   ├── common/
│   └── daily-platform-report/
│
├── argocd/						# ArgoCD Projects & ApplicationSets
	├── applicationsets/
	└── projects/
 
	  

├── voting-app  Application Source Code
│     ├── vote
│     ├── result
│     ├── worker
│     └── GitHub Actions CI


	  
├── platform-automation
│     └── Daily-platform-report 

---
