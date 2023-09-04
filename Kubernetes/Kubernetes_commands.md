# Kubernetes Commands
## Basic
`Kubectl run nginx --image nginx`:
- creates a pod with name nginx
- creates a container with nginx image inside the pod
- the image is downloaded from docker hub

`kubectl get pods` 
- show pods 

`kubectl get pods -o wide`

`kubectl describe pod nginx`

`minikube dashboard`
- show dashboard

## Creating pod with yaml
`kubectl create -f pod-definition.yml` or `kubectl apply -f pod-definition.yml` are both used for creating a new pod from the yml file 

pod-definition.yml
```yml
apiVersion: V1 # the api version of Kubernetes API you are using to create the project
kind: Pod # the type of the project you are creating
    # Options are: Service, ReplicaSet, Deployment
metadata: # only name and labels are allowed under metadata
    name: myapp-pod
    labels: # any name value pairs can be inserted here 
        app: myapp
        type: front-end
spec: # addtional information for Kub to pretaning the project
    containers:
        - name: nginx-container
          image: nginx 

```
## Updating pod that named 'redis'
`kubectl edit pod redis` or `kubectl apply -f redis-definition.yaml `

## Replication controller
`kubectl create -f rc-definition.yml` creates pods using spec-template in below yml file with replica=3

rc-definition.yml
```yml
apiVersion: V1 
kind: ReplicationController # the type of the project you are creating
    # Options are: Service, ReplicaSet, Deployment
metadata: 
    name: myapp-pod
    labels: 
        app: myapp
        type: front-end
spec: # defines what inside the project is created
    template: # definees a pod here for replication
        metadata: # Pod metadata copied from the pod-definition.yml
            name: myapp-pod
            labels: 
                app: myapp
                type: front-end
        spec: 
            containers:
                - name: nginx-container
                  image: nginx 
    replicas: 3
```
`kubectl get replicationcontroller` to view replications

## Replica Set - newer version of replication controller. suggested
`kubectl create -f replicaset-definition.yml` creates replica with replicaset-definition.yml file 

`kubectl get replicaset` to view replications

replicaset-definition.yml
```yml
apiVersion: apps/v1 # has to be apps/v1 instead of v1. Otherwise you will get unable to recognized replicaset-definition.yml error. 
kind: ReplicaSet
metadata: 
    name: myapp-pod
    labels: 
        app: myapp
        type: front-end
spec: # defines what inside the project is created
    template: # definees a pod here for replication
        metadata: # Pod metadata copied from the pod-definition.yml
            name: myapp-pod
            labels: 
                app: myapp
                type: front-end
        spec: 
            containers:
                - name: nginx-container
                  image: nginx 
    replicas: 3
    selector: # defines what pod for underwrite; required fields;
        matchLabels: 
            type: front-end
```
## Replica Set - how to scale
1. Update replicas number in `replicaset-definition.yml` file
2. Run `kubectl replace -f replicaset-definition.yml`

OR

1. Run `kubectl scale --replicas=6 -f replicaset-definition.yml`. The numbers in the file remains same 

OR
1. Run `kubectl edit replicaset myapp-replicaset` to edit the replica number. This command updates the file in Kub's memory. The original file is not updated. 
   
### commands
| Function | Commands |
|----------|----------|
| create replicaset  | `kubectl create -f replicaset-definition.yml`  |
| Get replicaset  | `kubectl get replicaset`  |
| Delete replicaset  | `kubectl delete replicaset myapp-replicaset`  |
| Replace replace replicaset with yml  | `kubectl replace -f replicaset-definition.yml`  |
| Scale replicaset  | `kubectl scale --replicas=6 -f replicaset-definition.yml`  |

## Deployment
Deployment is for:  
&nbsp;&nbsp;Rolling updates - replicas scale down one by one and scale up simutaneously one by one
&nbsp;&nbsp;Rollback - All replicas scales down to 0 and scale up again

### Update and rollback 



### commands
| Function | Commands |
|----------|----------|
| create deployment  | `kubectl create -f deployment.yaml`  |
| describe deployment  | `kubectl describe deployment myapp-deployment`  |
| get all info   | `kubectl get all`  |
| edit deployment | `kubectl eidt deployment myapp-deployment`  |
| get roll out status  | `kubectl rollout status deployment/myapp-deployment`  |
| get deployement history  | `kubectl rollout history deployment.apps/myapp-deployment`  |
| use `--record` to show caus of change in rollout history  | `kubectl create -f deployment.yaml --record`  |
| trigger a new rollout deployment with updates in yml  | `kubectl apply -f deployment-definition.yaml`  |
| trigger a new rollout deployment with updates command  | `kubectl set image deployment/myapp-deployment nginx-container=nginx:1.9.1`  |
| rollback  | `kubectl rollout undo deployment/myapp-deployment`  |

