## 🚀 CI/CD Pipeline with GitHub Actions

### 📖 Overview

This document describes the Continuous Integration (CI) and Continuous Delivery (CD) pipeline implemented for the **Production-Inspired Platform Engineering on Google Kubernetes Engine (GKE)** project.

The platform follows a **GitOps-based CI/CD architecture**, where GitHub Actions is responsible for building and validating application artifacts, while Argo CD handles deployment by continuously reconciling the desired state stored in the GitOps repository.

This separation creates a secure, repeatable, and fully automated deployment workflow.

---
## 📑 Table of Contents

* [📖 Overview](#-overview)
* [🎯 CI/CD Goals](#-cicd-goals)
* [🏗️ CI/CD Architecture](#️-cicd-architecture)
* [⚙️ Pipeline Workflow](#️-pipeline-workflow)
* [🔨 Continuous Integration](#-continuous-integration)
* [🚀 Continuous Delivery](#-continuous-delivery)
* [📦 Artifact Management](#-artifact-management)
* [🛡️ Security Pipeline](#️-security-pipeline)
* [🔄 GitOps Integration](#-gitops-integration)
* [📂 GitHub Actions Workflow](#-github-actions-workflow)
* [📊 Pipeline Benefits](#-pipeline-benefits)
* [⚠️ Challenges Encountered](#️-challenges-encountered)
* [🎓 Key Learnings](#-key-learnings)
* [📝 Summary](#-summary)

---
## 🎯 CI/CD Goals

The pipeline was designed with the following objectives:

* Fully automated application builds
* Continuous code validation
* Container image security scanning
* Software supply chain security
* Automated image publishing
* GitOps-based deployments
* Immutable application releases
* Repeatable deployments
* Production-inspired delivery workflow

---
## 🏗️ CI/CD Architecture

<p align="left">
  <img src="images/gitops.png" width="550" alt="CI/CD Architecture">
</p>

The pipeline separates Continuous Integration from Continuous Delivery.

GitHub Actions builds and validates application artifacts, while Argo CD deploys them to Kubernetes using GitOps.

---
## ⚙️ Pipeline Workflow

The CI/CD workflow follows these stages:

1. Developer pushes code to GitHub.
2. GitHub Actions starts the CI pipeline.
3. Application is built and tested.
4. Docker image is created.
5. Image is scanned using Trivy.
6. SBOM is generated.
7. Image is signed using Cosign.
8. Image is pushed to Google Artifact Registry.
9. GitOps repository image tag is updated.
10. Argo CD detects the Git commit.
11. Kubernetes cluster is synchronized.

---
## 🔨 Continuous Integration

GitHub Actions performs all build-related activities.

The pipeline includes:

* Source checkout
* Dependency installation
* Application build
* Unit testing
* Docker image build
* Image tagging
* Vulnerability scanning
* SBOM generation
* Image signing
* Image publishing

The CI pipeline never deploys resources directly to Kubernetes.

---
## 🚀 Continuous Delivery

Continuous Delivery is implemented using Argo CD.

Once GitHub Actions updates the GitOps repository:

* Argo CD detects the change.
* Desired state is compared with the cluster.
* Kubernetes resources are synchronized.
* Applications are updated automatically.

Deployment responsibility remains completely separate from the CI pipeline.

---
## 📦 Artifact Management

Container images are stored in **Google Artifact Registry**.

Each pipeline execution:

* Builds a new container image
* Applies a unique image tag
* Pushes the image to Artifact Registry
* Updates the corresponding image reference in the GitOps repository

This ensures that Kubernetes deployments always reference immutable image versions.

---
## 🛡️ Security Pipeline

Security is integrated into every build.

### Trivy

Every container image is scanned for known vulnerabilities before publication.

This helps identify:

* Operating system vulnerabilities
* Language package vulnerabilities
* High and critical CVEs

---
### Software Bill of Materials (SBOM)

An SBOM is generated for every build.

The SBOM provides:

* Package inventory
* Dependency visibility
* Software supply chain transparency

---
### Cosign

Container images are digitally signed using Cosign.

Benefits include:

* Image integrity verification
* Supply chain protection
* Trusted deployments

Only verified images proceed through the deployment workflow.

---
## 🔄 GitOps Integration

Instead of deploying directly to Kubernetes, GitHub Actions updates the GitOps repository.

The pipeline automatically updates the Kubernetes manifests with the newly published image tag.

Workflow:

```text
Application Repository
        │
GitHub Actions
        │
Build Image
        │
Push Image
        │
Update GitOps Repository
        │
Argo CD
        │
Google Kubernetes Engine
```

This approach makes Git the single source of truth for deployments.

---
## 📂 GitHub Actions Workflow

The pipeline consists of the following logical stages.

| Stage          | Description                         |
| -------------- | ----------------------------------- |
| Checkout       | Clone application source code       |
| Build          | Compile application                 |
| Test           | Execute unit tests                  |
| Docker Build   | Build container image               |
| Trivy Scan     | Scan image for vulnerabilities      |
| SBOM           | Generate Software Bill of Materials |
| Cosign         | Digitally sign container image      |
| Push Image     | Publish image to Artifact Registry  |
| Update GitOps  | Update Kustomize image tag          |
| Commit Changes | Push updated manifests              |

---
## 📊 Pipeline Benefits

The CI/CD implementation provides:

* Automated builds
* Immutable container images
* Continuous validation
* Vulnerability scanning
* Secure software supply chain
* GitOps deployment workflow
* Reduced manual intervention
* Version-controlled deployments
* Faster release cycles
* Repeatable application delivery

---
## ⚠️ Challenges Encountered

During implementation several challenges were addressed:

* Workload Identity authentication
* Artifact Registry permissions
* Image tagging strategy
* GitHub Actions authentication with Google Cloud
* Automated GitOps repository updates
* Cosign keyless signing
* Trivy integration
* Managing environment-specific image updates with Kustomize

These challenges were resolved through iterative testing, GitHub Actions debugging, IAM configuration, and GitOps workflow validation.

---
## 🎓 Key Learnings

This implementation provided hands-on experience with:

* GitHub Actions
* CI pipeline automation
* Docker image lifecycle
* Google Artifact Registry
* Container vulnerability scanning
* Software supply chain security
* Cosign image signing
* GitOps automation
* Kubernetes deployment workflows
* Production-inspired CI/CD practices

---
## 📝 Summary

The platform implements a modern cloud-native CI/CD pipeline by combining GitHub Actions with GitOps principles.

GitHub Actions automates application validation, container image creation, vulnerability scanning, SBOM generation, image signing, and artifact publishing. Deployment is delegated to Argo CD, which continuously synchronizes the Kubernetes cluster with the desired state stored in Git.

This architecture provides a secure, automated, and repeatable software delivery process aligned with modern Platform Engineering and DevSecOps practices.

---
