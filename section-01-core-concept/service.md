## Services

### 📌 Definition
A **Service** provides a stable network endpoint to access a set of Pods. Because Pods are **ephemeral** and their IPs change, Services use **labels and selectors** to route traffic reliably.

A Service has three types:
- **ClusterIP** (default): Internal access within the cluster
- **NodePort**: External access via `<NodeIP>:<NodePort>`
- **LoadBalancer**: works with **a cloud provider only**

### 🔹 ClusterIP
**ClusterIP** exposes the Service on an internal IP address that is only reachable **inside the cluster**.

It is mainly used for:
- communication between internal components
- backend services accessed by other Pods

#### Characteristics
- Default Service type
- Not accessible from outside the cluster
- Most commonly used Service type

### 🔹 NodePort
**NodePort** exposes the Service on a static port on each Node’s IP address.

Traffic flow: `<NodeIP>`:NodePort → Service → Pod

It is mainly used for:
- simple external access
- testing and development environments

#### Characteristics
- Accessible from outside the cluster
- NodePort range: **30000–32767**
- Not commonly used in production (usually replaced by LoadBalancer or Ingress)

### 🔹 LoadBalancer
LoadBalancer exposes the Service externally using a cloud provider’s managed load balancer.

When a Service of type LoadBalancer is created, Kubernetes requests an external load balancer from the underlying cloud platform and assigns a public IP address.

Traffic Flow: Client → Cloud LoadBalancer → NodePort → Service → Pod

#### Characteristics
- Provides external access via a cloud-managed load balancer
- Automatically creates a NodePort internally
- Commonly used in production environments
- Requires a cloud provider (EKS, GKE, AKS, etc.)

### 🧪 Useful Commands
```bash
# List services
kubectl get services

# Describe a service
kubectl describe service nginx-service

# Expose a deployment as ClusterIP
kubectl expose deployment nginx \
  --type=ClusterIP \
  --port=80 \
  --target-port=80

# Expose a deployment as NodePort
kubectl expose deployment nginx \
  --type=NodePort \
  --port=80 \
  --target-port=80

# Get service endpoints
kubectl get endpoints nginx-service
```
### 📃 Example Service Manifest (ClusterIP)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

### 📃 Example Service Manifest (NodePort)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

### 📃 Example Service Manifest (LoadBalancer)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-lb
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```
