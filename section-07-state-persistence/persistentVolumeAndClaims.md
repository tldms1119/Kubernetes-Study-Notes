## Persistent Volumes & Persistent Volume Claim

### 📌 Definition
A **PersistentVolume(PV)** is a **cluster-wide storage resource** provisioned by an administrator or dynamically by a StroageClass. PV exists independently of Pods.

A **PersistentVolumeClaim(PVC)** is a request for storage by a user or Pod. PVC is namespace-scoped and binds to a matching PV. PVC-PV Binding is **one-to-one**, but a PVC can be mounted by multiple Pods in the same namespace.

### ✅ Key Notes
- PV is not **namespace-scoped**
- Created before PVC (static provisioning)
- `hostPath` is mainly for testing (not production)

### 🔹 persistentVolumeReclaimPolicy
- `Delete`: Delete PV and underlying storage
- `Retain`: Keep PV and data

#### PV-PVC Binding Flow
```
Pod → PVC → PV → Physical Storage
```

### 🧪 Useful Commands
```bash
# List PVs
kubectl get pv

# List PVCs
kubectl get pvc

# Describe PV
kubectl describe pv pv-volume

# Describe PVC
kubectl describe pvc pvc-claim
```

### 📃 Example PersistentVolume Manifest
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-volume
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  # In production, AWS EBS(EKS) / NFS / GCP Persistent Disk (CKE) / Azure Disk are commonly used.
  hostPath:
    path: /mnt/data
```

### 📃 Example PersistentVolumeClaim Manifest
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

### 📃 Example Pod Using PVC Manifest
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pvc-pod
spec:
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "sleep 3600"]
      volumeMounts:
        - name: storage
          mountPath: /data
  volumes:
    - name: storage
      persistentVolumeClaim:
        claimName: pvc-claim
```
