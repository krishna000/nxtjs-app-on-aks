# Next.js on AKS with Helm and Terraform

This guide describes how to containerize a **Next.js monolithic application**, push images securely to Docker Hub, deploy on **Azure Kubernetes Service (AKS)** using **Helm charts**, automate with **Terraform**, and monitor with **Grafana**.
---

## 📌 Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Repositories](#repositories)
4. [Containerization](#containerization)
5. [Helm Chart Development](#helm-chart-development)
6. [Publishing Helm Charts](#publishing-helm-charts)
7. [Terraform Automation](#terraform-automation)
8. [Deployment Workflow](#deployment-workflow)
9. [Monitoring with Grafana](#monitoring-with-grafana)
10. [Security Considerations](#security-considerations)
11. [Benefits](#benefits)
12. [Next Steps](#next-steps)

---

## 📖 Overview

We provide a secure, scalable, and automated approach for deploying a Next.js application on AKS using containerization, Helm, and Terraform. Monitoring is integrated with Prometheus and Grafana.

---

## 🏗 Architecture

* **Next.js Application Repo** → Source code + Dockerfile.
* **Helm Chart Repo** → Deployment templates for app and services.
* **Terraform Infrastructure Repo** → Creates AKS, networking, monitoring stack, and supporting Azure resources.
* **Terraform Deployment Repo** → Deploys Helm charts and manages app lifecycle on AKS.
* **Grafana/Prometheus** → Observability and monitoring.

---

## 📂 Repositories

1. **Repo 1 – Application**

   * Next.js code, Dockerfile, CI/CD to build + push Docker image.
2. **Repo 2 – Helm Charts**

   * Templates for Deployment, Service, Ingress, ConfigMaps, Secrets.
   * Packaged and published as Helm charts.
3. **Repo 3 – Terraform Infra**

   * Azure resources provisioning (AKS, networking, Key Vault, monitoring).
4. **Repo 4 – Terraform Deployment**

   * Automates Helm releases and application deployments to AKS.

---

## 📦 Containerization

* Build Docker image with Next.js app.
* Push image to **Docker Hub private repository**.
* Authenticate AKS with `docker-registry` Kubernetes secret.

---

## ⛵ Helm Chart Development

* Define chart with Kubernetes manifests for Deployment, Service, and optional Ingress.
* Configure chart values for image repo, tag, and resource limits.
* Secure configs using Secrets and ConfigMaps.

---

## 🚀 Publishing Helm Charts

### Option A: Docker Hub (Recommended, Free)

* Helm 3 supports pushing charts as **OCI artifacts** to Docker Hub.
* Package → Push → Pull workflow with authentication.
* Charts stored in **private repo**, pulled with Docker credentials.

### Option B: Azure Container Registry (Enterprise Option)

* Provides better AKS integration and Azure AD authentication.
* Small storage cost (~$5/month for Basic SKU).
* Suitable for production.

---

## ⚙️ Terraform Automation

* **Infrastructure Repo** provisions AKS cluster, networking, monitoring, and optional ACR.
* **Application Deployment Repo** deploys Helm charts to AKS using Terraform Helm provider.
* Clear separation ensures modularity, governance, and CI/CD readiness.

---

## 🔄 Deployment Workflow

1. Developer pushes code to **Next.js repo**.
2. CI/CD builds Docker image → Pushes to Docker Hub private repo.
3. Helm chart packaged → Pushed to Docker Hub (OCI registry).
4. Terraform infra repo provisions AKS and supporting resources.
5. Terraform deployment repo applies Helm release.
6. AKS pulls Docker image and Helm chart securely using credentials.

---

## 📊 Monitoring with Grafana

* Deploy **Prometheus + Grafana** via Helm.
* Prometheus scrapes app & cluster metrics.
* Grafana dashboards configured for:

  * App response time
  * Pod CPU/memory utilization
  * Error rates (4xx/5xx)
  * Cluster health
* Alerts integrated with Slack/Teams.

---

## 🔐 Security Considerations

* Store credentials in **Azure Key Vault** or Kubernetes Secrets.
* Restrict repo access via Docker Hub PAT or Azure AD roles.
* Enable RBAC and network policies in AKS.
* Limit access to Helm charts/images to authorized users only.

---

## ✅ Benefits

* **Scalable**: AKS manages scaling automatically.
* **Secure**: Private image and chart repositories.
* **Automated**: Terraform provides reproducible deployments.
* **Observable**: Grafana enables real-time monitoring.
* **Modular**: Separate repos simplify governance.

---

## 📌 Next Steps

* Finalize repository setup.
* Create CI/CD workflows for image builds, Helm packaging, and Terraform.
* Configure Kubernetes secrets for secure pulls.
* Deploy on staging AKS cluster.
* Onboard monitoring dashboards.

---

**End of README.md**
