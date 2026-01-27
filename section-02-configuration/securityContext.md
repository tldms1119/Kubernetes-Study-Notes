## SecurityContext

### 📌 Definition
A **SecurityContext** defines privilege and access control settings for a Pod or Container.

It allows you to control:
- user and group IDs
- file system permissions

### 🧪 Useful Commands
```bash
# View pod security context
kubectl get pod nginx -o yaml
```

### 📃 Example SecurityContext Manifest
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  securityContext:
    runAsUser: 1000
    fsGroup: 2000
  containers:
    - name: nginx
      image: nginx

```
