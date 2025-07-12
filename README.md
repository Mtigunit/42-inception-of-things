# 🚀 Inception-of-Things (IoT)

A hands-on **Kubernetes & DevOps lab** using **Vagrant**, **K3s**, **K3d**, and **Argo CD**, designed to teach you how to deploy scalable apps, set up GitOps pipelines, and manage clusters on local virtual machines.

---

## Project Overview

**Inception-of-Things** aims to:
- Build a minimal Kubernetes environment using **K3s** on Vagrant VMs.
- Deploy and expose **multiple applications** via Ingress.
- Set up **K3d** for local Docker-based clusters.
- Automate application deployment with **Argo CD** & GitOps.
- [Bonus] Integrate **GitLab** for a full local CI/CD pipeline.

---

## Repo Structure

```
📦inception-of-things
 ┣ 📂bonus
 ┃ ┣ 📂confs
 ┃ ┃ ┣ 📜argocd.yaml
 ┃ ┃ ┗ 📜gitlab-values.yaml
 ┃ ┗ 📂scripts
 ┃ ┃ ┗ 📜install.sh
 ┣ 📂p1
 ┃ ┣ 📂scripts
 ┃ ┃ ┣ 📜install_k3s_agent.sh
 ┃ ┃ ┗ 📜install_k3s_server.sh
 ┃ ┗ 📜Vagrantfile
 ┣ 📂p2
 ┃ ┣ 📂configs
 ┃ ┃ ┣ 📂app1
 ┃ ┃ ┃ ┣ 📜app1-configMap.yaml
 ┃ ┃ ┃ ┣ 📜app1-deployment.yaml
 ┃ ┃ ┃ ┗ 📜app1-service.yaml
 ┃ ┃ ┣ 📂app2
 ┃ ┃ ┃ ┣ 📜app2-configMap.yaml
 ┃ ┃ ┃ ┣ 📜app2-deployment.yaml
 ┃ ┃ ┃ ┗ 📜app2-service.yaml
 ┃ ┃ ┣ 📂app3
 ┃ ┃ ┃ ┣ 📜app3-configMap.yaml
 ┃ ┃ ┃ ┣ 📜app3-deployment.yaml
 ┃ ┃ ┃ ┗ 📜app3-service.yaml
 ┃ ┃ ┗ 📜my-ingress.yml
 ┃ ┣ 📂scripts
 ┃ ┃ ┗ 📜install_k3s_server.sh
 ┃ ┗ 📜Vagrantfile
 ┣ 📂p3
 ┃ ┣ 📂confs
 ┃ ┃ ┗ 📜argocd-app.yaml
 ┃ ┗ 📂scripts
 ┃ ┃ ┗ 📜install.sh
 ┣ 📜.gitignore
 ┣ 📜README.md
 ┗ 📜iot.pdf
```
---

## Parts Breakdown

### Part 1 — K3s with Vagrant

Create **2 Vagrant VMs**:  
- **Server**: `192.168.56.110`
- **ServerWorker**: `192.168.56.111`  
Install **K3s**:  
- Master mode on Server  
- Agent mode on Worker  
Access cluster with **kubectl**.

---

### Part 2 — Deploy 3 Applications

Use **Ingress** to expose apps by hostname:  
- `app1.com` → App1  
- `app2.com` → App2 (3 replicas)  
- Default → App3  
Test by editing `/etc/hosts` on your local machine to map `192.168.56.110` to `app1.com`, etc.

---

### Part 3 — K3d & Argo CD GitOps

Use **K3d** for a local Docker-based cluster.  
Install **Argo CD** in its own namespace.  
Link Argo CD to your public **GitHub repo**.  
Deploy an application with **2 versions** (`v1` and `v2`) via GitOps.  
Test version upgrade by changing the image tag and pushing to Git.

---

### Bonus — GitLab CI/CD

Optional: run **GitLab** in its own namespace (`gitlab`).  
Integrate GitLab with your cluster for full local CI/CD.

---

## Requirements

- **Vagrant**
- **VirtualBox**
- **kubectl**
- **Docker**
- **K3s / K3d**
- **Argo CD**
- **GitHub & DockerHub accounts**

---

## How to Run

### 1. Launch Vagrant VMs
```bash
cd p1
vagrant up
```

SSH into each machine:
vagrant ssh Server
vagrant ssh ServerWorker

### 2. Deploy K3s & Apps
```bash
cd ../p2
vagrant up
```

### 3. Setup K3d & Argo CD
```bash
cd ../p3
./scripts/setup.sh
```

Access **Argo CD UI** at `http://localhost:8080` (default).

### 4. Bonus: Setup GitLab (Optional)
```bash
cd ../bonus
./scripts/setup_gitlab.sh
```
