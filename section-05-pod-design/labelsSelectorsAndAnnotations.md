## Labels & Selectors & Annotations

### 📌 Definition
#### Labels
- Key-value metadata attached to Kubernetes objects (Pods, Services, Deployments, etc)
- Used for grouping, filtering and selecting resources
- can be queried and changed at runtime

#### Selectors
- Used to select a set of objects based on labels
- Commonly used by Services, ReplicaSets, Deployments
- use operators such as =, ==, !=, in, notin, exists

#### Annotations
- Key-value metadata for non-indentifying information
- Not used for selection or filtering
- Ideal for
  - build/version info
  - URLs
  - description

### 🧪 Useful Commands
```bash
# View labels
kubectl get pods --show-labels
kubectl get pods -L app, env

# Filter using selectors
kubectl get pods -l app=web
kubectl get pods -l 'env in (prod,staging)'
kubectl get pods -l 'app!=api'

# Add / update labels
kubectl label pod my-pod tier=backend
kubectl label pod my-pod tier=backend --overwrite

# Remove labels
kubectl label pod my-pod tier-
```

### 📃 Example Manifest
#### Pod with labels & Annotation
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
  labels:
    app: web
    env: prod
  annotations:
    version: "1.0,1"
    description: "Main frontend pod"
spec:
  containers:
    - name: nginx
    image: nginx
```

#### Service using Selector
```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  selector:
    app: web
  ports:
    - port: 80
    targetPort: 80
```
