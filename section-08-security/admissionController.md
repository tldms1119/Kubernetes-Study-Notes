## Admission Controller

### 📌 Definition
**Admission Controller** are plugins that **intercept requests to the Kubernetes API server after authentication and authrization**, but **before the object is persisted in etcd**. They can **modify**(mutate) the request or **validate** it.

#### Traffic flow
```
Request → Authentication → Authorization → Admission Controller → etcd
```

### 🔹 Types of Admission Controllers
1. Mutating Admission Controllers
   - Can **change the object before** it is stored
   - Example use cases:
     - Add labels or annotations
     - Inject sidecar containers
     - Apply default values
    
2. Validating Admission Controllers
   - **Cannot modify** the object
   - Only approve or reject the request
   - Example use cases:
     - Enforce naming conventions
     - Ensure required labels are present
     - Validate resource limits
    
### 🔹 Built-in Admission Controllers
| Controller               | Type       | Purpose                                    |
| ------------------------ | ---------- | ------------------------------------------ |
| NamespaceLifecycle       | Validating | Prevent deletion of active namespaces      |
| LimitRanger              | Validating | Enforce resource limits                    |
| ServiceAccount           | Mutating   | Auto-attach default ServiceAccount to Pods |
| DefaultTolerationSeconds | Mutating   | Set default toleration for node taints     |
| ResourceQuota            | Validating | Enforce quotas in namespaces               |
| PodSecurity              | Validating | Enforce security standards                 |

> CKAD focus: Mutating/Validating for Pods, Labels, and default ServiceAccount

### 🔹 Webhook Admission Controllers
- External HTTP callbacks triggered by API server
- Can be mutating or validating
- Useful for custom policy enforcement
