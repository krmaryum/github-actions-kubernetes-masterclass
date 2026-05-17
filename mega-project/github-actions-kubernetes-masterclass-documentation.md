# GitHub Actions Kubernetes Masterclass – Complete Project Documentation

## Project Overview

This project demonstrates a complete DevOps workflow using:

- GitHub Actions CI/CD
- Docker
- Docker Hub
- Kubernetes
- kind (Kubernetes in Docker)
- Frontend + Backend + MySQL Architecture

The application is called **SkillPulse**, a skill tracking platform.

---

# Architecture

```text
Frontend (HTML/JS)
        ↓
Backend API (Go)
        ↓
MySQL Database
```

Deployment Flow:

```text
GitHub Push
    ↓
GitHub Actions CI
    ↓
Docker Image Build
    ↓
Docker Hub Push
    ↓
Kubernetes Deployment
```

---

# Technologies Used

| Technology | Purpose |
|---|---|
| GitHub Actions | CI/CD |
| Docker | Containerization |
| Docker Hub | Image Registry |
| Kubernetes | Container Orchestration |
| kind | Local Kubernetes Cluster |
| MySQL | Database |
| Go | Backend |
| HTML/CSS/JS | Frontend |

---

# Repository

Repository URL:

```text
https://github.com/krmaryum/github-actions-kubernetes-masterclass
```

---

# Project Structure

```text
github-actions-kubernetes-masterclass/
│
├── .github/workflows/
├── backend/
├── frontend/
├── mysql/
├── k8s/
├── docs/
├── docker-compose.yml
├── Makefile
└── README.md
```

---

# Step 1 – Fork Repository

Forked repository from:

```text
LondheShubham153/github-actions-kubernetes-masterclass
```

---

# Step 2 – Configure GitHub Secrets

Opened:

```text
GitHub Repository
→ Settings
→ Secrets and variables
→ Actions
```

Added repository secrets:

| Secret Name | Value |
|---|---|
| DOCKERHUB_USERNAME | krmaryum |
| DOCKERHUB_TOKEN | Docker Hub Access Token |

Added repository variable:

| Variable | Value |
|---|---|
| DEPLOY_ENABLED | true |

---

# Step 3 – Enable GitHub Actions

Opened:

```text
GitHub → Actions
```

Enabled workflows for forked repository.

---

# Step 4 – Trigger CI Pipeline

Created test commit:

```bash
echo "// workflow trigger" >> frontend/js/app.js

git add .
git commit -m "trigger ci with frontend change"
git push origin main
```

---



# Step 5 – GitHub Actions Pipeline Success

Pipeline stages completed:

- Checkout Code
- Docker Login
- Build Backend Image
- Build Frontend Image
- Push Docker Images

GitHub Actions status:

```text
SUCCESS ✅
```

---

# Step 6 – Install kind and kubectl

## Install kind

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-arm64

chmod +x ./kind

sudo mv ./kind /usr/local/bin/kind
```

## Install kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"

chmod +x kubectl

sudo mv kubectl /usr/local/bin/
```

---

# Step 7 – Fix Architecture Issue

Initial problem:

```text
SIGSEGV segmentation violation
```

Root cause:

```text
Wrong kind binary installed (amd64 on arm64 machine)
```

Checked architecture:

```bash
hostnamectl
```

Output:

```text
Architecture: arm64
```

Installed correct ARM64 kind binary.

---

# Step 8 – Create Kubernetes Cluster

Ran:

```bash
make up
```

This created:
- kind Kubernetes cluster
- Docker image loading
- Kubernetes deployments
- Services

---

# Step 9 – Verify Kubernetes Cluster

## Nodes

```bash
kubectl get nodes
```

Output:

```text
skillpulse-control-plane
skillpulse-worker
skillpulse-worker2
```

## Pods

```bash
kubectl get pods -n skillpulse
```

Output:

```text
backend Running
frontend Running
mysql Running
```

## Services

```bash
kubectl get svc -n skillpulse
```

Output:

```text
backend ClusterIP
frontend NodePort
mysql ClusterIP
```

---

# Step 10 – Application Testing

Opened application:

```text
http://localhost:8888
```

Application loaded successfully.

---

# Step 11 – Health Check

Executed:

```bash
curl http://localhost:8888/health
```

Response:

```json
{"status":"healthy"}
```

---

# Final Result

## CI/CD Completed

✅ GitHub Actions Working  
✅ Docker Builds Working  
✅ Docker Hub Push Working  

## Kubernetes Completed

✅ kind Cluster Working  
✅ Frontend Running  
✅ Backend Running  
✅ MySQL Running  
✅ Services Working  

## Application Testing

✅ Browser Access Working  
✅ Health Check Working  

---

# Key Learnings

- GitHub Actions workflow automation
- Docker image build and push
- Docker Hub authentication
- Kubernetes deployments
- kind cluster management
- Debugging CI/CD failures
- ARM64 architecture troubleshooting
- Service exposure using NodePort

---

# Conclusion

This project successfully demonstrates a complete DevOps workflow integrating:
- GitHub Actions
- Docker
- Docker Hub
- Kubernetes
- kind

The application was deployed successfully and verified through browser testing and API health checks.

# Project Status

```text
COMPLETED SUCCESSFULLY ✅
```
