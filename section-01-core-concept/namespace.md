## Namespaces

### 📌 Definition
A **Namespace** is a logical partition within a Kubernetes cluster.

Namespaces are used to:
- organize resources
- isolate environments (dev / test / prod)
- apply resource quotas and access control

### 🧪 Useful Commands
```bash
# Create namespace
kubectl create namespace dev

# List namespaces
kubectl get namespaces

# Set default namespace for current context
kubectl config set-context --current --namespace=dev

# Create resource in specific namespace
kubectl apply -f pod.yaml -n dev

# Get resources in a namespace
kubectl get pods -n dev
```
