# Spring PetClinic Kubernetes (minikube)

## Prerequisites

Install the required dependencies:

**macOS:**
```bash
brew install colima docker docker-compose minikube kubectl
```

**Linux:**
Install Docker, Docker Compose, Minikube, and kubectl using your distribution's package manager.

## Setup

### 1. Start the Container Runtime

**macOS (Colima):**
```bash
colima start --cpu 4 --memory 8 --disk 60 --runtime docker
```

> Alternatively, you can use Docker Desktop on macOS instead of Colima.

**Linux:**
No additional runtime setup needed — just make sure Docker is running.

### 2. Start Minikube

```bash
minikube start --driver=docker --cpus=4 --memory=8192
```

Verify the cluster is running:
```bash
minikube status
kubectl get nodes
```

### 3. Enable Ingress Addon

```bash
minikube addons enable ingress
```

### 4. Deploy the Application

```bash
git clone https://github.com/bbrockbernd/spring-petclinic-k8s.git
cd spring-petclinic-k8s
kubectl apply -f k8s -n spring-petclinic
kubectl apply -f k8s/services/mysql/mysql-standalone.yaml
kubectl apply -f k8s/ingress/ingress.yml
```

### 5. Configure Local DNS and Access

**macOS:**
```bash
sudo sh -c 'echo "127.0.0.1 petclinic.local" >> /etc/hosts'
minikube tunnel
```

**Linux:**
```bash
sudo sh -c 'echo "$(minikube ip) petclinic.local" >> /etc/hosts'
```

Then visit [http://petclinic.local](http://petclinic.local) in your browser.

## Cluster Management

Stop the cluster:
```bash
minikube stop
```

Delete the cluster (start from scratch):
```bash
minikube delete
```
