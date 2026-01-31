## Ingress & Ingress Networking

### 📌 Definition
**Ingress** provides **HTTP/HTTPS routing** to services inside a Kubernetes cluster. It enables routing based on **hostnames** and **URL Paths**, and typically exposes applications to external users.

Ingress consists of:
- **Ingress Controller**: implements the routing logic
- **Ingress Resource**: defines the routing rules

#### Ingress Controller
- watches Ingress resources
- routes external traffic to internal services
- is usually deployed as a Deployment with Service (NodePort / LoadBalancer), ConfigMap, ServcieAccount(RBAC resources)
- Ingress does not work without a controller
- Controller selection is done via `ingressClassName`
- Common Ingress Controllers
  - Nginx Ingress Controller
  - HAProxy Ingress
  - Traefik
  - Cloud provider Controllers (GKE, EKS, AKS)
 
#### Ingress Resource
- defines **routing rules** that map incoming HTTP/HTTPS requests to Services
- supports **Host-based** / **Path-based** / **TLS termination**
- has key Fields:
  - `ingressClassName`: specifies which controller should handle the Ingress
  - `rules`: routing rules (host, path)
  - `backend`: target Service and port
  - `tls`: HTTPS configuration
 
### 🧪 Useful Commands
```bash
# List Ingress resources
kubectl get ingress

# Describe Ingress
kubectl describe ingress app-ingress

# Check Ingress Controller Pods
kubectl get pods -n ingress-nginx
```

### 📃 Example Simple Ingress Resource Manifest
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
spec:
  ingressClassName: nginx
  rules:
    - host: app.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: app-service
                port:
                  number: 80
```

### 📃 Example Path-Based Ingress Resource Manifest
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: path-ingress
spec:
  # # If there is only one Ingress Controller in the cluster, ingressClassName can be omitted.
  ingressClassName: nginx 
  rules:
    - host: example.com
      http:
        paths:
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: api-service
                port:
                  number: 80
          - path: /web
            pathType: Prefix
            backend:
              service:
                name: web-service
                port:
                  number: 80
```

### 📃 Example TLS Ingress Resource Manifest
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: tls-ingress
spec:
  ingressClassName: nginx
  tls:
    - hosts:
        - secure.example.com
      secretName: tls-secret    # TLS requires a Secret of type kubernetes.io/tls
  rules:
    - host: secure.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: secure-service
                port:
                  number: 443
```

  
