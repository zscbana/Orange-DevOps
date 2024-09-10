1-Create a ReplicaSet using the below yaml

omarelbanna@Omars-MacBook-Air Lab02 % kubectl apply -f task1.yaml 
replicaset.apps/new-replica-set created
omarelbanna@Omars-MacBook-Air Lab02 % kubectl get replicaset

NAME              DESIRED   CURRENT   READY   AGE
new-replica-set   4         4         0       32s
omarelbanna@Omars-MacBook-Air Lab02 % kubectl get pods -l name=busybox-pod

NAME                    READY   STATUS             RESTARTS   AGE
new-replica-set-8znxv   0/1     ErrImagePull       0          49s
new-replica-set-nh5nq   0/1     ImagePullBackOff   0          49s
new-replica-set-p6nt9   0/1     ImagePullBackOff   0          49s
new-replica-set-x4whc   0/1     ErrImagePull       0          49s

-------------------------------------------------------------------------
2-How many PODs are DESIRED in the new-replica-set?

omarelbanna@Omars-MacBook-Air Lab02 % kubectl get replicaset new-replica-set

Desired = 4 
NAME              DESIRED   CURRENT   READY   AGE
new-replica-set   4         4         0       3m6s

-------------------------------------------------------------------------
3-What is the image used to create the pods in the new-replica-set?

omarelbanna@Omars-MacBook-Air Lab02 % kubectl describe replicaset new-replica-set

    Image:      busybox777

-------------------------------------------------------------------------
4-How many PODs are READY in the new-replica-set?

omarelbanna@Omars-MacBook-Air Lab02 % kubectl get replicaset new-replica-set

READY = 0 

NAME              DESIRED   CURRENT   READY   AGE
new-replica-set   4         4         0       3m6s

-------------------------------------------------------------------------

5-Why do you think the PODs are not ready?
wrong image name 

omarelbanna@Omars-MacBook-Air Lab02 % kubectl describe pod new-replica-set-p6nt9       
  Warning  Failed     8m16s (x6 over 10m)  kubelet            Error: ImagePullBackOff

-------------------------------------------------------------------------
6-Delete any one of the 4 PODs. How many pods now

omarelbanna@Omars-MacBook-Air Lab02 % kubectl delete pod  new-replica-set-p6nt9
pod "new-replica-set-p6nt9" deleted

omarelbanna@Omars-MacBook-Air Lab02 % kubectl get replicaset new-replica-set     

NAME              DESIRED   CURRENT   READY   AGE
new-replica-set   4         4         0       13m

Still 4 
-------------------------------------------------------------------------
7-Why are there still 4 PODs, even after you deleted one?

The replicaset is still in the process of creating a new pod to replace the one that was deleted

-------------------------------------------------------------------------
8-Create a ReplicaSet using the below yaml

apiVersion is v1 change it to apps/v1 

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-1
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx

Kubernetes organizes its resources into several API groups to manage different kinds of objects and their evolution over time.
The v1 API group generally includes basic resources like Pods, Services, and Namespaces.
The apps API group is specifically used for more complex workload resources, including Deployments, ReplicaSets, StatefulSets, and DaemonSets.
