
# 🚀 DevOps Coding Assessment – Budget Rails App

This repository contains the Docker, Kubernetes, ArgoCD, and Tekton configurations required to deploy a **Ruby on Rails application with PostgreSQL** using GitOps and CI/CD principles.

---

## 📁 Repository Structure

```
.
├── docker/              # Dockerfile and Docker Compose for local dev
├── apps/                # Kubernetes manifests (Deployments, Services, Ingress, etc.)
├── argocd/              # ArgoCD app & config setup
├── tekton/              # Tekton Tasks, Pipelines, and PipelineRuns
├── screenshots/         # Visual proof of deployment steps
└── README.md            # This documentation
```

---

## ✅ Step-by-Step Breakdown

### ✅ Step 1: Docker (Rails + PostgreSQL)

- **Location**: `docker/`
- **Files**: `Dockerfile`, `docker-compose.yml`
- **How to run locally**:
  ```bash
  cd docker/
  docker-compose up --build
  ```
- App accessible at: `http://localhost:3000`

---

### ✅ Step 2: Kubernetes Deployment

- **Location**: `apps/`
- **Commands to apply**:
  ```bash
  kubectl apply -f namespace.yaml
  kubectl apply -f .
  ```
- PostgreSQL uses a **StatefulSet**.
- Rails app exposed via **Ingress** at `http://budget-app.local`
  > Ensure you add `127.0.0.1 budget-app.local` to `/etc/hosts`

---

### ✅ Step 3: GitOps with ArgoCD

- **Location**: `argocd/`
- **Key Files**:
  - `application.yaml`: Defines the ArgoCD app
  - `argocd-cm.yaml` and `argocd-rbac-cm.yaml`: Config maps
- **Deploy ArgoCD**:
  ```bash
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  ```
- **Port Forward UI**:
  ```bash
  kubectl port-forward svc/argocd-server -n argocd 8080:443
  ```
- Access: [https://localhost:8080](https://localhost:8080)

---

### ✅ Step 4: CI/CD with Tekton

- **Location**: `tekton/`
- **Key Components**:
  - `git-clone-task.yaml`: Clones source code
  - `kaniko-task.yaml`: Builds and pushes Docker image
  - `kaniko-pipeline.yaml`: Pipeline definition
  - `kaniko-pipelinerun.yaml`: Pipeline execution
- **Run pipeline via Tekton Dashboard**:
  ```bash
  kubectl port-forward svc/tekton-dashboard -n tekton-pipelines 9097:9097
  ```
  Visit: [http://localhost:9097](http://localhost:9097)

- **Expected Output**: Image pushed to Docker Hub  
  `docker.io/kodiarasan23/budget-app`

---

## 🔐 Secrets (Do Not Include in Public Repo)

- DockerHub credentials: stored as Kubernetes Secret named `dockerhub-secret`
  ```bash
  kubectl create secret generic dockerhub-secret \
    --type=kubernetes.io/basic-auth \
    --from-literal=username=YOUR_USERNAME \
    --from-literal=password=YOUR_PASSWORD
  ```

---

## 📸 Screenshots

Refer to the `/screenshots/` folder for:

- Docker setup
- Kubernetes app running
- ArgoCD app synced
- Tekton pipeline successful
- Docker Hub image proof

---

## 📦 Submission Notes

- This repository is private and zip archived as required.
- All keys and sensitive data have been excluded.
- Let me know if you require access to the Docker Hub or GitHub repo.

---

## 🙋‍♂️ Candidate Info

- **Name**: Kodi Krishnan  
- **Docker Hub**: [kodiarasan23](https://hub.docker.com/u/kodiarasan23)  
- **GitHub**: [KodiKrishnan](https://github.com/KodiKrishnan)

---

Thank you for reviewing my assessment!
