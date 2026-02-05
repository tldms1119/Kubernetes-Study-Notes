## ClusterRole & ClusterRoleBinding

### 📌 Definition
A **ClusterRole** defines permissions at the cluster level, and a **ClusterRoleBinding** grants those permissions to users, groups or ServiceAccount **accross the entire cluster**.

> Role & RoleBinding = Namespace scope
>
> ClusterRole / ClusterRoleBinding = Cluster scope

### 🧪 Useful Commands
```bash
# List cluster roles
kubectl get clusterroles

# List cluster role bindings
kubectl get clusterrolebindings

# Describe cluster role
kubectl describe clusterrole pod-reader-global

# Check permissions
kubectl auth can-i get pods --all-namespaces

# Check Namespace scope resources
kubectl api-resources --namespaced=true

# Check Cluster scope resources
kubectl api-resources --namespaced=false
```

### 📃 Example ClusterRole Manifest
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: pod-reader-global
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list"]
```

### 📃 Example ClusterRoleBinding Manifest
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-pods-global
subjects:
  - kind: User
    name: alice
    apiGroup: rbac.authorization.k8s.io
  - kind: ServiceAccount
    name: app-sa
    namespace: dev
roleRef:
  kind: ClusterRole
  name: pod-reader-global
  apiGroup: rbac.authorization.k8s.io
```
