# kubernates
# Kubernetes Learning Journey (45 Days)

## 📌 Overview

This repository documents my **45-day Kubernetes learning journey**, focused on gaining practical Kubernetes knowledge for enterprise applications, especially Oracle BRM deployments running on Kubernetes.

The goal is to build a strong understanding of Kubernetes concepts through hands-on practice, real-world examples, and daily exercises rather than only learning theory.

---

# 🎯 Objectives

- Understand Kubernetes architecture
- Learn Kubernetes core components
- Deploy and manage applications
- Troubleshoot Kubernetes workloads
- Learn Kubernetes from a BRM (Billing and Revenue Management) perspective
- Gain practical experience with kubectl commands
- Prepare for Kubernetes interview questions

---

# 📅 Learning Duration

**Total Duration:** 45 Days

**Daily Study Time**
- Weekdays: 1.5–2 Hours
- Weekends: 3–4 Hours

---

# 📚 Learning Roadmap

## Week 1 – Kubernetes Fundamentals

### Topics

- Introduction to Kubernetes
- Why Kubernetes?
- Docker vs Kubernetes
- Cluster Architecture
- Control Plane
- Worker Nodes
- Pods
- Namespaces
- Labels
- Selectors
- YAML Basics

### Hands-on

- Install Kubernetes locally
- Explore cluster information
- Create first Pod
- View Pod logs
- Describe Pods
- Delete and recreate Pods

---

## Week 2 – Application Deployment

### Topics

- Deployments
- ReplicaSets
- Scaling
- Rolling Updates
- Rollbacks
- Services
  - ClusterIP
  - NodePort
  - LoadBalancer

### Hands-on

- Deploy Nginx
- Scale Deployments
- Expose Services
- Perform Rolling Updates

---

## Week 3 – Configuration & Storage

### Topics

- ConfigMaps
- Secrets
- Environment Variables
- Volumes
- Persistent Volumes
- Persistent Volume Claims
- Storage Classes

### Hands-on

- Create ConfigMaps
- Mount Volumes
- Manage Secrets

---

## Week 4 – Troubleshooting

### Topics

- Logs
- Pod Events
- kubectl exec
- Debugging
- Resource Limits
- Requests
- Liveness Probe
- Readiness Probe

### Common Issues

- CrashLoopBackOff
- ImagePullBackOff
- Pending Pods
- Failed Scheduling

---

## Week 5 – Advanced Kubernetes

### Topics

- Jobs
- CronJobs
- Multi-container Pods
- Networking Basics
- Ingress
- Resource Optimization

### Project

Deploy a complete multi-tier application.

---

## Week 6 – Kubernetes for Oracle BRM

### Topics

- BRM Deployment Architecture
- CM Pods
- DM Pods
- Pipeline Pods
- Configuration Management
- Log Analysis
- Restarting Services
- Customization Deployment
- Debugging BRM Applications

---

# 💻 Daily Practice Format

Every learning session follows the same approach:

1. Learn the concept
2. Understand the architecture
3. Perform hands-on practice
4. Complete a small exercise
5. Answer interview questions
6. Apply the concept to Oracle BRM

---

# 🛠 Practice Environment

Learning will be performed using:

- Kind
- Minikube
- Killercoda
- kubectl CLI

**Note:** Office Kubernetes environments will only be used for observation and troubleshooting. All practice exercises will be performed on local or sandbox environments.

---

# 📖 Topics Covered

- Kubernetes Architecture
- Nodes
- Pods
- ReplicaSets
- Deployments
- Services
- ConfigMaps
- Secrets
- Volumes
- Persistent Storage
- Namespaces
- Labels
- Selectors
- Rolling Updates
- Rollbacks
- Scaling
- Logging
- Monitoring
- Troubleshooting
- Jobs
- CronJobs
- Ingress
- Resource Management

---

# 🎯 End Goal

By the end of this learning journey, I aim to:

- Understand Kubernetes architecture
- Deploy applications confidently
- Troubleshoot production issues
- Work efficiently with Kubernetes-based Oracle BRM deployments
- Understand container orchestration
- Build confidence for Kubernetes-related interview discussions

---

# 📌 Learning Resources

## Documentation

- Kubernetes Official Documentation

## Video Courses

- TechWorld with Nana
- KodeKloud
- Google Cloud Tech

## Practice Platforms

- Killercoda
- Kind
- Minikube

---

# 📈 Progress Tracker

| Week | Status |
|--------|--------|
| Week 1 | ⬜ |
| Week 2 | ⬜ |
| Week 3 | ⬜ |
| Week 4 | ⬜ |
| Week 5 | ⬜ |
| Week 6 | ⬜ |

---

# 📝 Notes

This repository serves as my personal learning journal where I will continuously update:

- Notes
- Commands
- Practice exercises
- YAML files
- Hands-on projects
- Interview questions
- Oracle BRM Kubernetes use cases

---


```
kubernetes-learning/
│
├── README.md
├── notes/
│   ├── day01.md
│   ├── day02.md
│   ├── day03.md
│   └── ...
├── yaml/
│   ├── pod.yaml
│   ├── deployment.yaml
│   ├── service.yaml
│   └── configmap.yaml
├── projects/
│   ├── nginx/
│   ├── multi-tier-app/
│   └── brm-scenarios/
├── interview-questions/
│   ├── basic.md
│   ├── intermediate.md
│   └── advanced.md
└── troubleshooting/
    ├── crashloopbackoff.md
    ├── imagepullbackoff.md
    └── pod-debugging.md
```
---

## 🚀 Happy Learning!