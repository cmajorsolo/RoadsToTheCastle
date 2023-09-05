# Kubernetes

## Components
1. API server - backend of the UI
2. ETCD: distributed key-value store for storing the data used to manage the cluster. It has all the master and nodes information in a multi-master, multi-node cluster. It makes sure there is no conflicts between the masters 
3. Scheduler: Assign nodes to newly created containers 
4. Controller: Monitors nodes and containers. When a node or container gets down, it brings it up again. 
5. Container runtime: service that used to run containers - docker 
Kubelet: Agent runs on each node. It makes sure that containers are running on the node. 

## Master vs Worker 
- Master node: 
    - kube-apiserver 
    - etcd, controller, scheduler
- Worker node: 
    - Kubelet
    - Container runtime - docker, rkt, or cri-o

## Concepts
- Pod: 
    - normally contains one of a kind container but multiple containers can live on same pod. The other container normally a help container. 
- Replication controller: 
    - Load balancing & scaling over nodes
- Replica set: newer version of Replication controller 
- Services: group of pods
    - NodePort
        - Node:30008 -> Service:80 <- Pod:80
        - load balancing is automatically done
    - ClusterIP
        - Problem statement: when having a system that has a group of front-end pods and back-end pods, how would frontend pods know which backend pod to talk to? Kubernetes provide a layer that groups backend pods together and provides information to frontend pods. Either frontend or backend service gets an ip and name assign to it. Inside the cluster, the name is used by other pods to acces the service. 
    - LoadBalancer

   

