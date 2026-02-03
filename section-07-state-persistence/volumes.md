## Volumes

### 📌 Definition
A **Volume** is a directory accessible to containers in a Pod. Its lifecycle is tied to the **Pod**, not the container.

### ✅ Key Notes
- Volume exists as long as the Pod exists
- Data survives container restarts
- Data is lost when Pod is deleted

### 📃 Example Volume Mount Manifest
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-pod
spec:
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "sleep 3600"]
      volumeMounts:
        - name: cache
          mountPath: /cache
  volumes:
    - name: cache
      hostPath:
        path: /data/cache
        type: Directory
      # emptyDir: {}
```
