# Helm GitOps Demo

A cloud-native Node.js backend API application deployed using Docker, Kubernetes with Helm charts, and GitOps automation with ArgoCD.

---

## Project Structure

```
helm-gitops-demo/
├── backend/              # Node.js Express API server
│   ├── server.js        # Main application file
│   ├── package.json     # Dependencies
│   └── Dockerfile       # Docker image configuration
├── myapp/               # Helm Chart for Kubernetes
│   ├── Chart.yaml       # Chart metadata
│   ├── values.yaml      # Configuration values
│   └── templates/       # Kubernetes resource templates
├── docker-compose.yml   # Local development setup
├── argocd-app.yaml     # ArgoCD deployment manifest
└── README.md           # This file
```

---

## Prerequisites

Before starting, ensure you have installed:
- **Docker** and **Docker Compose** (for local development)
- **kubectl** (Kubernetes command-line tool)
- **Helm** (Kubernetes package manager)
- **ArgoCD CLI** (optional, for GitOps)

---

## Getting Started

Choose one of the three deployment options below:

---

### Option 1: Local Development with Docker Compose

**Step 1:** Start the application
```bash
docker-compose up -d
```

**Step 2:** Verify the application is running
```bash
docker-compose ps
```

**Step 3:** Test the API
```bash
curl http://localhost:5000
```

**Step 4:** View logs
```bash
docker-compose logs -f backend
```

**Step 5:** Stop the application
```bash
docker-compose down
```

---

### Option 2: Kubernetes Deployment with Helm

**Prerequisites:**
- Kubernetes cluster running (minikube, kind, or cloud provider)

**Step 1:** Install the Helm chart
```bash
helm install myapp ./myapp
```

**Step 2:** Check deployment status
```bash
kubectl get pods
```

**Step 3:** Check service status
```bash
kubectl get svc
```

**Step 4:** View application logs
```bash
kubectl logs -l app.kubernetes.io/name=myapp
```

**Step 5:** Upgrade (if you make changes)
```bash
helm upgrade myapp ./myapp
```

**Step 6:** Uninstall
```bash
helm uninstall myapp
```

---

### Option 3: GitOps Deployment with ArgoCD

**Prerequisites:**
- Kubernetes cluster with ArgoCD installed
- Git repository access

**Step 1:** Deploy using ArgoCD manifest
```bash
kubectl apply -f argocd-app.yaml
```

**Step 2:** Check ArgoCD application status
```bash
argocd app list
argocd app get myapp
```

**Step 3:** Sync the application
```bash
argocd app sync myapp
```

**Step 4:** View application in Kubernetes
```bash
kubectl get pods
```

---

## API Endpoints

The backend provides the following endpoints:

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Root endpoint - returns "Hello World" |
| `/health` | GET | Health check endpoint |
| `/api/data` | GET | Sample data endpoint |

**Test endpoints:**
```bash
curl http://localhost:5000
curl http://localhost:5000/health
curl http://localhost:5000/api/data
```

---

## Configuration

### Customize Helm Deployment

Edit `myapp/values.yaml` to customize:

```yaml
replicaCount: 2                    # Number of pod replicas
image.repository: myapp-backend    # Container image name
image.tag: "1.0.0"                 # Image version
autoscaling.enabled: true          # Enable auto-scaling
autoscaling.minReplicas: 2         # Minimum pods
autoscaling.maxReplicas: 5         # Maximum pods
resources.limits.cpu: "500m"       # CPU limit
resources.limits.memory: "512Mi"   # Memory limit
```

---

## Common Commands

### Docker Compose Commands
```bash
docker-compose up -d              # Start services
docker-compose down               # Stop services
docker-compose ps                 # Show running services
docker-compose logs -f            # View live logs
docker-compose build --no-cache   # Rebuild without cache
```

### Kubernetes Commands
```bash
kubectl get pods                  # List all pods
kubectl get svc                   # List all services
kubectl describe pod <pod-name>   # Show pod details
kubectl logs <pod-name>           # View pod logs
kubectl exec -it <pod-name> sh    # SSH into pod
```

### Helm Commands
```bash
helm install myapp ./myapp        # Install chart
helm upgrade myapp ./myapp        # Upgrade chart
helm uninstall myapp              # Remove chart
helm values myapp                 # Show current values
```

---

## Local Development

To develop the backend application locally:

**Step 1:** Navigate to backend directory
```bash
cd backend
```

**Step 2:** Install dependencies
```bash
npm install
```

**Step 3:** Start the development server
```bash
npm start
```

**Step 4:** The server runs on http://localhost:5000

---

## Building and Pushing Docker Image

**Step 1:** Build the Docker image
```bash
docker build -t myapp-backend:1.0.0 ./backend
```

**Step 2:** Tag the image for your registry
```bash
docker tag myapp-backend:1.0.0 <your-registry>/myapp-backend:1.0.0
```

**Step 3:** Push to registry
```bash
docker push <your-registry>/myapp-backend:1.0.0
```

**Step 4:** Update `myapp/values.yaml` with new image
```yaml
image.repository: <your-registry>/myapp-backend
image.tag: "1.0.0"
```

---

## Troubleshooting

### Port already in use
```bash
docker-compose down -v
```

### Docker image won't build
```bash
docker-compose build --no-cache
```

### Check application logs
```bash
docker-compose logs -f backend
```

### Kubernetes pod not starting
```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

### Check Helm chart syntax
```bash
helm lint ./myapp
helm template myapp ./myapp
```

---

## Technology Stack

- **Runtime:** Node.js 18
- **Framework:** Express.js
- **Containerization:** Docker
- **Orchestration:** Kubernetes, Helm
- **GitOps:** ArgoCD
- **Package Manager:** npm

---

## Features

- ✅ RESTful API endpoints
- ✅ Health checks
- ✅ Auto-scaling (HPA)
- ✅ Security contexts
- ✅ Graceful shutdown
- ✅ Comprehensive logging
- ✅ Production-ready configuration
- ✅ GitOps automation

---

## License

MIT



