# ✅ To-Do Reminder App with Flask, MongoDB & Kubernetes

A cloud-native **To-Do Reminder Application** built with **Flask** and **MongoDB**, deployed on **Kubernetes** and scalable on platforms like **Minikube** and **AWS EKS**. This project showcases container orchestration, deployment strategies, replication, health monitoring, and alerting in a modern microservices environment.

> 🧠 Built as part of **CS-GY 9223: Cloud Computing Assignment** at NYU Tandon  
> 👩‍💻 By: Swetha Jagadeesan & Abhishek Srikumar  
> 🧑‍🏫 Instructor: Prof. Sambit Sahu

---

## 🚀 Project Highlights

- 🛠️ Flask + MongoDB To-Do App (Add, delete, list tasks)
- 🐳 Fully containerized using Docker
- ☸️ Kubernetes deployment (Minikube & AWS EKS)
- 🔁 ReplicationController with auto-scaling and self-healing
- 🔄 Zero-downtime rolling updates
- ❤️‍🔥 Health checks (Liveness & Readiness probes)
- 📢 Prometheus + Alertmanager integration with Slack for alerting

---

## 🧱 Tech Stack

- **Frontend**: HTML + JS (served via Flask)
- **Backend**: Flask (Python)
- **Database**: MongoDB
- **Containerization**: Docker
- **Orchestration**: Kubernetes (Minikube & AWS EKS)
- **Monitoring**: Prometheus + Alertmanager
- **Cloud**: AWS (EKS Cluster)

---

## 🗂️ Project Structure

```
.
├── backend/                 # Flask App
│   ├── app.py              # Main API
│   ├── requirements.txt
│   └── Dockerfile
├── k8s/                    # Kubernetes YAML manifests
│   ├── Deployment.yaml
│   ├── Services.yaml
│   ├── flask-app-rc.yaml   # ReplicationController
│   ├── Deployment_Rolling.yaml
│   ├── Deployment_Health.yaml
│   ├── mongodb-pvc.yaml
│   └── rule-file.yaml      # Prometheus alerting rule
├── docker-compose.yml
└── README.md
```

---

## 🧪 Local Setup using Docker Compose

1. **Build Docker image**:
```bash
docker build -t swetha0009/your-flask-app:latest .
```

2. **Run with Docker Compose**:
```bash
docker-compose up
```

3. **Access app**: [http://localhost:5001](http://localhost:5001)

4. **Stop**:
```bash
docker-compose down
```

---

## ☸️ Kubernetes Deployment

### 🔹 On Minikube

1. **Start Minikube**:
```bash
minikube start
```

2. **Enable tunneling (for external access)**:
```bash
minikube tunnel
```

3. **Apply resources**:
```bash
kubectl apply -f mongodb-pvc.yaml
kubectl apply -f Deployment.yaml
kubectl apply -f Services.yaml
```

4. **Access app**:
```bash
minikube service flask-service --url
```

---

### 🔸 On AWS EKS

1. **Create EKS cluster** via AWS Console  
2. **Configure kubectl**:
```bash
aws eks --region us-east-1 update-kubeconfig --name flask-app-cluster
```

3. **Deploy**:
```bash
kubectl apply -f mongodb-pvc.yaml
kubectl apply -f Deployment.yaml
kubectl apply -f Services.yaml
```

4. **Verify**:
```bash
kubectl get pods
kubectl get services
```

---

## 🔁 ReplicationController (High Availability)

- Defined in `flask-app-rc.yaml`
- Example:
```yaml
replicas: 4
```

- Auto-recovers if a pod crashes:
```bash
kubectl delete pod <pod-name>
kubectl get pods  # New pod automatically created
```

- Scale up/down by updating the replicas count.

---

## 🔄 Rolling Updates

- Implemented in `Deployment_Rolling.yaml`
- Use `RollingUpdate` strategy to avoid downtime during version upgrades.
```bash
kubectl apply -f Deployment_Rolling.yaml
kubectl rollout status deployment flask-app
```

---

## ❤️‍🩹 Health Monitoring

### Flask App

- Exposes `/healthz` endpoint

### Kubernetes Probes

Defined in `Deployment_Health.yaml`:
```yaml
livenessProbe:
  httpGet:
    path: /healthz
readinessProbe:
  httpGet:
    path: /healthz
```

- Test with broken app version → Pods restart automatically

---

## 📢 Alerting with Prometheus + Slack

1. **Install using Helm**:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack
```

2. **Apply Prometheus rules**:
```bash
kubectl apply -f rule-file.yaml
```

3. **Configure Alertmanager**:  
   Use Slack webhook to receive alerts when pods fail.

---

## 🧼 Cleanup

```bash
# For Minikube
minikube stop
minikube delete

# For AWS
eksctl delete cluster --name flask-app-cluster
```

---

## 🧑‍💻 Authors

- **Swetha Jagadeesan**  
  [GitHub](https://github.com/Swetha3009) | [LinkedIn](https://www.linkedin.com/in/swetha-jagadeesan-972b821b4/)

- **Abhishek Srikumar**

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙌 Acknowledgements

- NYU Tandon, CS-GY 9223 Cloud Computing
- Docker, Kubernetes, AWS EKS
- Prometheus + Alertmanager
