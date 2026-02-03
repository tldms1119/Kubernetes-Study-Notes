## RBAC (Role-Based Access Control)

### 📌 Definition
**RBAC** controls access to Kubernetes resources using **Roles** and **Bindings**.
> Permissions are defined in Roles and assigned using Bindings

- **Role**: A Role defines a set of permissions **within a specific namespace**
- **RoleBinding**: A RoleBinding assigns a Role to a **user, group or ServiceAccount** within a namespace

### 🧪 Useful Commands
```bash
# List roles
kubectl get roles -n dev

# List role bindings
kubectl get rolebindings -n dev

# Describe role
kubectl describe role pod-reader -n dev

# Check permissions
kubectl auth can-i get pods -n dev
```

### 📃 Example Roles Manifest
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: dev
rules:
  - apiGroups: [""]        # "" means core such as Pods, Service, ConfigMap etc. (Deployments="apps")
    resources: ["pods"]
    verbs: ["get", "list"]
```

### 📃 Example RoleBinding Manifest
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: dev
subjects:
# Users and Groups come from external authentication systems such as crt, cloud IAM, OIDC(Google, Github)
  - kind: User      
    name: alice
    apiGroup: rbac.authorization.k8s.io
  - kind: ServiceAccount
    name: app-sa
    namespace: dev
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
