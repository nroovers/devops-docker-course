# Exercise 3.7 - Kubernetes

## Docker 
Docker, the topic of this course, is a platform for “virtualising” application environments through containers. These containers host applications and all relevant dependencies. Containers ease the way applications are build and deployed among different environments as they ensure that applications are consistently deployed through containers. 
Docker provides a container runtime environment for a single machine. For example, all course material and exercises were on 1 machine.

## Why Kubernetes
In an enterprise environment however, applications are often deployed over various machines and this is why a solution is required to properly manage distributed containers.
This is where Kubernetes comes into place. **Kubernetes** automates the scaling, managing, updating and removing containers across different nodes, or in short, **container orchestration**. 

## What is Kubernetes
A Kubernetes setup consists of a collection of nodes, i.e. a Kubernetes cluster. A node is a server or virtual machine that hosts a container runtime, such as Docker. Kubernetes is not bound to Docker specifically, but allows to host various container technologies. A cluster consists of a Mater node and multiple worker nodes. The master node manages the other worker nodes.

Master node consists of:
-	**API Server**: provides API to manage and control a cluster
-	**Controller manager**: controller to automate the management of nodes and their state
-	**Scheduler**: schedules the assignment of pods to nodes based on resource availability

Worker node consists of:
-	**Kubelet**: an agent that provides information about the node to the master and ensures that the pods are running as instructed by the master node
-	**Proxy**: implements network rules that allow different parts of applications to communicate with each other across nodes and beyond (outside world)
-	**Pod**: a pod is a unit of deployment which can host 1 or more (related) containers
