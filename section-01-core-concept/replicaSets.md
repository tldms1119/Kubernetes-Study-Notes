## ReplicaSets

### 📌 Definition
A **ReplicaSet** ensures that a specified number of **identical Pod replicas** are running at any given time.

If a Pod is deleted or crashes, the ReplicaSet automatically creates a new one to maintain the desired state.  
ReplicaSets use **label selectors** to manage which Pods they control.

> In practice, ReplicaSets are usually **managed by Deployments**, not directly by users.

---

### 🧪 Useful Commands
```bash
# List ReplicaSets
kubectl get rs

# Get detailed information
kubectl describe rs <replicaset-name>

# Create ReplicaSet from YAML
kubectl create -f replicaset.yaml

# Check which pods are managed by a ReplicaSet
kubectl get pods --show-labels

# Delete a ReplicaSet (pods will also be deleted unless --cascade=false)
kubectl delete rs <replicaset-name>
```

### 📃 Example ReplicaSets Manifest yaml
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```
