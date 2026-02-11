## Kustomize

### 📌 Definition
Kustomize is a native Kubernetes configuration customization tool that allows you to modify YAML manifests without templates.

Unlike Helm, Kustomize works by:
- Taking existing YAML files
- Applying patches and overlays
- Producing final manifests

### 📂 Sample Structure 1
```
base/
├── deployment.yaml
├── service.yaml
└── kustomization.yaml
```
kustomization.yaml
```yaml
resources:
  - deployment.yaml
  - service.yaml

# Customization
commonLabels:
  environment: dev
```

### 📂 Sample Structure 2
```
base/
├── deployment.yaml
├── service.yaml
└── overlays/
    ├── dev/
    │   └── kustomization.yaml
    └── prod/
        └── kustomization.yaml

```
kustomization.yaml
```yaml
resources:
  - ../../base

namePrefix: dev-

patches:
  - patch.yaml
```
patch.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
```

### 🧪 Useful Commands
```bash
# overlay using dev kustomization.yaml
kubectl apply -k overlays/dev

# preview output
kubectl kustomize overlays/dev

# overlay using dev kustomization.yaml
kubectl kustomize overlays/dev | kubectl apply -f -
```
#### Helm vs Kustomize
> Helm = more powerful in functionality using templates
> 
> Kustomize = more Kubernetes-native & simpler
