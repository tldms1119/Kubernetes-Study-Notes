## ClusterRole & ClusterRoleBinding

### 📌 Definition
A **ClusterRole** defines permissions at the cluster level, and a **ClusterRoleBinding** grants those permissions to users, groups or ServiceAccount **accross the entire cluster**.

> Role & RoleBinding = Namespace scope
>
> ClusterRole / ClusterRoleBinding = Cluster scope

### ✅ Scope and RBAC Usage
- In general, **namespace-scoped resources** are controlled using **Roles and RoleBindings**
- **Cluster-scoped resources** must be controlled using **ClusterRoles and ClusterRoleBindings**
- However, **ClusterRole can also be used to define permissions for namespace-scoped resources**, especially when the same permissions need to be reused across multiple namespaces
- The **actual scope of the permission is determined by the binding**, not by the role itself

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
