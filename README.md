# Helm GitOps Demo

A cloud-native backend API application with Node.js, Docker, Kubernetes deployment using Helm, and GitOps with ArgoCD.

## Quick Start

### Option 1: Docker Compose (Local Development)
```bash
docker-compose up -d
```

Access: http://localhost:5000

### Option 2: Kubernetes with Helm
```bash
helm install myapp ./myapp
kubectl get pods
```

### Option 3: GitOps with ArgoCD
```bash
kubectl apply -f argocd-app.yaml
```

## Project Structure

```
helm-gitops-demo/
├── backend/           # Node.js Express API
├── myapp/             # Helm Chart
├── docker-compose.yml # Docker Compose config
├── argocd-app.yaml   # ArgoCD manifest
└── README.md          # This file
```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Root endpoint |
| `/health` | GET | Health check |
| `/api/data` | GET | Sample data |

## Commands

### Start/Stop
```bash
docker-compose up -d       # Start
docker-compose down        # Stop
docker-compose ps          # Status
docker-compose logs -f     # Logs
```

### Kubernetes
```bash
helm install myapp ./myapp        # Install
helm upgrade myapp ./myapp        # Upgrade
helm uninstall myapp              # Uninstall
kubectl get pods                  # List pods
kubectl logs -l app.kubernetes.io/name=myapp  # View logs
```

### Testing
```bash
curl http://localhost:5000
curl http://localhost:5000/health
curl http://localhost:5000/api/data
```

## Development

```bash
cd backend
npm install
npm start
```

Backend runs on port 5000.

## Deployment

### Docker
```bash
docker build -t myapp-backend:1.0.0 ./backend
docker push <registry>/myapp-backend:1.0.0
```

### Kubernetes
```bash
helm install myapp ./myapp -f myapp/values.yaml
```

### GitOps (ArgoCD)
```bash
kubectl apply -f argocd-app.yaml
argocd app sync myapp
```

## Configuration

Edit `myapp/values.yaml` to customize:
- `replicaCount` - Number of replicas
- `image.repository` - Container image
- `image.tag` - Image tag
- `autoscaling.enabled` - Enable auto-scaling
- `resources` - CPU/Memory limits

## Features

- ✅ Health checks
- ✅ Auto-scaling (HPA)
- ✅ Security contexts
- ✅ Graceful shutdown
- ✅ Error handling
- ✅ Production-ready

## Troubleshooting

**Port already in use:**
```bash
docker-compose down -v
```

**Images won't build:**
```bash
docker-compose build --no-cache
```

**Check logs:**
```bash
docker-compose logs -f backend
```

## Technology Stack

- **Backend:** Node.js 18, Express
- **Containerization:** Docker
- **Orchestration:** Kubernetes, Helm
- **GitOps:** ArgoCD

## License

MIT

## Author

Kalyani Bambal



