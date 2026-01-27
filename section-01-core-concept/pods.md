## Pods

### 📌 Definition
A **Pod** is the smallest deployable unit in Kubernetes.  
It represents a single instance of a running application and can contain **one or more containers** that share the same network namespace and storage volumes.

Containers inside a Pod:
- share the same IP address
- can communicate via `localhost`
- are scheduled together on the same node

### 🧪 Useful Commands
```bash
# Create a pod (imperative)
kubectl run nginx --image=nginx

# List pods
kubectl get pods
kubectl get pods -o wide

# Get detailed pod information
kubectl describe pod nginx

# View logs
kubectl logs nginx

# Execute a command inside the container
kubectl exec -it nginx -- bash

# Delete a pod
kubectl delete pod nginx
```

### 📃 Example Pod Manifest
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```
