# Kubernetes
---
##Concepts

### Pods
A Pod is a collection of one or more containers. Containers in a Pod share context, such as storage. They model a single application, or a group of tightly coupled applications. If a Pod dies, the node can generally replace it.

### Nodes
A Node is represents a single physical or virtual machine. A node may run multiple pods, but most commonly runs a single pod. 

To view the nodes on a cluster:
``kubectl get nodes``

## Overview
- [ ] Orchestration
- [ ] Kubernetes:
  - [ ] Architecture:
    - [ ] clusters
    - [ ] nodes
    - [ ] pods
    - [ ] services
    - [ ] volumes
  - [ ] Controllers:
    - [ ] Deployments
    - [ ] ReplicaSets
  - [ ] Objects:
    - [ ] names
    - [ ] namespaces
    - [ ] labels
    - [ ] selectors
  - [ ] YAML:
    - [ ] Configuration
    - [ ] deployment files
  - [ ] Load balancing
  - [ ] Master node control layer
  - [ ] kubectl
  - [ ] Kubernetes Dashboard
  - [ ] Security
  - [ ] Networking:
    - [ ] ingress/egress rules
  - [ ] Scheduling
  - [ ] Monitoring
- [ ] Amazon ECS & EKS
- [ ] MiniKube: setting up a single-node cluster


## Resources
- [Educational k8s Comic](https://cloud.google.com/kubernetes-engine/kubernetes-comic/)
