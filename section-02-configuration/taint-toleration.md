## Taint & Toleration

### 📌 Definition
- **Taint**: Marks a Node to indicate that **only certain Pods can be scheduled** on it.  
- **Toleration**: Allows a Pod to **tolerate a Node's taint**.

In short: **Taints → Node**, **Tolerations → Pod**,  
used to control which Pods can be scheduled on which Nodes.

### 🧪 Useful Commands
```bash
# Add a taint to a node
kubectl taint nodes node1 color=blue:NoSchedule

# Remove a taint
kubectl taint nodes node1 color:NoSchedule-

# Describe node to see taints
kubectl describe node node1

# Check pods tolerations
kubectl get pod <pod-name> -o yaml
```

### 📃 Example Pod Manifest with Toleration
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: taint-test-pod
spec:
  containers:
    - name: nginx
      image: nginx
  tolerations:
    - key: "color"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
              # NoSchedule: Pod cannot be scheduled on Node → needs toleration
              # PreferNoSchedule: Avoid if possible, not mandatory
              # NoExecute: Existing Pods will be evicted → needs toleration
```
