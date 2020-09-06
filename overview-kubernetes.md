# Kubernetes
---

## Concepts

### Pods
A Pod is a collection of one or more containers. Containers in a Pod share context, such as storage. They model a single application, or a group of tightly coupled applications. If a Pod dies, the node can generally replace it.  

About Pods: https://kubernetes.io/docs/concepts/workloads/pods/

### Deployments
A Deployment describes the desired state of your Pods. You describe how a pod is structured (what containers/images it has), how many pods you want, among other things. When you apply a Deployment, Kubernetes will create ReplicaSets to manage distribution of Pods. 
About Deployments:  
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/  

To see active Deployments:
``kubectl get deployments``

To apply a deployment from a YAML file:
``kubectl apply -f <YAML file>``


- #### ReplicaSets
    - ReplicaSets manage a group of identical Pods across multiple nodes, acting as a sort of multi-node, process manager, but for Pods. A ReplicaSet makes sure that a specific number of the same type of Pod are running at the same time by creating and deleting pods. Though it is possible to manually define a ReplicaSet, it is suggested to work with Deployments instead.
About ReplicaSets: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/

### Nodes
A Node is represents a single physical or virtual machine. A node may run multiple pods, but most commonly runs a single pod.  

To view the nodes on a cluster:
``kubectl get nodes``  
About Nodes: https://kubernetes.io/docs/concepts/architecture/nodes/


## Example deployment YAML:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
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
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
Explanation: This creates a deployment named ``nginx-deployment``. It **spec**ifies that the deployment should maintain 3 **replicas** of pods. The pods this applies to are those that are **select**ed to **match** the **label** ``app: nginx``. The **template** defines a Pod labeled with ``app: nginx``, **spec**ified to run the **container** named ``nginx`` from the image ``nginx:1.14.2``. The **containerPort** field indicates that the container listens on ``80``.


## Overview
- [x] Orchestration
  - The Idea of monitering, managing, and otherwise coordinating Computer Systems(like containors, for instance). There exists a few services which do this and Kubernetes focuses on Container Orchestration (and, fortunately, works well with Docker) and focuses on the deployment, scaling, and general management of software applications.
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
- [ ] Amazon ECS & EKSKv
- [ ] MiniKube: setting up a single-node cluster


## Resources
- [Educational k8s Comic](https://cloud.google.com/kubernetes-engine/kubernetes-comic/)
- A Rather comprehensive, 55 min long, Youtube video called [Introduction to Microservices, Docker, and Kubernetes](https://www.youtube.com/watch?v=1xo-0gCVhTU)
  - They start talking about Docker [here](https://youtu.be/1xo-0gCVhTU?t=398)
  - They start talking about Kubernetes [here](https://youtu.be/1xo-0gCVhTU?t=710)
  - They start their demonstaration in VS Code [here](https://youtu.be/1xo-0gCVhTU?t=1130)
- [Wikipedia](https://en.wikipedia.org/wiki/Kubernetes)
- A [K8s + Devops](https://rancher.com/blog/2020/create-kubernetes-devops-pipeline) blog postKv
