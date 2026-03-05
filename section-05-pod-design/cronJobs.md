## CronJobs

### 📌 Definition
A **CronJob** runs Jobs on a time-based Schedule, similar to Linux cron. Each execution of a CronJob creates a **new Job**
- completions: Total number of successful pod executions required
- parallelism: Maximum number of pods running at the same time
- backoffLimit: Number of retries before the Job is marked as failed
- activeDeadlineSeconds: Once job reaches its time limit, it won't deploy additional pods, even if the `backoffLimit` is not yet reached

#### Cron Schedule Format
```text
* * * * *
| | | | |
| | | | └─ Day of week (0–6)
| | | └── Month (1–12)
| | └── Day of month (1–31)
| └──── Hour (0–23)
└────── Minute (0–59)
```

### ✅ Key Notes
- CronJobs create Jobs, not Pods directly
- Old Jobs are cleaned up based on history limits

### 🧪 Useful Commands
```bash
# Get CronJobs
kubectl get cronjobs

# Describe CronJob
kubectl describe cronjob hello-cron

# Get Jobs created by CronJob
kubectl get jobs
```

### 📃 Example CronJob Manifest
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello-cron
spec:
  schedule: "*/5 * * * *"
  successfulJobsHistoryLimit: 3
  failedJobsHistoryLimit: 1
  jobTemplate:
    spec:
      completions: 1
      parallelism: 1
      template:
        spec:
          restartPolicy: OnFailure
          containers:
            - name: hello
              image: busybox
              command: ["sh", "-c", "date; echo Hello from CronJob"]
```
