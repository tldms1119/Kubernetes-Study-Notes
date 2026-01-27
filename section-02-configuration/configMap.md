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
