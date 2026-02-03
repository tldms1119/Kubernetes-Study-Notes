## Storage Class

### 📌 Definition
A **StorageClass** defines how storage is dynamically provisioned in a Kubernetes cluster. It allows PersistentVolumes(PVs) to be created automatically when a PersistentVolumeClaim(PVC) is requested.

#### Dynamic Provisioning Flow
```
PVC → StorageClass → Provisioner → PV Created → PVC Binding 
```

### 🔹 volumeBindingMode
- `Immediate` (default): PV created **as soon as PVC is created**
- `WaitForFirstConsumer`: PV created **after Pod is scheduled** (Preferred for cloud environments)

### 🔹 reclaimPolicy
- `Delete`: Delete PV and underlying storage
- `Retain`: Keep PV and data

### 📃 Example StorageClass(Cloud) Manifest
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: false # if it's true, PVC size can be increased (Storage backend must support it)
```

### 📃 Example Using StorageClass in PVC Manifest
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: app-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: standard
  resources:
    requests:
      storage: 5Gi
```
