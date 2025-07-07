# FlipCoin – GitOps Environments Repository

This repository contains the Kubernetes deployment manifests and Argo CD configurations used to manage the **FlipCoin** application using GitOps principles.

---

## 📌 Problem Statement

As part of building a modern DevSecOps pipeline, we needed a GitOps-based solution to handle the **deployment, promotion, and rollback** of the FlipCoin app. 
Key goals were:

- Ensure **Argo CD** can continuously reconcile desired and actual states
- Maintain separation of concerns between infrastructure and application
- Support automated updates from the CI pipeline with **minimal manual intervention**

---

## 🧱 Repository Structure

```text
gitops-environments/
├── argocd/
│   └── root-app.yaml           # Argo CD Application for syncing the dev environment
├── dev/
    └── flipcoin/
        ├── deployment.yaml     # K8s Deployment manifest
        ├── service.yaml        # K8s Service manifest
        └── kustomization.yaml  # Kustomize base for the dev environment
````
---

## 🚀 Argo CD Integration

We use Argo CD to automatically sync and deploy manifests from this repository. The `argocd/root-app.yaml` file defines an `Application` resource pointing to the `dev/flipcoin` environment.

**Key configuration:**

✅ **Automated Syncing**
✅ **Self-healing deployments**
✅ **Pruning of deleted resources**

---

## 🛠️ Challenges Faced

* Designing a **multi-environment structure** that supports scalability while staying DRY
* Preventing **Argo CD sync loops** from CI/CD pipelines that modify only image tags
* Handling Argo CD application bootstrapping via **Terraform and Helm**
* Coordinating seamless updates from the CI workflow into this repo for image versioning

---

## ✅ Outcome
* CI pipeline updates deployment image tags → Argo CD detects changes and syncs automatically
* Rapid rollback ability by reverting Git commits
* Clear separation of infrastructure (managed via Terraform) and deployments (managed here)

---

## 🔗 Related Repositories

* 💻 [FlipCoin Code & CI/CD Repository](https://github.com/RESTfulAyush/flipCoin.git)
* 🔧 [Terraform Infrastructure Repository](https://github.com/RESTfulAyush/infra-gitops-devsecops.git)
