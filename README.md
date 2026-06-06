<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=32&duration=3000&pause=1000&color=00D4FF&center=true&vCenter=true&width=600&lines=Chat+App+K8s+Deployment+%F0%9F%9A%80;Full+Stack+on+Kubernetes+%E2%9A%99%EF%B8%8F;Docker+%7C+K8s+%7C+MongoDB+%F0%9F%94%A5" alt="Typing SVG" />

<br/>

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![RHEL](https://img.shields.io/badge/RHEL_8-EE0000?style=for-the-badge&logo=redhat&logoColor=white)

<br/>

> **A production-style 3-tier real-time chat application fully deployed on Kubernetes**  
> *Built as a fresher DevOps project to demonstrate end-to-end containerisation and orchestration*

<br/>

![GitHub last commit](https://img.shields.io/github/last-commit/kush699425/chat-app-k8s-deployment?color=00D4FF&style=flat-square)
![GitHub repo size](https://img.shields.io/github/repo-size/kush699425/chat-app-k8s-deployment?color=00D4FF&style=flat-square)
![GitHub stars](https://img.shields.io/github/stars/kush699425/chat-app-k8s-deployment?style=flat-square&color=FFD700)

</div>

---

## 📌 Table of Contents

- [About the Project](#-about-the-project)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Screenshots](#-screenshots)
- [What I Learned](#-what-i-learned)

---

## 🧠 About the Project

This project deploys a **full-stack real-time chat application** on a Kubernetes cluster running on **Red Hat Enterprise Linux 8** inside VMware Workstation.

The goal was not just to make the app work — but to follow **real-world DevOps practices**:

- ✅ Each service runs in its own **Kubernetes Pod**
- ✅ All resources are isolated inside a dedicated **Namespace**
- ✅ MongoDB data is persisted using **PersistentVolume + PVC**
- ✅ Services communicate over a **ClusterIP internal network**
- ✅ Docker images are **built locally and pushed to Docker Hub**

---

## 🏗️ Architecture

```
                    ┌─────────────────────────────────────────┐
                    │           Kubernetes Cluster             │
                    │              (chat-app ns)               │
                    │                                          │
  User              │  ┌──────────┐       ┌──────────────┐    │
  ───────►  :8080   │  │ Frontend │──────►│   Backend    │    │
  port-forward      │  │  React   │       │   Node.js    │    │
                    │  │  :80     │       │   :5001      │    │
                    │  └──────────┘       └──────┬───────┘    │
                    │                            │             │
                    │                     ┌──────▼───────┐    │
                    │                     │   MongoDB    │    │
                    │                     │   :27017     │    │
                    │                     │  (PVC: 5Gi)  │    │
                    │                     └──────────────┘    │
                    └─────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Category | Technology | Purpose |
|---|---|---|
| 🖥️ OS | RHEL 8 (VMware) | Host environment |
| 🐳 Containers | Docker | Build & package images |
| ☸️ Orchestration | Kubernetes | Deploy & manage pods |
| ⚛️ Frontend | React + Nginx | UI served via Nginx |
| 🟢 Backend | Node.js + Express | REST API + Socket.io |
| 🍃 Database | MongoDB | Persistent data store |
| 🗂️ Registry | Docker Hub | Store container images |

---

## 📁 Project Structure

```
chat-app-k8s-deployment/
│
├── 📄 namespace.yaml              # Isolated namespace: chat-app
│
├── 📄 frontend-deployment.yaml    # React app (kush699425/chatapp-frontend)
├── 📄 frontend-service.yaml       # ClusterIP on port 80
│
├── 📄 backend-deployment.yaml     # Node.js API (kush699425/chatapp-backend)
├── 📄 backend-service.yaml        # ClusterIP on port 5001
│
├── 📄 mongodb-deployment.yaml     # MongoDB with volume mount
├── 📄 mongodb-service.yaml        # ClusterIP on port 27017
├── 📄 mongodb-pv.yaml             # PersistentVolume (5Gi hostPath)
└── 📄 mongodb-pvc.yaml            # PersistentVolumeClaim (5Gi)
```

---

## 🚀 Getting Started

### Prerequisites

- Kubernetes cluster (Minikube / kubeadm)
- `kubectl` configured and working
- Docker installed (to build images if needed)

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/kush699425/chat-app-k8s-deployment.git
cd chat-app-k8s-deployment
```

### 2️⃣ Create the Namespace

```bash
kubectl create -f namespace.yaml
```

### 3️⃣ Set Up MongoDB Storage

```bash
kubectl apply -f mongodb-pv.yaml
kubectl apply -f mongodb-pvc.yaml
```

### 4️⃣ Deploy All Services

```bash
kubectl apply -f mongodb-deployment.yaml
kubectl apply -f mongodb-service.yaml
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml
```

### 5️⃣ Verify Pods are Running

```bash
kubectl get pods -n chat-app
```

Expected output:

```
NAME                                    READY   STATUS    RESTARTS
backend-deployment-xxxxxxxxx-xxxxx      1/1     Running   0
frontend-deployment-xxxxxxxxx-xxxxx     1/1     Running   0
mongodb-deployment-xxxxxxxxx-xxxxx      1/1     Running   0
```

### 6️⃣ Access the App

```bash
kubectl port-forward -n chat-app service/frontend 8080:80
```

🌐 Open in browser: **http://localhost:8080**

---

## 📸 Screenshots

<div align="center">

### ✅ All Pods Running
![Pods Running](screenshots/pods.png)

### 🌐 Services
![Services](screenshots/services.png)

### 💬 Live App
![App Running](screenshots/app.png)

</div>

> 💡 *Add your own screenshots by creating a `screenshots/` folder and dropping in your images*

---

## 🧪 Verify the Deployment

```bash
# Check all resources in the namespace
kubectl get all -n chat-app

# Check logs if backend is restarting
kubectl logs deployment/backend-deployment -n chat-app

# Describe a pod for detailed events
kubectl describe pod -l app=backend -n chat-app
```

---

## 📖 What I Learned

```
🔷 Creating and using Kubernetes Namespaces for isolation
🔷 Writing Deployment manifests for multi-tier applications
🔷 Connecting services using ClusterIP and DNS names
🔷 Setting up PersistentVolume + PVC for stateful workloads
🔷 Building Docker images and pushing to Docker Hub
🔷 Using kubectl port-forward to access cluster services locally
🔷 Debugging pod restarts using kubectl logs and describe
```

---

## 🐳 Docker Images Used

| Service | Image |
|---|---|
| Frontend | `kush699425/chatapp-frontend:latest` |
| Backend | `kush699425/chatapp-backend:latest` |
| Database | `mongo:latest` |

---

## 🙌 Credits

Original application source: [iemafzalhassan/full-stack_chatApp](https://github.com/iemafzalhassan/full-stack_chatApp)

Kubernetes deployment & configuration by: **Kush Gohil**

---

<div align="center">

### ⭐ If this project helped you, consider giving it a star!

[![GitHub](https://img.shields.io/badge/GitHub-kush699425-181717?style=for-the-badge&logo=github)](https://github.com/kush699425)

*Made with ❤️ and a lot of `kubectl apply`*

</div>
