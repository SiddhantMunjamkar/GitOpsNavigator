# GitOpsNavigator
# 🚀 Kubernetes GitOps Platform with Progressive Delivery

This project demonstrates a complete GitOps-based CI/CD pipeline using **ArgoCD**, **Kustomize**, **Helm**, **GitHub Actions**, **Prometheus**, and **Grafana**. It supports **canary** and **blue/green** deployment strategies using **Argo Rollouts**, along with automated rollback capabilities based on **Prometheus metrics**.

---

## 🧩 Tech Stack

- **ArgoCD** – GitOps controller to sync Kubernetes manifests from GitHub
- **Helm** – Package manager for Kubernetes apps
- **Kustomize** – Environment-specific configuration overlays
- **GitHub Actions** – CI/CD automation (build/test/push)
- **Prometheus** – Monitoring and metric collection
- **Grafana** – Metrics visualization and dashboards
- **Argo Rollouts** – Progressive delivery controller (Blue/Green & Canary strategies)

---


## 🗺️ Architecture Diagram

This GitOps system works as follows:

1. Developers push code to GitHub.
2. GitHub Actions builds & tests the image, then pushes it to DockerHub.
3. ArgoCD syncs Kubernetes manifests (Kustomize overlays) and pulls the image.
4. Argo Rollouts handles deployment strategies per environment.
5. Prometheus tracks rollout metrics, enabling automatic rollback.
6. Grafana visualizes everything.

📷 **System Design Image**  
<img src="images/ArgoCD_project_architecture.png" width="300" alt="GitOpsNavigator Architecture" />

---
## ⚙️ Setup Instructions

### 1. Install Prometheus (Monitoring)

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

kubectl create namespace monitoring

helm install prometheus prometheus-community/prometheus \
  --namespace monitoring 

  ```

### 2. Install Grafana (Metrics Dashboards)

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

helm install grafana grafana/grafana \
  --namespace monitoring 

  ```

### 3. Install ArgoRollouts into your Cluster
https://argoproj.github.io/argo-rollouts/installation/#controller-installation

```bash
kubectl create namespace argo-rollouts
kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml

```

### 4. Install ArgoCD into your Cluster
https://argoproj.github.io/argo-cd/getting_started/#cluster-installation
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 5. Install ArgoCD Application
https://argoproj.github.io/argo-cd/user-guide/kustomize/#install-the-application-resource
```bash
# For dev deployment
kubectl apply -n argocd -f manifests/argocd/kustomize-application-dev.yaml

# For staging deployment
kubectl apply -n argocd -f manifests/argocd/kustomize-application-staging.yaml

# For prod deployment
kubectl apply -n argocd -f manifests/argocd/kustomize-application-prod.yaml

```
## 🚦 Deployment Strategies

### 🔧 Dev Environment
- Basic Kustomize overlays  
- For development and quick testing

### 🧪 Staging Environment
- Uses Argo Rollouts with **Blue/Green strategy**  
- Safer pre-production testing

### 🚀 Production Environment
- Uses Argo Rollouts with **Canary strategy**
- Integrated with **Prometheus** for rollback
- Monitors **latency**, **error rate**, and **success rate**

---

## 📊 Observability Stack

### 🔹 Prometheus
- Scrapes metrics from rollout controller  
- Automatically triggers rollback if metrics exceed thresholds

### 🔸 Grafana
- Connects to Prometheus  
- Displays real-time monitoring dashboards

---

## ✅ Features

- 🔁 **Automated deployments** via GitOps  
- 🌀 **Canary & Blue/Green** strategies using Argo Rollouts  
- 📉 **Metric-based rollback** with Prometheus  
- 📊 **Real-time dashboards** via Grafana  
- 🛠️ Fully **customizable** with Kustomize  
- 🧪 Integrated with **GitHub Actions** for CI/CD




