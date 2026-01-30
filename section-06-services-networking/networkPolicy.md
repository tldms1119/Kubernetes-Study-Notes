## Network Policy

### 📌 Definition
A **NetworkPolicy** controls **network traffic to/from** pods. It allows restricting **ingress**(incoming) and/or **egress**(outgoing) traffic based on labels, namespaces, and ports.
- `PodSelector` selects which pods the policy applies to
- `policyTypes` could be `Ingress`, `Egress` or both
- `ingress` controls the list of allowed incoming rules
- `egress` controls the list of allowed outgoing rules
- `namespaceSelector` selects which namespace the policy applis to
- `ipBlock` allow specific IP address or range to come in/go out

> By default, in fo NetworkPolicy exists, **all traffic is allowed**.

### 🧪 Useful Commands
```bash
# List NetworkPolicies
kubectl get networkpolicy

# Describe NetworkPolicy
kubectl describe networkpolicy allow-from-app

# Test connectivity (requires another Pod)
kubectl exec -it test-pod -- curl http://backend:80
```
### 📃 Example Manifest 1: Allow Ingress from Specific Pods Only
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
    - Ingress
  ingress:
    - from:
        - podSelector:
            matchLabels:
              name: api-pod
      ports:
        - protocol: TCP
          port: 80
```

### 📃 Example Manifest 2: Deny All Egress Except to Certain IP Range
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-backup-policy
spec:
  podSelector: {}
  policyTypes:
    - Egress
  egress:
    - to:
        - ipBlock:
            cidr: 10.0.0.0/24
      ports:
        - protocol: TCP
          port: 80
```
