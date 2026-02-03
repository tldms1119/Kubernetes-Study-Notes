## KubeConfig

### 📌 definition
**KubeConfig** is a configuration file used to organize information about clusters, users, namespaces, and authentication mechanisms. The `kubectl` command-line tool uses KubeConfig files to find the information required to choose a cluster and communicate with the API server of that cluster. By default, `kubectl` looks for a file named `config` in the `$HOME/.kube` directory.

### ✅ Key Notes
- Three main parts:
  - **Clusters**: Details about the Kubernetes API server (URL) and Certificate Authority(CA)
  - **Users**: Authentication credential for users (Client Certificates, Tokens, or Basic Auth)
  - **Contexts**: An association that ties together a **Cluster**, a **User**, and **NameSpace**(Optional)
- Current Context: Specifies which context is currently active for all `kubectl` commands
- Data Handling: Certificate data can be referenced via a file path or embedded directly as Base64-encoded strings using the `-data`(ex.`certificate-authority-data`)

### 🧪 Useful Command
```bash
# View the current configuration
kubectl config view

# Get the name of the active context
kubectl config current-context

# List all available contexts
kubectl config get-contexts

# Switch to a different context
kubectl config use-context <context-name>

# Create/Update a cluster entry
kubectl config set-cluster developemnt --server=https://1.2.3.4:6443 --certificate-authority=/path/to/ca.crt

# Create/Update a context entry (Linking User and Cluster)
kubectl config set-context dev-user-context --cluster=development --user=dev-user --namespace=order-system

# Run a command using a specific KubeConfig file
kubectl get pods --kubeconfig=/root/custom-config.yaml
```

### 📃 Example KubeConfig Manifest
```yaml
apiVersion: v1
kind: Config
current-context: prod-admin-context
clusters:
- name: production-cluster
  cluster:
    certificate-authority: /etc/kubernetes/pki/ca.crt
    server: https://10.0.0.10:6443

users:
- name: admin-user
  user:
    client-certificate: /root/admin.crt
    client-key: /root/admin.key

contexts:
- name: prod-admin-context
  context:
    cluster: production-cluster
    user: admin-user
    namespace: finance
```
