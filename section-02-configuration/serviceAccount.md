## ServiceAccounts

### 📌 Definition
A **ServiceAccount** provides an identity for processes running inside Pods. Pods use ServiceAccounts to authenticate with the Kubernetes API server.

### 🧪 Useful Commands
```bash
# List ServiceAccounts
kubectl get serviceaccounts

# Create ServiceAccount
kubectl create serviceaccount app-sa

# Describe ServiceAccount
kubectl describe serviceaccount app-sa
```

### 📃 Example ServiceAccount Manifest
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: app-sa
```

### 📃 Example Pod Using ServiceAccount
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sa-pod
spec:
  serviceAccountName: app-sa
  containers:
    - name: app
      image: nginx
```
