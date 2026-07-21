

# Kubernetes Day 1 – Introduction & Architecture

## Today's Goal

By the end of today, you should understand:

* What Kubernetes is
* Why Kubernetes was created
* Problems it solves
* Kubernetes Architecture
* Important components
* Your first Kubernetes commands (without affecting your office cluster)

---

# Step 1: Why do we need Kubernetes?

Imagine you've developed a BRM REST API.

```
Spring Boot Application
        |
      Docker
        |
   Running Container
```

Everything works fine.

Now your company receives **10,000 requests per minute**.

Problems begin:

* One container is not enough.
* Need multiple containers.
* If one container crashes, users cannot access the application.
* Updates should happen without downtime.
* Containers must automatically restart.
* Traffic should be distributed evenly.

Managing all of this manually becomes nearly impossible.

This is exactly why Kubernetes exists.

---

# Step 2: What is Kubernetes?

**Definition**

> Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, networking, and management of containerized applications.

Simply put:

Docker creates containers.

Kubernetes manages thousands of containers.

Think of it like this:

```
Docker
    ↓
Creates Containers

Kubernetes
    ↓
Manages Containers
```

---

# Step 3: Real-world analogy

Imagine a restaurant.

Without a manager:

* Chef doesn't come
* Waiter disappears
* Tables are unmanaged
* Orders get lost

Restaurant fails.

Now add a restaurant manager.

The manager:

* Hires more chefs when customers increase.
* Replaces sick chefs.
* Assigns tables.
* Ensures smooth operation.

Kubernetes is that manager.

Containers are the chefs.

---

# Step 4: What Kubernetes does

Kubernetes automatically:

✅ Starts containers

✅ Stops containers

✅ Restarts failed containers

✅ Adds more containers during high traffic

✅ Removes extra containers when traffic decreases

✅ Updates applications without downtime

✅ Monitors application health

---

# Step 5: Kubernetes Architecture

```
                  Users
                    |
               Load Balancer
                    |
             +----------------+
             | Control Plane  |
             +----------------+
               |    |      |
      API Server Scheduler Controller
               |
        ----------------------
        |                    |
   Worker Node 1        Worker Node 2
        |                    |
     Pods                 Pods
        |                    |
   Containers          Containers
```

---

# Step 6: Components Overview

### 1. Control Plane (Master)

This is the brain of Kubernetes.

It decides:

* Where Pods run
* Which node gets new Pods
* What happens if a Pod crashes
* Cluster health

---

### 2. Worker Node

A worker node actually runs your applications.

Example:

```
Worker Node

Docker / containerd

Pod 1
Pod 2
Pod 3
```

---

### 3. Pod

A Pod is the smallest deployable unit in Kubernetes.

Most Pods contain one container.

Example:

```
Pod

┌────────────────┐
│ Nginx Container│
└────────────────┘
```

---

### 4. Node

A machine (physical or virtual) that runs Pods.

Example:

```
AWS VM

↓

Node

↓

Pod

↓

Container
```

---

### 5. Cluster

A Kubernetes cluster is simply a collection of nodes.

```
Cluster

Node 1

Node 2

Node 3

Node 4
```

---

# Step 7: Important Components

| Component          | Responsibility                            |
| ------------------ | ----------------------------------------- |
| API Server         | Entry point for all Kubernetes requests   |
| Scheduler          | Chooses which node runs a Pod             |
| Controller Manager | Keeps the desired state of the cluster    |
| etcd               | Stores all cluster data                   |
| Kubelet            | Runs on each worker node and manages Pods |
| Container Runtime  | Runs containers (containerd, CRI-O, etc.) |

---

# Step 8: Flow of a Deployment

Suppose you run:

```bash
kubectl apply -f nginx.yaml
```

The flow is:

```
kubectl

↓

API Server

↓

etcd stores desired state

↓

Scheduler selects Node

↓

Kubelet creates Pod

↓

Container Runtime starts Container
```

This is the basic lifecycle you'll use constantly.

---

# Step 9: Kubernetes vs Docker

| Docker             | Kubernetes          |
| ------------------ | ------------------- |
| Creates containers | Manages containers  |
| Single host        | Multiple hosts      |
| Manual scaling     | Automatic scaling   |
| Manual recovery    | Automatic recovery  |
| Limited networking | Advanced networking |
| No self-healing    | Self-healing        |

---

# Step 10: Commands You'll Learn Soon

Don't worry about memorizing these yet.

```bash
kubectl get pods
```

```bash
kubectl get nodes
```

```bash
kubectl describe pod
```

```bash
kubectl logs
```

```bash
kubectl exec
```

These will become second nature as we practice.

---

# Practice Task for Today

Since you don't want to experiment on your office Kubernetes cluster, install a local learning environment first. A good option is:

* **Minikube** (recommended for beginners), or
* **Kind (Kubernetes in Docker)** if you're already comfortable with Docker.

We'll use that environment for all hands-on exercises.

---

# Today's Key Takeaways

* Kubernetes is a **container orchestration platform**.
* Docker **creates** containers; Kubernetes **manages** them.
* A **Cluster** consists of one or more **Nodes**.
* Nodes run **Pods**.
* Pods contain **Containers**.
* The **Control Plane** manages the cluster.

---
