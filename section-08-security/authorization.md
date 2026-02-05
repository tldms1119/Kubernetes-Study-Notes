## Authorization.md

### 📌 Definition
**Authorization** determines what an authenticated user or process is allowed to do in a Kubernetes cluster.

> Authentication = Who are you?
> 
> Authorization = What can you do?

Kubernetes supports **multiple authorization modes**, which are evaluated in order.

### 🔹 Authorization Modes Overview

#### 1. Node Authorization
- Used by **kubelets(nodes)** to access the API server
- Restricts nodes so they can only:
  - read Pods assigned to them
  - update their own Node Status
  - read Secrets related to their Pods
- Automatically enabled in most clusters
- Not used by human users

#### 2. ABAC(Attribute-Based Access Control)
- Access decisions based on attributes:
  - user
  - resource
  - namespace
  - verb (list, create, update, delete)
- Uses static policy **JSON** files
- Hard to manage and scale
- Changes require API Server restart (Rarely used today)

#### 3. RBAC(Role-Based Access Control)
- Access is granted based on **Roles** and **Bindings**
- Most commonly used authorization mode
- Fine-grained permissions
- Default in modern Kubernetes

#### 4. Webhook Authorization
- Authorization decisions are delegated to an **external service**
- API server sends a request and waits for allow/deny response
- Flexible and extensible
- Adds latency and complexity
