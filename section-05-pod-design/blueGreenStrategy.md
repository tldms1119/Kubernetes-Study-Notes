## Blue/Green Deployment Strategy

### 📌 Definition
A **Blue/Green Deployment** runs two identical environments:
- **Blue**: current production version
- **Green**: new version
Traffic is switched from Blue to Green by updating the Service selector once all tests on pods in the Green Deployment have done.

> Besides the built-in strategies (RollingUpdate, Recreate), Kubernetes commonly implements Blue/Green and Canary deployments using multiple Deployments and Services.

### ✅ Key Notes
- Zero-downtime deployment
- Fast rollback by switching the Service selector back
- Requires duplicate environments (higher resource usage)

### 📃 Example Blue Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
      version: v1
  template:
    metadata:
      labels:
        app: my-app
        version: v1
    spec:
      containers:
        - name: app
          image: my-app:v1
```

### 📃 Example Green Manifest
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-green
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
      version: v2
  template:
    metadata:
      labels:
        app: my-app
        version: v2
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
    version: v2   # switch from v1 to v2
  ports:
    - port: 80
      targetPort: 80
``` 
