## Node Affinity

### 📌 Definition
Node Affinity allows Pods to be **scheduled only on Nodes that match certain conditions**.

- **requiredDuringSchedulingIgnoredDuringExecution**: Pod must match the rules to be scheduled  
- **preferredDuringSchedulingIgnoredDuringExecution**: Pod prefers matching Nodes but can be scheduled elsewhere

Affinity is based on **Node labels**.

---

### 🧪 Useful Commands
```bash
# Check node labels
kubectl get nodes --show-labels

# Add a label to a node
kubectl label nodes node1 disktype=ssd

# Describe pod to check nodeAffinity
kubectl get pod <pod-name> -o yaml
```

### 📃 Example Pod Manifest with Node Affinity
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: affinity-pod
spec:
  containers:
    - name: nginx
      image: nginx
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: disktype
                operator: In
                values:
                  - ssd
      preferredDuringSchedulingIgnoredDuringExecution:
        - weight: 1    # Higher weight → higher preference for the scheduler
          preference:
            matchExpressions:
              - key: zone
                operator: In
                values:
                  - zone1
```
