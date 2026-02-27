## Deployments

### 📌 Definition
A **Deployment** provides declarative updates for Pods and ReplicaSets.

It manages:
- creating ReplicaSets
- rolling updates
- scaling applications
- self-healing via ReplicaSets

> In practice, Deployments are the **most common way to run applications** in Kubernetes.

### 🧪 Useful Commands
```bash
# Create deployment (imperative)
kubectl create deployment nginx --image=nginx --replicas=3

# Apply deployment from YAML
kubectl apply -f deployment.yaml

# List deployments
kubectl get deployments

# Scale deployment
kubectl scale deployment nginx --replicas=5

# Rolling update
kubectl set image deployment/nginx nginx=nginx:alpine
```

### 📃 Example Deployment Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx        # Which Pods do I manage?
  template:
    metadata:
      labels:
        app: nginx      # Pod's label -> Must match the selectors's matchLabels above
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```

