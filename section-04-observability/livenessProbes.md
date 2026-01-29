## Liveness Probes

### 📌 Definition
Liveness Probes can be configured on a container to periodically check if the application running inside the container is healthy. If the liveness probe fails, the container is considered to be unhealthy and is restarted by Kubernetes.  

### 🔍 Readiness VS Liveness
- Readiness Probe: Determines whether a pod can receive traffic.
- Liveness Probe: Determines whether a container should be restarted.

### 📃 Example Liveness Probes Manifest
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    name: simple-webapp
spec:
  containers:
    - name: simple-webapp
      image: simple-webapp
      ports:
        - containerPort: 8080
      livenessProbe:
        # in case of HTTP
        httpGet:
          path: /api/health
          port: 8080
        # in case of TCP
        tcpSocket:
          port: 3306
        # in case of Exec command
        exec:
          command: ["cat", "/app/is_healthy"]
        initalDelaySeconds: 5
        periodSeconds: 10
        failureThreshold: 5   # the number of retry, default = 3
```
