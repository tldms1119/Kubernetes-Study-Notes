## Canary Deployment

### 📌 Definition
A Canary Deployment releases a new version to a small subset of users first. Traffic is split between stable and canary versions by running multiple deployments with different replica counts.

> Traffic distribution is proportional to the number of Pods

### Key Notes
- Gradual rollout with reduced risk
- Easy to increase canary traffic by scaling replicas
- Kubernetes Service does not support weighted routing natively (only relies on the number of pods in each deployment)
- Advanced traffic control requires Ingress or service mesh (ex. Istio)

### 📃 Example Stable Deployment Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-stable
spec:
  replicas: 9
  selector:
    matchLabels:
      app: my-app
      track: stable
  template:
    metadata:
      labels:
        app: my-app
        track: stable
    spec:
      containers:
        - name: app
          image: my-app:v1
```

### 📃 Example Canary Deployment Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-canary
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
      track: canary
  template:
    metadata:
      labels:
        app: my-app
        track: canary
    spec:
      containers:
        - name: app
          image: my-app:v2
```

### 📃 Example Service Manifest
```yaml
apiVersion: v1
kind: Service
metadata:
  name: app-service
spec:
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 80
```
