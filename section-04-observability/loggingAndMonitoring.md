## Logging & Monitoring

### 🔍 Opensource Comparison for logging
| Category              | Tool                                       | Description                                                                          |
| --------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------ |
| Metrics Collection    | Prometheus                                 | Collects and stores time-series metrics from Kubernetes components and applications. |
| Metrics Visualization | Grafana                                    | Visualizes metrics using dashboards and supports multiple data sources.              |
| Logs                  | EFK Stack (Elasticsearch, Fluentd, Kibana) | Collects, stores, and analyzes logs with full-text search capabilities.              |
| Logs (Lightweight)    | Loki + Grafana                             | Stores logs using labels instead of full indexing, optimized for Kubernetes.         |
| Log Collector         | Fluentd / Fluent Bit                       | Collects logs from nodes and containers and forwards them to log backends.           |

### 🧪 Useful Commands
```bash
# View logs of a specific pod
kubectl logs <pod-name>

# Stream logs in real time (useful for debugging)
kubectl logs -f <pod-name>

# View logs from a specific container inside a pod
kubectl logs <pod-name> -c <container-name>

# View logs from all pods matching a label selector
kubectl logs -l app=<label-name>

# View logs from the previous container instance (after a crash or restart)
kubectl logs <pod-name> --previous

# Display CPU and memory usage of all nodes
kubectl top nodes

# Display CPU and memory usage of pods
kubectl top pods

# Display resource usage of pods in a specific namespace
kubectl top pods -n <namespace>
```
