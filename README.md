# MERN-K8s-ArgoCD Project

This repository contains a full-stack **MERN application** (MongoDB, Express, React, Node.js) deployed on a **Kubernetes cluster** using:

- **Argo CD** for GitOps-based deployment
- **GitHub Actions** for CI/CD automation
- **Prometheus & Grafana** for cluster monitoring

---

## 📁 Project Structure

- `backend_api/` — Express / Node.js backend  
- `frontend-app/` — React frontend  
- `.github/workflows/ci-cd.yaml` — GitHub Actions CI/CD pipeline  

---

## 🔄 CI/CD Pipeline (GitHub Actions)

Triggered on every push to the `main` branch:

### 🧪 Step 1: Test
- Run backend unit tests (`npm test`)
- Run frontend unit tests (`npm run test`) and lint checks (`npm run lint`)

### 🛠️ Step 2: Build & Push
- Build Docker images for backend and frontend
- Tag images with both `latest` and `${BUILD_NUMBER}`
- Push images to Docker Hub

### 🚀 Step 3: Deploy
- Clone the [mern-k8s-manifests](https://github.com/bouthaina/mern-k8s-manifests) repository
- Update image tags in `backend.yaml` and `frontend.yaml`
- Commit and push changes back to the manifests repo
- Argo CD detects the commit and syncs the changes to the cluster

---

## 🔧 Argo CD Integration

- Argo CD is installed in a dedicated namespace on the cluster
- It watches the `mern-k8s-manifests` repository for changes
- When image tags are updated, Argo CD performs a GitOps sync to apply the new deployment

---

## 📊 Monitoring Stack (Prometheus + Grafana)

This project includes a monitoring stack deployed via ArgoCD using the `kube-prometheus-stack` Helm chart.

### 🔧 Setup Details

- **Prometheus** collects metrics from:
  - Kubernetes nodes and pods
  - kube-state-metrics
  - node-exporter
- **Grafana** provides dashboards for:
  - Cluster health (CPU, memory, storage)
  - Pod and container metrics

---

## 🚀 Running Locally / Testing

1. Ensure your Kubernetes cluster is running and accessible  
2. Push any change to the `main` branch → triggers the CI/CD pipeline  
3. Open the Argo CD UI → verify the **Application** status and sync  
4. Access the app via NodePort  
5. Open Grafana to monitor cluster and app metrics

---

## ✅ Summary

This repository demonstrates:
- A full MERN stack deployed on Kubernetes  
- Automated CI/CD with GitHub Actions  
- GitOps deployment using Argo CD  
- Real-time monitoring with Prometheus and Grafana  
