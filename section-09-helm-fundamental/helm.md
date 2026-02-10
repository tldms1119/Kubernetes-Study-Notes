## Helm

### 📌 Definition
Helm is a **package manager for Kubernetes** that helps you define, install, and manage Kubernetes applications using reusable templates.

Managing raw Kubernetes YAML files becomes difficult as applications grow due to many resources, environment-specific values and repetitive configuration.
Helm solves this by:
- Packaging multiple YAMLs in to a **Chart**
- Using **template + values**
- Managing **application release**

### ✅ Core Concepts
- **Chart**: A Chart is a Helm package including **Kubernetes manifests** and **default configuration values**. It's reusable Kubernetes application **blueprint**.
- **Release**: A Release is a running instance of a Chart in a cluster. One chart has multiple releases and each release has a name/version/revision history.
- **Repository**: A Chart Repository stores and distributes charts (Artifact Hub, Bitnami Helm repo)

### 📁 Helm Chart Structure
```
my-chart/
├── Chart.yaml        # Chart metadata
├── values.yaml       # Default values
├── templates/        # Kubernetes manifests (templated)
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
└── charts/           # Chart dependencies
```

### 🧪 Useful Commands
```bash
# install my-nginx(=release name) from nginx-chart(=chart name)
helm install my-nginx nginx-chart

# Add Bitnami Helm repository to the local Helm repo list
helm repo add bitnami https://charts.bitnami.com/bitnami

# Search for charts related to "nginx" in all added Helm repositories
helm search repo nginx

# Install a Helm chart from a local directory
helm install my-app ./chart

# Upgrade an existing release with a new version of the chart or updated values
helm upgrade my-app ./chart

# Roll back a release to a previous revision
helm rollback my-app 1

# Install a chart with overriding default values
helm install my-app ./my-chart -f values-prod.yaml

# Show revision history for a specific release
helm history my-app

# List all Helm releases in the current namespace
helm list

# List all Helm repositories currently configured in the local environment
helm repo list
```
