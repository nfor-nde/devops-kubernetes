# Kubernetes MongoDB + Mongo Express Deployment

This project demonstrates how to deploy **MongoDB** and **Mongo Express** on Kubernetes using:

- Deployments
- Services
- ConfigMaps
- Secrets

The setup is designed for learning Kubernetes fundamentals and can be run locally using **Minikube** or **Kind**.

---

# Prerequisites

Before running this project, install the following tools:

## 1. Install Docker

Kubernetes requires a container runtime.

### Windows

Download and install Docker Desktop:

https://www.docker.com/products/docker-desktop/

Verify installation:

```bash
docker --version
```

### macOS

Install Docker Desktop:

```bash
brew install --cask docker
```

Or download Docker Desktop manually.

Verify:

```bash
docker --version
```

### Ubuntu/Linux

```bash
sudo apt update

sudo apt install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io -y
```

Verify:

```bash
docker --version
```

---

# Install kubectl

kubectl is the command-line tool used to interact with Kubernetes clusters.

## Windows

Using Chocolatey:

```powershell
choco install kubernetes-cli
```

Using Winget:

```powershell
winget install Kubernetes.kubectl
```

Verify:

```bash
kubectl version --client
```

---

## macOS

```bash
brew install kubectl
```

Verify:

```bash
kubectl version --client
```

---

## Ubuntu/Linux

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s \
https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x kubectl

sudo mv kubectl /usr/local/bin/
```

Verify:

```bash
kubectl version --client
```

---

# Install Minikube

Minikube allows you to run Kubernetes locally.

## Windows

```powershell
winget install Kubernetes.minikube
```

Verify:

```bash
minikube version
```

---

## macOS

```bash
brew install minikube
```

Verify:

```bash
minikube version
```

---

## Ubuntu/Linux

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Verify:

```bash
minikube version
```

---

# Alternative: Install Kind

Kind (Kubernetes in Docker) is another lightweight way to run Kubernetes locally.

## Windows

```powershell
winget install Kubernetes.kind
```

---

## macOS

```bash
brew install kind
```

---

## Ubuntu/Linux

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64

chmod +x ./kind

sudo mv ./kind /usr/local/bin/kind
```

Verify:

```bash
kind version
```

---

# Clone Repository

```bash
git clone https://github.com/nfor-nde/devops-kubernetes.git

cd devops-kubernetes
```

---

# Start Kubernetes Cluster

## Using Minikube

```bash
minikube start
```

Verify:

```bash
kubectl get nodes
```

---

## Using Kind

```bash
kind create cluster
```

Verify:

```bash
kubectl get nodes
```

---

# Project Structure

```text
.
├── mongodb-secret.yaml
├── mongodb-configmap.yaml
├── mongodb-deployment.yaml
└── mongo-express-deployment.yaml
```

---

# Deploy the Application

## Step 1: Create Secret

```bash
kubectl apply -f mongodb-secret.yaml
```

Verify:

```bash
kubectl get secrets
```

---

## Step 2: Create ConfigMap

```bash
kubectl apply -f mongodb-configmap.yaml
```

Verify:

```bash
kubectl get configmaps
```

---

## Step 3: Deploy MongoDB

```bash
kubectl apply -f mongodb-deployment.yaml
```

Verify:

```bash
kubectl get pods
kubectl get svc
```

Expected:

```text
mongo
```

---

## Step 4: Deploy Mongo Express

```bash
kubectl apply -f mongo-express-deployment.yaml
```

Verify:

```bash
kubectl get pods
kubectl get svc
```

---

# Check Resources

```bash
kubectl get all
```

Expected output:

```text
mongodb-deployment
mongo-express
mongo
mongo-express-service
```

---

# View Logs

## MongoDB Logs

```bash
kubectl logs deployment/mongodb-deployment
```

## Mongo Express Logs

```bash
kubectl logs deployment/mongo-express
```

---

# Access Mongo Express

## Minikube

Run:

```bash
minikube service mongo-express-service
```

This automatically opens the browser.

---

## Kind

Use port forwarding:

```bash
kubectl port-forward service/mongo-express-service 8081:8081
```

Then open:

```text
http://localhost:8081
```

---

# Login Credentials

## Mongo Express Web Interface

```text
Username: admin
Password: admin123
```

## MongoDB Root User

```text
Username: username
Password: password
```

These values are configured inside:

```text
mongodb-secret.yaml
```

---

# Useful Commands

View all pods:

```bash
kubectl get pods
```

View services:

```bash
kubectl get svc
```

Describe a pod:

```bash
kubectl describe pod <pod-name>
```

Delete everything:

```bash
kubectl delete -f .
```

Delete cluster (Kind):

```bash
kind delete cluster
```

Delete cluster (Minikube):

```bash
minikube delete
```

---

# Learning Objectives

This project demonstrates:

- Kubernetes Deployments
- Kubernetes Services
- ConfigMaps
- Secrets
- Service Discovery
- MongoDB Deployment
- Mongo Express Deployment
- Internal Cluster Networking
- Kubernetes Resource Management

---

## Author

**Nfor Nde Nyambi**

Software Engineer | CEO & Founder, NdeTek

GitHub: https://github.com/nfor-nde

LinkedIn: https://www.linkedin.com/in/nfor-nde/
