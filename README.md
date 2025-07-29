# 🚀 Deploy a Dockerized Flask Web App on Kubernetes using Ansible

## 📌 Project Overview

This project demonstrates how to **build, push, and deploy a Flask web application** using:

* **Docker** for containerization
* **Ansible** for automation
* **Kubernetes (Minikube)** for orchestration

All tools are configured on **WSL (Ubuntu)** with **Docker Desktop** and **Minikube (VirtualBox)**.

---

## 🏗️ Architecture

```
Flask App → Docker Image → DockerHub → Kubernetes (Minikube)
                       (Automated using Ansible)
```

---

## 📂 Project Structure

```
flask-k8s-ansible-project/
├── app/
│   ├── app.py                # Flask application
│   └── requirements.txt      # Flask dependencies
├── k8s/
│   ├── deployment.yaml       # K8s Deployment manifest
│   └── service.yaml          # K8s Service manifest
├── ansible/
│   ├── inventory.ini         # Ansible inventory
│   └── deploy.yml            # Ansible playbook (build, push, deploy)
├── Dockerfile                # Dockerfile for Flask app
└── README.md                 # Project documentation
```

---

## ⚙️ Prerequisites

1. **Docker Desktop** with WSL integration enabled
2. **Minikube (VirtualBox driver)** installed and running
3. **WSL (Ubuntu)** with:

   ```bash
   ansible --version
   kubectl version --client
   docker --version
   ```
4. DockerHub account for pushing images

---

## 🚀 Steps to Run

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/<your-username>/flask-k8s-ansible-project.git
cd flask-k8s-ansible-project
```

### 2️⃣ Start Minikube (on Windows terminal)

```bash
minikube start --driver=virtualbox
```

### 3️⃣ Configure Kubernetes Access in WSL

```bash
mkdir -p ~/.kube
cp /mnt/c/Users/<YourWindowsUser>/.kube/config ~/.kube/config
ln -s /mnt/c/Users/<YourWindowsUser>/.minikube ~/.minikube
```

Edit `~/.kube/config` and fix paths (`\` → `/`).

### 4️⃣ Run the Ansible Playbook (in WSL)

```bash
ansible-playbook -i ansible/inventory.ini ansible/deploy.yml
```

---

## 🔎 Verify Deployment

```bash
kubectl get pods
kubectl get svc
```

Access the application in the browser:

```
http://<minikube-ip>:30007
```

Find Minikube IP:

```bash
minikube ip
```

---

## 🛠️ Troubleshooting

1. **Docker module error in Ansible**
   → Use `--break-system-packages` to install required Python packages:

   ```bash
   pip3 install docker kubernetes --break-system-packages
   ```
2. **Config file path issues in WSL**
   → Ensure kubeconfig paths point to `/home/<user>/.minikube/...` and not `C:\Users`.

---

## ✨ Features

* Fully automated container build & deployment using Ansible
* Works with **Minikube** on Windows + WSL
* Modular design with separate manifests & playbook

---

## 🖊️ Author

**Yatindra Panchal**

