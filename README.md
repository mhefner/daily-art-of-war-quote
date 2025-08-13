# Daily Art of War Quote

A web application that displays daily quotes from Sun Tzu's "The Art of War" - timeless wisdom for modern times.

## 📖 Overview

This web application serves a curated collection of quotes from Sun Tzu's ancient military treatise "The Art of War," presenting strategic wisdom that remains relevant for business, leadership, and personal development. Each day brings a new quote to inspire and educate.

## ✨ Features

- 📅 Daily rotating quotes from "The Art of War"
- 🌐 Clean, responsive web interface
- 🐳 Containerized with Docker for easy deployment
- 🚀 Ready for GitOps deployment with ArgoCD
- 📱 Mobile-friendly design
- ⚡ Lightweight and fast

## 🚀 Quick Start

### Using Docker

Pull and run the pre-built image:

```bash
docker run -p 8080:80 mhefner1983/daily-art-of-war-quote:latest
```

Then open your browser to `http://localhost:8080`

### Building from Source

1. Clone the repository:
```bash
git clone https://github.com/mhefner/daily-art-of-war-quote.git
cd daily-art-of-war-quote
```

2. Build the Docker image:
```bash
docker build -t daily-art-of-war-quote .
```

3. Run the container:
```bash
docker run -p 8080:80 daily-art-of-war-quote
```

## 🐳 Docker Image

The application is available as a Docker image on Docker Hub:

- **Repository**: `mhefner1983/daily-art-of-war-quote`
- **Tags**: Available tags include `latest` and versioned releases

### Pushing New Versions

```bash
docker push mhefner1983/daily-art-of-war-quote:tagname
```

Replace `tagname` with your desired version (e.g., `v1.0.0`, `latest`).

## ☸️ Kubernetes Deployment

This application is designed for deployment via ArgoCD and GitOps workflows.

### Sample Kubernetes Manifest

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: daily-art-of-war-quote
  labels:
    app: daily-art-of-war-quote
spec:
  replicas: 2
  selector:
    matchLabels:
      app: daily-art-of-war-quote
  template:
    metadata:
      labels:
        app: daily-art-of-war-quote
    spec:
      containers:
      - name: daily-art-of-war-quote
        image: mhefner1983/daily-art-of-war-quote:latest
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "64Mi"
            cpu: "50m"
          limits:
            memory: "128Mi"
            cpu: "100m"
---
apiVersion: v1
kind: Service
metadata:
  name: daily-art-of-war-quote-service
spec:
  selector:
    app: daily-art-of-war-quote
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```

### ArgoCD Application

Create an ArgoCD Application pointing to your Kubernetes manifests:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: daily-art-of-war-quote
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/mhefner/daily-art-of-war-quote
    targetRevision: HEAD
    path: k8s
  destination:
    server: https://kubernetes.default.svc
    namespace: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

## 🛠️ Development

### Prerequisites

- Docker
- Node.js (if developing locally)
- kubectl (for Kubernetes deployment)
- ArgoCD CLI (optional)

### Local Development

1. Fork and clone the repository
2. Make your changes
3. Test locally with Docker:
   ```bash
   docker build -t daily-art-of-war-quote:dev .
   docker run -p 8080:80 daily-art-of-war-quote:dev
   ```
4. Submit a pull request

## 📄 Quote Sources

All quotes are sourced from Sun Tzu's "The Art of War," one of the most influential works on strategy and tactics ever written. The text is in the public domain.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. Areas for contribution include:

- Additional quotes or better translations
- UI/UX improvements
- Performance optimizations
- Documentation improvements
- Kubernetes manifests and Helm charts

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- Sun Tzu for the timeless wisdom
- The open source community for the tools and inspiration
- Contributors who help improve this project

## 📧 Contact

For questions or suggestions, please open an issue on GitHub or contact the maintainer.

---

*"All warfare is based on deception."* - Sun Tzu

**Visit the app and discover your daily dose of strategic wisdom!**
