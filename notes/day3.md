# Kubernetes Day 3 – ReplicaSet

## Objective

Learn why ReplicaSets are required, how they maintain the desired number of Pods, and perform hands-on scaling and self-healing.

---

# What is a ReplicaSet?

A **ReplicaSet** is a Kubernetes resource that ensures a specified number of identical Pods are always running.

If a Pod fails, crashes, or is deleted, the ReplicaSet automatically creates a new Pod to maintain the desired number of replicas.

---

# Why Do We Need a ReplicaSet?

### Problem with a Pod

* A Pod can fail or be deleted.
* Kubernetes will not automatically recreate a standalone Pod.
* This can lead to application downtime.

### Solution

ReplicaSet continuously monitors the Pods and ensures the required number of replicas are always available.

---

# ReplicaSet Features

* Maintains the desired number of Pods.
* Automatically recreates failed or deleted Pods (Self-Healing).
* Supports scaling up and scaling down.
* Uses Labels and Selectors to identify the Pods it manages.

---

# ReplicaSet YAML Structure

```yaml
apiVersion: apps/v1
kind: ReplicaSet

metadata:
  name: nginx-rs

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
      - name: nginx
        image: nginx
```

---

# Explanation of Each Field

## apiVersion

```yaml
apiVersion: apps/v1
```

Specifies the Kubernetes API version.

ReplicaSet belongs to the **Apps API Group**, therefore it uses **apps/v1**.

---

## kind

```yaml
kind: ReplicaSet
```

Specifies the type of Kubernetes resource to create.

Examples:

* Pod
* ReplicaSet
* Deployment
* Service

---

## metadata

```yaml
metadata:
  name: nginx-rs
```

Stores information about the ReplicaSet.

Example:

* Name
* Labels
* Namespace

---

## spec

```yaml
spec:
```

Defines the desired configuration of the ReplicaSet.

Contains:

* replicas
* selector
* template

---

## replicas

```yaml
replicas: 3
```

Specifies the number of Pods that should always be running.

Desired State:

```
Desired Pods = 3
```

If one Pod is deleted:

```
Current Pods = 2

↓

ReplicaSet creates 1 new Pod
```

---

## selector

```yaml
selector:
  matchLabels:
    app: nginx
```

Identifies which Pods belong to the ReplicaSet.

The selector matches Pods based on labels.

---

## template

```yaml
template:
```

Acts as a blueprint for creating new Pods.

Whenever ReplicaSet needs a new Pod, it uses this template.

---

## template.metadata.labels

```yaml
labels:
  app: nginx
```

Assigns labels to the Pods created by the ReplicaSet.

**Important:**

These labels **must match** the selector.

Example:

```yaml
selector:
  matchLabels:
    app: nginx

template:
  metadata:
    labels:
      app: nginx
```

If they do not match, the ReplicaSet cannot manage the Pods.

---

## template.spec

```yaml
spec:
```

Defines the Pod configuration.

Contains:

* Containers
* Images
* Ports
* Volumes
* Environment Variables (later topics)

---

## containers

```yaml
containers:
- name: nginx
  image: nginx
```

Specifies:

* Container Name
* Docker Image

---

# ReplicaSet Workflow

```
kubectl apply -f replicaset.yaml
        │
        ▼
API Server
        │
        ▼
ReplicaSet Created
        │
        ▼
ReplicaSet checks desired replicas
        │
        ▼
Creates Pods using Template
        │
        ▼
Scheduler assigns Pods to Nodes
        │
        ▼
Container Runtime starts Containers
        │
        ▼
Pods become Running
```

---

# Self-Healing

Delete a Pod:

```bash
kubectl delete pod <pod-name>
```

ReplicaSet detects:

```
Desired = 3
Current = 2
```

Automatically creates:

```
New Pod
```

without any manual intervention.

---

# Scaling

Increase replicas:

```bash
kubectl scale rs nginx-rs --replicas=5
```

Result:

```
Desired = 5
Current = 5
```

ReplicaSet creates two additional Pods.

---

Decrease replicas:

```bash
kubectl scale rs nginx-rs --replicas=2
```

Result:

```
Desired = 2
Current = 2
```

ReplicaSet removes the extra Pods.

---

# Commands Practiced

Create ReplicaSet

```bash
kubectl apply -f replicaset.yaml
```

View ReplicaSets

```bash
kubectl get rs
```

View Pods

```bash
kubectl get pods
```

Detailed ReplicaSet Information

```bash
kubectl describe rs nginx-rs
```

Delete a Pod

```bash
kubectl delete pod <pod-name>
```

Scale ReplicaSet

```bash
kubectl scale rs nginx-rs --replicas=5
```

Delete ReplicaSet

```bash
kubectl delete rs nginx-rs
```

---

# Common YAML Errors

Incorrect

```yaml
replica: 3
```

Correct

```yaml
replicas: 3
```

---

Incorrect

```yaml
conatiners:
```

Correct

```yaml
containers:
```

---

# Interview Questions

### What is a ReplicaSet?

A ReplicaSet ensures that the desired number of identical Pods are always running by automatically creating or deleting Pods as required.

---

### What happens if a Pod is deleted?

ReplicaSet detects the missing Pod and creates a new one to maintain the desired replica count.

---

### What is the purpose of `selector`?

It identifies and manages Pods by matching their labels.

---

### Why should `selector.matchLabels` and `template.metadata.labels` match?

Because the ReplicaSet uses the selector to identify and manage the Pods it creates. If the labels do not match, the ReplicaSet cannot recognize those Pods.

---

### Difference Between Pod and ReplicaSet

| Pod                     | ReplicaSet                          |
| ----------------------- | ----------------------------------- |
| Creates a single Pod    | Creates and maintains multiple Pods |
| No self-healing         | Provides self-healing               |
| No scaling              | Supports scaling                    |
| Used for simple testing | Used for high availability          |

---

# Day 3 Outcome

By the end of this session, I learned to:

* Understand the purpose of ReplicaSets.
* Create a ReplicaSet using YAML.
* Explain each section of the ReplicaSet YAML.
* Use labels and selectors.
* Verify ReplicaSets using kubectl commands.
* Observe self-healing by deleting a Pod.
* Scale ReplicaSets up and down.
* Troubleshoot common YAML errors.
