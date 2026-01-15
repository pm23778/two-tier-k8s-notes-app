# ================================================
# 🚀 Full Two-Tier Kubernetes Notes App Setup + GitHub Push
# ================================================



This project demonstrates a **Two-Tier Application Architecture** deployed on **Kubernetes** using:
- **Backend (API)**
- **MySQL Database (StatefulSet)**

It is designed for **learning, practice, and DevOps portfolio showcase**.

---

## ⚙️ Components Used

### 1️⃣ Namespace
- Name: `notes-app`
- Purpose: Isolates all application resources

### 2️⃣ Backend Deployment
- Runs backend container
- Image: `prashanrmaurya/two-tier-backend:latest`
- Exposed on port `5000`
- Uses environment variables to connect MySQL

### 3️⃣ Backend Service
- Type: `ClusterIP`
- Exposes backend internally inside cluster

### 4️⃣ MySQL StatefulSet
- Ensures **stable network identity**
- Uses **Persistent Volume Claim**
- Image: `prashanrmaurya/mysql:latest`

### 5️⃣ MySQL Headless Service
- `clusterIP: None`
- Required for StatefulSet DNS resolution

---

## 📌 Prerequisites

- Docker
- Kubernetes cluster (Minikube / Kind / Cloud)
- `kubectl` configured and working

Check cluster:
\`\`\`bash
kubectl get nodes
\`\`\`

---

## 🚀 How to Run (Step-by-Step)

### Step 1: Create Namespace
\`\`\`bash
kubectl apply -f namespace.yml
\`\`\`

### Step 2: Deploy MySQL
\`\`\`bash
kubectl apply -f mysql-service.yml
kubectl apply -f mysql-statefulset.yml
kubectl get pods -n notes-app
\`\`\`

### Step 3: Deploy Backend
\`\`\`bash
kubectl apply -f backend-deployment.yml
kubectl apply -f backend-service.yml
kubectl get all -n notes-app
\`\`\`

### Step 4: Access Backend (Port Forwarding)
\`\`\`bash
kubectl port-forward svc/two-tier-backend 5000:5000 -n notes-app
\`\`\`

Open browser or API client:

### Step 5: Cleanup
\`\`\`bash
kubectl delete namespace notes-app
\`\`\` 


##Deploy MySQL
kubectl apply -f mysql-service.yml
kubectl apply -f mysql-statefulset.yml

##Verify MySQL pod:
kubectl get pods -n notes-app
kubectl describe pod <mysql-pod-name> -n notes-app

##Deploy Backend
kubectl apply -f backend-service.yml
kubectl apply -f backend-deployment.yml

##Check backend pods:
kubectl get pods -n notes-app
kubectl describe pod <backend-pod-name> -n notes-app

##Check services:
kubectl get svc -n notes-app

##Access Backend Locally
kubectl port-forward svc/two-tier-backend 5000:5000 -n notes-app

##Open in browser
http://localhost:5000

