
# ☸️ Kubernetes Complete Interview & Practical Study Guide

This guide covers **everything you need to master Kubernetes (K8s)** for interviews and real-world DevOps use. It includes architecture, kubectl commands, YAML examples, advanced concepts, and common interview Q&A — ensuring you can confidently answer 90%+ of Kubernetes questions.

---

## 🚀 1. What is Kubernetes?

**Answer:**
Kubernetes is an **open-source container orchestration platform** developed by Google to **automate deployment, scaling, and management** of containerized applications.

**Key Benefits:**
- Automated container deployment and scaling  
- Self-healing (auto-restarts failed pods)  
- Load balancing and service discovery  
- Rolling updates and rollbacks  
- Works across clouds (AWS, Azure, GCP, etc.)

---

## 🧩 2. Kubernetes Architecture

### Core Components

| Component | Description |
|------------|-------------|
| **Master Node (Control Plane)** | Manages the cluster and coordinates workloads |
| **Worker Node** | Runs containerized applications (Pods) |
| **Pod** | Smallest deployable unit (wrapper for one or more containers) |
| **Kubelet** | Agent on each node to manage Pods |
| **Kube Proxy** | Manages networking and routing rules |
| **etcd** | Key-value store that holds cluster state |
| **API Server** | Frontend for Kubernetes control plane |
| **Controller Manager** | Ensures desired state (e.g., pod replicas) |
| **Scheduler** | Assigns pods to nodes based on resource availability |

**Kubernetes Flow:**
1. User submits YAML manifest → API Server  
2. Scheduler assigns pod to a node  
3. Kubelet creates containers via Docker/Containerd  
4. Controller ensures pod matches desired state  

---

## 🧰 3. Kubectl Command Cheat Sheet

| Task | Command |
|------|----------|
| View cluster info | `kubectl cluster-info` |
| List nodes | `kubectl get nodes` |
| List pods | `kubectl get pods` |
| View pod details | `kubectl describe pod <pod>` |
| Create resource | `kubectl apply -f file.yaml` |
| Delete resource | `kubectl delete -f file.yaml` |
| Get deployments | `kubectl get deployments` |
| Logs from a pod | `kubectl logs <pod>` |
| Exec into container | `kubectl exec -it <pod> -- /bin/bash` |

---

## 🧱 4. Core Kubernetes Objects

### 1. **Pod**
Smallest unit of deployment.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: nginx
    ports:
    - containerPort: 80
```

### 2. **ReplicaSet**
Ensures the desired number of pods are running.
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: nginx
        image: nginx
```

### 3. **Deployment**
Manages ReplicaSets and rolling updates.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: nginx
        image: nginx:latest
```

### 4. **Service**
Exposes pods to network traffic.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort
```

### 5. **Namespace**
Logical partition for resources.
```bash
kubectl create namespace dev
kubectl get ns
```

---

## 🧩 5. Kubernetes Networking

- Each pod gets a **unique IP address**.  
- Pods communicate via **ClusterIP** services.  
- External access via **NodePort** or **LoadBalancer**.  
- **Ingress Controller** provides advanced routing (e.g., NGINX Ingress).

**Ingress Example:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: myapp-service
            port:
              number: 80
```

---

## 💾 6. Kubernetes Storage

**PersistentVolume (PV):**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

**PersistentVolumeClaim (PVC):**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

## ⚙️ 7. ConfigMaps & Secrets

**ConfigMap Example:**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_ENV: production
```

**Secret Example:**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  password: cGFzc3dvcmQ=   # base64 encoded
```

---

## 📦 8. DaemonSets, StatefulSets, and Jobs

| Resource | Purpose |
|-----------|----------|
| **DaemonSet** | Ensures one pod per node (e.g., logging agents) |
| **StatefulSet** | For stateful apps like DBs (persistent identity) |
| **Job** | Runs a task to completion |
| **CronJob** | Schedules recurring tasks |

---

## ☁️ 9. Kubernetes with Docker, Jenkins, and AWS

- Docker builds images → pushed to registry (DockerHub/ECR).  
- Jenkins triggers `kubectl apply -f` for CI/CD.  
- AWS EKS (Elastic Kubernetes Service) runs managed clusters.

**Jenkins Pipeline Example:**
```groovy
pipeline {
    agent any
    stages {
        stage('Deploy to K8s') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl rollout status deployment/myapp-deploy'
            }
        }
    }
}
```

---

## 🧠 10. Kubernetes Interview Questions (with Answers)

**Q1: What is the difference between a Pod and a Deployment?**  
**A:** Pod is a single running instance; Deployment manages multiple pods and their updates.

**Q2: What is the purpose of a Service in Kubernetes?**  
**A:** To expose and load balance traffic to Pods.

**Q3: How do you perform a rolling update?**  
**A:** By updating the image in Deployment → `kubectl apply -f deployment.yaml`.

**Q4: What is the difference between ReplicaSet and ReplicationController?**  
**A:** ReplicaSet is the newer and more flexible version supporting label selectors.

**Q5: How do you expose a pod externally?**  
**A:** Using a **NodePort** or **LoadBalancer** service.

**Q6: What is an Ingress Controller?**  
**A:** It manages external HTTP/S traffic and routing to services.

**Q7: What is Helm in Kubernetes?**  
**A:** A package manager for K8s that manages charts (collections of YAML files).

**Q8: What is the difference between ConfigMap and Secret?**  
**A:** Both store configuration data; Secrets store sensitive info (base64 encoded).

**Q9: How do you check cluster health?**  
**A:** `kubectl get componentstatuses` or `kubectl get nodes`.

**Q10: What happens if a node fails?**  
**A:** Kubelet stops responding → Control Plane reschedules pods on another node.

---

## 🔍 11. Troubleshooting Kubernetes

| Problem | Command / Fix |
|----------|----------------|
| Pod stuck in CrashLoopBackOff | `kubectl logs <pod>` |
| Pod pending | Check node resources → `kubectl describe pod <pod>` |
| Service not reachable | Check service endpoints → `kubectl get ep` |
| Image pull error | Verify image path & credentials |
| Node not ready | `kubectl describe node <node>` |

---

## 🧾 12. Best Practices

- Use Namespaces for isolation  
- Manage secrets securely (avoid plaintext)  
- Use Readiness and Liveness probes  
- Keep YAML files in version control (Git)  
- Implement RBAC for user permissions  
- Enable autoscaling (`kubectl autoscale deployment myapp --min=2 --max=5 --cpu-percent=80`)  

---

## 🏁 13. Quick Revision Commands

| Task | Command |
|------|----------|
| Get pods | `kubectl get pods` |
| Get deployments | `kubectl get deploy` |
| Apply YAML | `kubectl apply -f file.yaml` |
| Delete resource | `kubectl delete -f file.yaml` |
| Check logs | `kubectl logs <pod>` |
| Access container | `kubectl exec -it <pod> -- bash` |
| Scale deployment | `kubectl scale deployment myapp --replicas=5` |
| Describe pod | `kubectl describe pod <pod>` |

---

## ✅ Final Tip

> Practice by deploying a full **3-tier application (frontend, backend, DB)** on Minikube or AWS EKS. Once you understand deployments, services, and scaling, you’ll be ready for any Kubernetes interview or real-world DevOps task.

---
