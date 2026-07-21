 **Day 1 Notes** 

---

# Kubernetes Day 1 – Environment Setup

## Objective

Set up a local Kubernetes environment on macOS using **Homebrew**, **Docker Desktop**, **kubectl**, and **Minikube**.

---

# Architecture

```text
                MacBook
                   │
            Homebrew (Package Manager)
                   │
     ┌─────────────┴─────────────┐
     │                           │
 Docker Desktop             kubectl CLI
     │                           │
     └─────────────┬─────────────┘
                   │
              Minikube
                   │
         Local Kubernetes Cluster
                   │
            Control Plane Node
                   │
                  Pods
```

---

# Software Used

| Software       | Purpose                                                     |
| -------------- | ----------------------------------------------------------- |
| Homebrew       | Package manager for macOS                                   |
| Docker Desktop | Container runtime used by Minikube                          |
| kubectl        | Command Line Interface (CLI) to communicate with Kubernetes |
| Minikube       | Creates a local single-node Kubernetes cluster              |

---

# What is Homebrew?

Homebrew is the package manager for macOS.

Instead of downloading applications manually, you can install software using a single command.

Example:

```bash
brew install kubectl
```

Benefits:

* Easy software installation
* Easy upgrades
* Easy removal
* Automatically manages dependencies

---

# Installing Homebrew

Run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installation:

```bash
echo >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv zsh)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv zsh)"
```

Verify:

```bash
brew --version
```

---

# What is Docker?

Docker is a platform used to create and run **containers**.

A container packages:

* Application
* Libraries
* Dependencies
* Runtime

into one portable unit.

Example:

```text
Application
      │
Dependencies
      │
Configuration
      │
Docker Container
```

Without Docker:

"My application works on my laptop but not on another machine."

With Docker:

"The same container runs consistently everywhere."

---

# Installing Docker Desktop

Install using Homebrew:

```bash
brew install --cask docker
```

Or download it from Docker's official website.

After installation:

1. Open Docker Desktop.
2. Accept the license.
3. Wait until Docker is running.

Verify:

```bash
docker --version
```

```bash
docker ps
```

Expected:

```text
CONTAINER ID   IMAGE   COMMAND   CREATED   STATUS   PORTS   NAMES
```

An empty list is normal if no containers are running.

---

# What is kubectl?

`kubectl` is the Kubernetes Command Line Interface (CLI).

It sends commands to the Kubernetes API Server.

Example:

```text
User
   │
kubectl
   │
API Server
   │
Kubernetes Cluster
```

Examples:

```bash
kubectl get pods
```

```bash
kubectl get nodes
```

```bash
kubectl logs
```

```bash
kubectl describe pod
```

Verify installation:

```bash
kubectl version --client
```

---

# What is Minikube?

Minikube creates a **local Kubernetes cluster** on your machine.

Instead of renting cloud infrastructure, Minikube runs Kubernetes locally using Docker.

Example:

```text
MacBook
    │
Docker
    │
Minikube
    │
Kubernetes Cluster
```

It is intended for:

* Learning Kubernetes
* Development
* Testing
* Practice

---

# Installing Minikube

Install:

```bash
brew install minikube
```

Verify:

```bash
minikube version
```

---

# Starting the Cluster

Start Minikube using Docker as the driver:

```bash
minikube start --driver=docker
```

This creates:

* Kubernetes Control Plane
* API Server
* Scheduler
* Controller Manager
* etcd
* Kubelet

---

# Verifying the Cluster

Check the node:

```bash
kubectl get nodes
```

Example:

```text
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   5m    v1.xx.x
```

Check system Pods:

```bash
kubectl get pods -A
```

Check cluster status:

```bash
minikube status
```

Example:

```text
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

---

# Frequently Used Minikube Commands

Start cluster:

```bash
minikube start
```

Stop cluster:

```bash
minikube stop
```

Delete cluster:

```bash
minikube delete
```

Restart cluster:

```bash
minikube stop
minikube start
```

Open dashboard:

```bash
minikube dashboard
```

SSH into the Minikube node:

```bash
minikube ssh
```

---

# Frequently Used Docker Commands

Docker version:

```bash
docker --version
```

Running containers:

```bash
docker ps
```

All containers:

```bash
docker ps -a
```

Docker images:

```bash
docker images
```

System information:

```bash
docker info
```

---

# Frequently Used kubectl Commands

List nodes:

```bash
kubectl get nodes
```

List Pods:

```bash
kubectl get pods
```

All namespaces:

```bash
kubectl get pods -A
```

Cluster information:

```bash
kubectl cluster-info
```

View configuration:

```bash
kubectl config view
```

Current context:

```bash
kubectl config current-context
```

---

# Relationship Between Components

```text
Homebrew
     │
     ├── Installs Docker Desktop
     ├── Installs kubectl
     └── Installs Minikube

Docker Desktop
        │
Runs Containers
        │
Minikube
        │
Creates Local Kubernetes Cluster
        │
kubectl
        │
Communicates with Kubernetes API Server
```

---

# Key Interview Questions

### 1. Why do we need Homebrew?

To install and manage software packages on macOS easily.

### 2. Why do we need Docker?

To package applications and their dependencies into portable containers.

### 3. Why do we need Minikube?

To run a local Kubernetes cluster for development and learning.

### 4. Why do we need kubectl?

To communicate with and manage a Kubernetes cluster.

### 5. Can Kubernetes run without Docker?

Yes. Kubernetes supports multiple container runtimes such as **containerd** and **CRI-O**. Modern Kubernetes commonly uses **containerd**. In our setup, Minikube uses Docker because it's beginner-friendly and already installed.

---

## Day 1 Summary

Today you accomplished the following:

* ✅ Installed Homebrew
* ✅ Installed Docker Desktop
* ✅ Installed Minikube
* ✅ Started a local Kubernetes cluster
* ✅ Verified the cluster with `kubectl`
* ✅ Understood the role of each tool in the Kubernetes ecosystem

---

