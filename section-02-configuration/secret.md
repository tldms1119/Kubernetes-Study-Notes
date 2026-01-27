## Secret

### 📌 Definition
A Secret is used to store **sensitive data** such as passwords, tokens, or keys. Secrets are similar to ConfigMaps but are **base64-encoded** and intended for confidential information.

### 🧪 Useful Commands
```bash
# Create Secret from literal values
kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=pass123

# List Secrets
kubectl get secrets

# Describe Secret
kubectl describe secret db-secret
```
### 📃 Example Secret Manifest
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  username: YWRtaW4=
  password: cGFzczEyMw==
```

### 📃 Example Deployment Using Secret
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: secret-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: secure
  template:
    metadata:
      labels:
        app: secure
    spec:
      containers:
        - name: app
          image: busybox
          command: ["sh", "-c", "env && sleep 3600"]
          env:
            - name: DB_USER
              valueFrom:
                secretKeyRef:
                  name: db-secret
                  key: username
            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: db-secret
                  key: password
```
