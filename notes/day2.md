# Kubernetes Day 2 Notes – YAML & Creating  First Pod

## Objective

Learn how Kubernetes uses YAML files to create resources and understand each section of a Pod YAML file through hands-on practice.

---

# 1. What is YAML?

**YAML (YAML Ain't Markup Language)** is a human-readable configuration file format used to define Kubernetes resources.

Instead of executing multiple commands, we write the desired configuration in a YAML file, and Kubernetes creates or updates the resource accordingly.

### Common Kubernetes resources created using YAML

* Pod
* Deployment
* Service
* ConfigMap
* Secret
* Namespace

---

# 2. Why do we use YAML?

### Advantages

* Human-readable
* Easy to maintain
* Reusable
* Can be stored in Git (Version Control)
* Used in CI/CD pipelines
* Standard approach in real-world projects

---

# 3. Imperative vs Declarative

## Imperative Approach

Uses commands to create resources.

Example:

```bash
kubectl run nginx --image=nginx
```

You tell Kubernetes **how** to perform the action.

---

## Declarative Approach

Uses YAML files.

Example:

```bash
kubectl apply -f pod.yaml
```

You describe **what** the final state should be, and Kubernetes ensures that state.

---

# 4. Structure of a Kubernetes YAML

Every Kubernetes YAML generally contains four main sections.

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
  - name: nginx
    image: nginx
```

---

# 5. Understanding Each Field

## apiVersion

Specifies which Kubernetes API version should process the resource.

Example:

```yaml
apiVersion: v1
```

**Important:**
`apiVersion` is **not** the Kubernetes cluster version.

Examples:

* Pod → `v1`
* Deployment → `apps/v1`

---

## kind

Specifies the type of Kubernetes resource to create.

Examples:

```yaml
kind: Pod
kind: Deployment
kind: Service
```

Changing the `kind` changes the type of resource Kubernetes creates.

---

## metadata

Contains information that identifies the resource.

Example:

```yaml
metadata:
  name: nginx-pod
```

Common metadata fields:

* name
* labels
* namespace
* annotations

(Currently we used only `name`.)

---

## spec

Defines the desired configuration of the resource.

Example:

```yaml
spec:
  containers:
  - name: nginx
    image: nginx
```

The `spec` section tells Kubernetes:

* What container to create
* Which image to use
* How the Pod should be configured

---

# 6. Pod vs Container

A Pod is the smallest deployable unit in Kubernetes.

A Pod contains one or more containers.

Example:

```
Pod (nginx-pod)
│
└── Container (nginx)
      │
      └── Image (nginx)
```

### Difference

| Pod                                | Container                    |
| ---------------------------------- | ---------------------------- |
| Kubernetes resource                | Running instance of an image |
| Can contain one or more containers | Runs the application         |

---

# 7. Complete Pod YAML

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
  - name: nginx
    image: nginx
```

---

# 8. Creating the Pod

Command:

```bash
kubectl apply -f pod.yaml
```

### Meaning

| Part     | Purpose                                      |
| -------- | -------------------------------------------- |
| kubectl  | Kubernetes CLI                               |
| apply    | Create or update a resource                  |
| -f       | Read configuration from a file               |
| pod.yaml | YAML file containing the resource definition |

---

# 9. Internal Flow of kubectl apply

```
pod.yaml
     │
     ▼
kubectl
     │
     ▼
API Server
     │
     ▼
Validation
     │
     ▼
Scheduler
     │
     ▼
Selected Node
     │
     ▼
Pull Image
     │
     ▼
Create Container
     │
     ▼
Pod Running
```

---

# 10. Verify the Pod

Command:

```bash
kubectl get pods
```

Example Output:

```text
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          97s
```

---

# 11. Understanding kubectl get pods Output

## NAME

Displays the Pod name.

Example:

```
nginx-pod
```

---

## READY

Shows:

```
Ready Containers / Total Containers
```

Example:

```
1/1
```

Meaning:

* Total Containers = 1
* Ready Containers = 1

---

## STATUS

Current Pod state.

Common values:

* Pending
* Running
* Completed
* Error
* CrashLoopBackOff

---

## RESTARTS

Number of times Kubernetes restarted the container.

Example:

```
0
```

Means the container has never restarted.

---

## AGE

Shows how long the Pod has existed.

Examples:

* 97s
* 5m
* 2h
* 1d

---

# 12. Common YAML Mistakes

### Incorrect

```yaml
apiVerson: v1
```

Correct

```yaml
apiVersion: v1
```

---

Incorrect

```yaml
kind: pod
```

Correct

```yaml
kind: Pod
```

---

Incorrect

```yaml
name:nginx-pod
```

Correct

```yaml
name: nginx-pod
```

Always maintain proper spelling, capitalization, and spacing.

---

# 13. Interview Questions

### Q1. What is YAML?

YAML is a human-readable configuration file format used to define Kubernetes resources declaratively.

---

### Q2. Why is YAML preferred over commands?

Because it is reusable, version-controlled, easy to maintain, and represents the desired state of Kubernetes resources.

---

### Q3. What is the purpose of `apiVersion`?

It specifies which Kubernetes API version should process the resource.

---

### Q4. What is `kind`?

It specifies the type of Kubernetes resource to create.

---

### Q5. What is `metadata`?

It contains identifying information about the resource, such as name, labels, namespace, and annotations.

---

### Q6. What is `spec`?

It defines the desired configuration of the Kubernetes resource.

---

### Q7. Why does the READY column show `1/1`?

It represents **Ready Containers / Total Containers** inside the Pod.

---

### Q8. What does `kubectl apply -f pod.yaml` do?

It creates the resource if it doesn't exist or updates it if it already exists based on the YAML definition.

---

# Commands Practiced

```bash
minikube status
minikube start

mkdir kubernetes-day2
cd kubernetes-day2

touch pod.yaml

vi pod.yaml

cat pod.yaml

kubectl apply -f pod.yaml

kubectl get pods
```


# Kubernetes Day 2 (Part 2) Notes – Working with Pods

## Objective

Learn how to inspect, troubleshoot, access, and delete Pods using `kubectl` commands.

---

# Kubernetes Pod Lifecycle

```text
Write pod.yaml
      │
      ▼
kubectl apply -f pod.yaml
      │
      ▼
Pod Created
      │
      ▼
kubectl get pods
      │
      ▼
Check Status
      │
      ▼
kubectl describe pod
      │
      ▼
View Complete Details
      │
      ▼
kubectl logs
      │
      ▼
View Application Logs
      │
      ▼
kubectl exec
      │
      ▼
Enter Running Container
      │
      ▼
kubectl delete pod
      │
      ▼
Pod Deleted
```

---

# 1. kubectl describe

## Command

```bash
kubectl describe pod nginx-pod
```

## Purpose

Displays detailed information about a Kubernetes resource.

Unlike `kubectl get`, which provides a summary, `kubectl describe` provides complete details useful for troubleshooting.

---

## Information Displayed

* Pod Name
* Namespace
* Node
* Status
* Pod IP
* Container Details
* Image
* Restart Count
* Conditions
* Events

---

## Important Fields

### Name

```text
Name: nginx-pod
```

Name of the Pod.

---

### Namespace

```text
Namespace: default
```

A Namespace logically separates resources within a Kubernetes cluster.

If no namespace is specified, Kubernetes uses the **default** namespace.

---

### Node

```text
Node: minikube
```

Shows which Kubernetes node is running the Pod.

Hierarchy:

```text
Cluster
   │
Node
   │
Pod
```

---

### Status

```text
Running
```

Current Pod state.

Common values:

* Pending
* Running
* Succeeded
* Failed
* Unknown

---

### IP

```text
10.244.0.5
```

Internal IP address assigned to the Pod.

Pods communicate with each other using Pod IPs.

---

### Container

```text
Container: nginx
```

Shows the container running inside the Pod.

---

### Image

```text
Image: nginx
```

Docker image used to create the container.

---

### Ready

```text
Ready: True
```

Indicates whether the container is ready to accept traffic.

---

### Restart Count

```text
Restart Count: 0
```

Number of times Kubernetes restarted the container.

---

## Events (Very Important)

Example:

```text
Scheduled
Pulling Image
Pulled Image
Created
Started
```

The Events section shows everything Kubernetes did while creating the Pod.

This is one of the first places engineers check when troubleshooting.

---

# 2. kubectl logs

## Command

```bash
kubectl logs nginx-pod
```

## Purpose

Displays logs generated by the application running inside the container.

It shows:

* Standard Output (stdout)
* Standard Error (stderr)

---

## Example

```text
Configuration complete; ready for start up
nginx/1.31.3
start worker processes
```

These logs indicate that the Nginx application started successfully.

---

## Real Project Usage

If an application fails to start, logs may show:

```text
Database connection failed
```

or

```text
Port already in use
```

or

```text
Application Started Successfully
```

Logs help identify application-level issues.

---

# Difference Between describe and logs

| kubectl describe                  | kubectl logs                         |
| --------------------------------- | ------------------------------------ |
| Shows Kubernetes resource details | Shows application logs               |
| Displays Events, Node, IP, Status | Displays stdout and stderr           |
| Used for Pod troubleshooting      | Used for application troubleshooting |

---

# 3. kubectl exec

## Command

```bash
kubectl exec -it nginx-pod -- /bin/bash
```

If Bash is unavailable:

```bash
kubectl exec -it nginx-pod -- /bin/sh
```

---

## Purpose

Executes commands inside a running container.

Used for:

* Debugging
* Viewing files
* Running Linux commands
* Checking configuration
* Troubleshooting applications

---

## Command Breakdown

| Option    | Meaning                      |
| --------- | ---------------------------- |
| exec      | Execute a command            |
| -i        | Interactive input            |
| -t        | Allocate terminal            |
| --        | Separator before the command |
| /bin/bash | Start Bash shell             |

---

## Prompt Change

Before:

```text
radha@MacBookAir ~ %
```

After:

```text
root@nginx-pod:/#
```

This indicates you are inside the container.

---

## Linux Commands Practiced

### Current User

```bash
whoami
```

Output:

```text
root
```

Displays the current user inside the container.

---

### Current Directory

```bash
pwd
```

Output:

```text
/
```

Shows the current working directory.

---

### List Files

```bash
ls
```

Example:

```text
bin
boot
dev
etc
usr
var
```

Displays files and directories inside the container.

---

# 4. kubectl delete

## Command

```bash
kubectl delete pod nginx-pod
```

## Purpose

Deletes the specified Pod from the Kubernetes cluster.

---

## Verification

```bash
kubectl get pods
```

Expected Output:

```text
No resources found in default namespace.
```

---

# apply vs delete

## Apply

```bash
kubectl apply -f pod.yaml
```

Creates a resource if it does not exist.

Updates the resource if it already exists.

Uses a YAML file as input.

---

## Delete

```bash
kubectl delete pod nginx-pod
```

Deletes an existing Pod from the cluster.

---

# Pod Troubleshooting Flow

```text
Application Not Working
        │
        ▼
kubectl get pods
        │
        ├── Pod Not Running
        │        │
        │        ▼
        │   kubectl describe pod
        │
        └── Pod Running
                 │
                 ▼
           kubectl logs
                 │
                 ▼
      Check Application Errors
                 │
                 ▼
kubectl exec
                 │
                 ▼
Inspect Files & Configuration
```

---

# Interview Questions

### What is `kubectl describe`?

Displays detailed information about a Kubernetes resource, including configuration, status, events, and container details.

---

### What is `kubectl logs`?

Displays the stdout and stderr output generated by the application running inside the container.

---

### What is `kubectl exec`?

Executes commands inside a running container. Commonly used for debugging and troubleshooting.

---

### Why do we use `kubectl logs` if the Pod is already Running?

A Pod can be in the Running state while the application inside it is failing. Logs help identify application-level issues.

---

### What is the difference between `kubectl get` and `kubectl describe`?

`kubectl get` provides a summary of resources, while `kubectl describe` provides detailed information including events, node details, IP, and container configuration.

---

### What is the difference between `kubectl apply` and `kubectl delete`?

* `kubectl apply` creates or updates a resource from a YAML file.
* `kubectl delete` removes an existing resource from the Kubernetes cluster.

---

# Commands Practiced

```bash
kubectl describe pod nginx-pod

kubectl logs nginx-pod

kubectl exec -it nginx-pod -- /bin/bash

whoami

pwd

ls

kubectl delete pod nginx-pod

kubectl get pods
```






---

# Key Takeaways

* Kubernetes uses YAML files to define resources.
* YAML follows the declarative approach.
* Every Pod YAML contains `apiVersion`, `kind`, `metadata`, and `spec`.
* A Pod contains one or more containers.
* `kubectl apply` creates or updates resources.
* `kubectl get pods` verifies the Pod status and health.
* Small YAML mistakes (spelling, capitalization, spacing) can prevent Kubernetes from creating resources.
* `kubectl describe` is used to inspect Pod details and Events.
* `kubectl logs` displays application logs from the container.
* `kubectl exec` allows you to enter a running container for debugging.
* Linux commands like `whoami`, `pwd`, and `ls` can be executed inside the container.
* `kubectl delete` removes a Pod from the cluster.
* A systematic troubleshooting approach is:

  1. Check Pod status (`kubectl get pods`)
  2. Inspect Pod details (`kubectl describe`)
  3. Review application logs (`kubectl logs`)
  4. Enter the container if deeper investigation is needed (`kubectl exec`)
