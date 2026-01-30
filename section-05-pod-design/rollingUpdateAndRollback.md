## Rolling Update & Rollback

### 📌 Definition
#### Rolling Update
- Gradually replaces old pods with new ones
- Enables **zero-downtime deployments**
- Controlled by:
  - `maxSurge`: extra pods allowed above desired replicas
  - `maxUnavailable`: Pods allowed to be unavailable during update

#### Rollback
- Reverts a deployment to **a previous revision**
- Used when a rollout causes failures
- Supported **only for Deployments** (Because Deployments keep revision history)

> All fields in a Deployment can be changed, but only changes under `spec.template` trigger a rollout

### 🔁 Recreate vs RollingUpdate

| Feature | Recreate | RollingUpdate |
|------|---------|--------------|
| Update method | Delete all Pods, then create new ones | Gradual Pod replacement |
| Downtime | Yes | No |
| Speed | Fast | Slower |
| Resource usage | Low | Temporarily higher |
| Default strategy | No | Yes |
| Typical use case | DB, single-instance apps | Web / API servers |

### 🧪 Useful Commands
```bash
# After changing yaml file and apply
kubectl apply -f deployment.yaml

# Record change cause
kubectl set image deployment/my-deploy nginx=nginx:1.25 --record

# Check rollout status
kubetl rollout status deployment/my-deploy

# View rollout history
kubectl rollout history deployment/my-deploy
kubectl rollout history deployment/my-deploy --revision=2

# Rollback
kubectl rollout undo deployment/my-deploy
kubectl rollout undo deployment/my-deploy --to-revision=1
```

### 📃 Example Strategy Manifest
#### RollingUpdate
```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 1
    maxUnavailable: 1
```
#### Recreate
```yaml
strategy:
  type: Recreate
```
