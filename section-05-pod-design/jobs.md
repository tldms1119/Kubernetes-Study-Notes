## Jobs

### 📌 Definition
**Jobs** are used to run one-time tasks in Kubernetes. Unlike Deployments, they are designed for **finite workloads** that terminate after completion.
- completions: Total number of successful pod executions required
- parallelism: Maximum number of pods running at the same time
- backoffLimit: Number of retries before the Job is marked as failed

### ✅ Key Notes
- `restartPolicy` must be `Never` or `OnFailure`
- Jobs are namespace-scoped

### 🧪 Useful Commands
```bash
# Create Job
kubectl apply -f job.yaml

# Get Jobs
kubectl get jobs

# Describe Job
kubectl describe job batch-job

# View Pods created by Job
kubectl get pods --selector=job-name=batch-job
```

### 📃 Example Job Manifest
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: batch-job
spec:
  completions: 6
  parallelism: 3
  backoffLimit: 4
  template:
    spec:
      restartPolicy: Never
      containers:
        - name: worker
          image: busybox
          command: ["sh", "-c", "echo Processing item; sleep 5"]
```
