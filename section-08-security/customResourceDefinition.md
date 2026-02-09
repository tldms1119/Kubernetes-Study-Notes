## Custom Resource Definition

### 📌 Definition
Kubernetes allow you to **extend its API** by defining your own resource types. A **Customer Resource Definition(CRD)** lets you create new kubernetes resources that behave like built-in ones(Pod, Service etc)

#### CRD Flow:
> Create Definition → Custom Resource(YAML) → Controller → Actual behavior

_CRD alone does nothing. A controller is required to make it meaningful._

### 📄 Example Custom Resource Definition Manifest
backup-crd.yaml
```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: backups.example.com
spec:
  group: example.com
  scope: Namespaced    # Namespaced or Cluster-scoped
  names:
    plural: backups
    singular: backup
    kind: Backup
    shortNames:
      - bk
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:      # properties under 'spec' 
            spec:
              type: object
              properties:
                schedule:
                  type: string
                retentionDays:
                  type: integer
                  minimum: 0
                  maximum: 10
```
### 📄 Example Custom Resource Manifest
backup.yaml
```yaml
apiVersion: example.com/v1
kind: Backup
metadata:
  name: my-backup
spec:
  schedule: "0 2 * * *"
  retentionDays: 7
```

### 🧪 Useful Commands
```bash
# Create Custom Resource Definition
kubectl create -f backup-crd.yaml

# Create Custom Resource
kubectl apply -f backup.yaml

# Get backup resources
kubectl get backups
```
