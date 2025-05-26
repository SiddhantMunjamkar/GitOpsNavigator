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

## 📁 Project Structure