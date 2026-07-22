# Kubernetes Day 2 Notes – YAML & Creating Your First Pod

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

---

# Key Takeaways

* Kubernetes uses YAML files to define resources.
* YAML follows the declarative approach.
* Every Pod YAML contains `apiVersion`, `kind`, `metadata`, and `spec`.
* A Pod contains one or more containers.
* `kubectl apply` creates or updates resources.
* `kubectl get pods` verifies the Pod status and health.
* Small YAML mistakes (spelling, capitalization, spacing) can prevent Kubernetes from creating resources.
