## Readiness Probes

### 📌 Definition
Even if a pod condition is **Ready**, the application inside the pod may still need time to warm up. To ensure that the application is actually ready to receive traffic, **Readiness Probes** can be used. A pod is marked as **Ready** only when its readiness probe succeeds.

#### Pod Status
- **Pending**: This is the phase where the scheduler tries to find a node to scehdule the pod. If no suitable node is available, the pod remains in Pending status.
- **ContainerCreating**: Once the pod is schedule, it goes into ContainerCreating Status where the required images are pulled and the containers are created.
- **Running**: When all containers in a pod have been created and started, it goes into Running status.

#### Pod Condition
- **PodScheduled**: Indicates whether the pod has been scheduled on to a node. The condition is set to true once scheduling is complete.
- **Initialized**: Indicates whether all init containers have succefully completed. The condition is set to true after initialization finishes.
- **ContainersReady**: Indicates whether is set to true when all container in the pod are ready. The condition is set to true when all containers pass their readiness checks.
- **Ready**: Indicates whether the pod is ready to serve traffic. The condition is set to true **only when all readiness probes succeed**.

> If a readiness probe fails, the pod remains in the Running state, but it is removed from the Service endpoints and does not receive traffic.

### 📃 Example Readiness Probes Manifest
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
      readinessProbe:
        # in case of HTTP
        httpGet:
          path: /health
          port: 8080
        # in case of TCP
        tcpSocket:
          port: 3306
        # in case of Exec command
        exec:
          command: ["cat", "/app/is_ready"]
        initalDelaySeconds: 5
        periodSeconds: 10
        failureThreshold: 5   # the number of retry, default = 3
```
