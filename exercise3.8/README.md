# Exercise 3.8 - Kubernetes deployment

## Introduction

For exercise 3.8, I chose the option to deploy an application to a Kubernetes cluster. The application that I deployed is the bloglist application (from the [Full Stack Open course](https://fullstackopen.com/en)) which consists of a frontend and a backend. A docker image has been created for each part and these are availabel on Docker Hub:

1. Backend: https://hub.docker.com/repository/docker/nroovers/bloglist-frontend

2. Frontend: https://hub.docker.com/repository/docker/nroovers/bloglist-backend

The application has been deployed to a Kubernetes cluster hosted on Azure: Azure Kubernetes Service.

## Setup

This section describes the steps that were taken to deploy the bloglist application to a Kubernetes cluster on Azure.


### Step 1: Preparation

In order to deploy an application to a kubernetes cluster, we need to create a kubernetes manifest file which describes the resources that will be deployed to the cluster. Such a Kubernetes manifest file can be converted from a docker compose file with the ```kompose``` tool (more info [here](https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes/)):

In the folder where the docker-compose file is stored, run the following command:
```
$ kompose convert
```

This created the relavant kubernetes manifest yaml files:

- [backend-deployment.yaml](/exercise3.8/backend-deployment.yaml)
- [backend-service.yaml](/exercise3.8/backend-service.yaml)
- [frontend-deployment.yaml](/exercise3.8/frontend-deployment.yaml)
- [frontend-service.yaml](/exercise3.8/frontend-service.yaml)



### Step 2: Azure & Kubernetes setup


Create an Azure resource group, named *ex38ResourceGroup*:
```
$ az group create --name ex38ResourceGroup --location westeurope
```

Create a Kubernetes cluster, named *ex38AKSCluster*, under the created resource group. The cluster has 2 nodes:
```
$ az aks create \
    --resource-group ex38ResourceGroup \
    --name ex38AKSCluster \
    --node-count 2
```

The cluster can be managed and configured with the ```kubectl``` command line interface. But first ```kubectl``` needs to connect to the cluster with following command:
```
$ az aks get-credentials --resource-group ex38ResourceGroup --name ex38AKSCluster
```

### Step 3: Application deployment


Deploy the bloglist application to the kubernetes cluster via the created kubernetes manifest files:
```
$ kubectl apply -f backend-deployment.yaml -f backend-service.yaml -f frontend-deployment.yaml -f frontend-service.yaml
```

In order to expose the frontend externally, create a Service object of type LoadBalancer which will expose the frontend deployment:
```
$ kubectl expose deployment frontend --type=LoadBalancer --name=frontend-loadbalancer
```
Now the bloglist application has been deployed to a kubernetes cluster and is externally accessible. 

### Step 4: Verification

The setup results in 4 services, including the frontent, backend and the load balancer (see following ```kubectl``` output). 

```
$ kubectl get services
NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
backend                 ClusterIP      10.0.108.110   <none>          3001/TCP       14h
frontend                ClusterIP      10.0.199.228   <none>          80/TCP         14h
frontend-loadbalancer   LoadBalancer   10.0.144.56    51.105.105.75   80:30961/TCP   14h
kubernetes              ClusterIP      10.0.0.1       <none>          443/TCP        14h
```

The load balancer exposes an external-IP address which makes the application available via [51.105.105.75 ](http://51.105.105.75).


We can also see that 2 pods have been created seperating the backend and frontend into 2 different containers: 

```
$ kubectl get pods -o wide
NAME                        READY   STATUS    RESTARTS   AGE   IP           NODE                                NOMINATED NODE   READINESS GATES
backend-dcd9ff6dc-s62v5     1/1     Running   0          14h   10.244.1.2   aks-nodepool1-14148720-vmss000000   <none>           <none>
frontend-79f77d47d5-mr7rj   1/1     Running   0          14h   10.244.1.3   aks-nodepool1-14148720-vmss000000   <none>           <none>
```


## More info

- DevOps with Docker course: https://devopswithdocker.com/
- Create a kubernetes cluster in Azure: https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app
