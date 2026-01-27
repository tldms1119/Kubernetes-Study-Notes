## ConfigMap

### 📌 Definition
A ConfigMap is used to store **non-confidential** configuration data as key-value pairs. It allows you to **decouple configuration from application code**, making applications more portable and easier to manage.

### 🧪 Useful Commands
```bash
# Create ConfigMap from literal values
kubectl create configmap app-config \
  --from-literal=ENV=dev \
  --from-literal=DEBUG=true

# Create ConfigMap from file
kubectl create configmap app-config \
  --from-file=config.properties

# List ConfigMaps
kubectl get configmaps

# Describe ConfigMap
kubectl describe configmap app-config
```
### 📃 Example ConfigMap Manifest
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  ENV: dev
  DEBUG: "true"
```
### 📃 Example Deployment Using ConfigMap
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo
  template:
    metadata:
      labels:
        app: demo
    spec:
      containers:
        - name: app
          image: busybox
          command: ["sh", "-c", "env && sleep 3600"]
          env:
            - name: ENV
              valueFrom:
                configMapKeyRef:
                  name: app-config
                  key: ENV
            - name: DEBUG
              valueFrom:
                configMapKeyRef:
                  name: app-config
                  key: DEBUG
```
