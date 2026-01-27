## Multi-Container Pods

### 📌 Definition
It indicates a pod which has **more than one containers** for specific purposes.

All containers in a Pod:
- share the same **network namespace** (same IP, can communicate via localhost)  
- share **storage volumes**  
- are **scheduled together** on the same Node

Multi-container Pods are commonly used to implement design patterns such as:
- **Co-located containers**
- **Init containers**  
- **Sidecars**

#### Co-located Containers
- Two or more containers running together in a Pod to perform tightly coupled tasks.

#### Init Containers
- Run before main containers start
- Typically used for setup tasks like waiting for a service to become available or pre-loading configuration or secrets

#### Sidecars
- Auxiliary container that enhances the main container
- Typically used for Logging and monitoring agent or Proxy for traffic

### 📃 Example Multi-Container Pods Manifest - Co-located Container
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    name: simple-webapp
spec:
  containers:
    - name: web-app
      image: web-app
      ports:
        - containerPort: 8080
    - name: main-app
      image: main-app
```

### 📃 Example Multi-Container Pods Manifest - Init Container
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    name: simple-webapp
spec:
  containers:
    - name: web-app
      image: web-app
      ports:
        - containerPort: 8080
  # flow : start db-checker > end db-checker > start api-checker > end api-checker > start web-app
  initContainers:
    - name: db-checker
      image: busybox
      command: 'wait-for-db-to-start.sh'
    - name: api-checker
      image: busybox2
      command: 'wait-for-another-api.sh'
```

### 📃 Example Multi-Container Pods Manifest - Sidecar Container
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    name: simple-webapp
spec:
  containers:
    - name: web-app
      image: web-app
      ports:
        - containerPort: 8080
  # flow : start log-shipper > start web-app > end web-app > end log-shipper
  initContainers:
    - name: log-shipper
      image: busybox
      command: 'setup-log-shipper.sh'
      restartPolicy: Always
```
