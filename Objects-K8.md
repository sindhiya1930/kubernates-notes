1.Pod

Containes one or more containers, group dependent container in pod

2.Replicaset (2019, Replication controller deprecated)

Users increasing -> multiple replicas of pod -> k8 makes sure it is up and running

3.Deployment

Deployment history and roll back -> creates replica set with pods -> another deployent another repicaset. Empty the v1 deploment.-> Deployment statergies

Recreate :delete v1 , create new v2 (may cause downtime)

Rolling update : delete one pod from v1, create new pod in v2. similarly for pod 2. Before deleting last pod traffic is routed to v2 and then process is followed (Default Stratergy)

inmem version of manifest file and tag to deployment.
if replicas not specified -> default 1

4.Service

comm between pods

clusterIp -> internally cluster comm, 
nodeport -> traffic from outside of cluster to single desired pod/deployment
loadbalancer -> traffic from outside of cluster to multiple desired pod/deployment or replicaset
if service type not specified -> default loadbalancer

MANIFEST
1.apiVersion (api call version of object)
2.kind (type of object)
3.metadata (info about pod-> name, label)
4.spec : info on pod (what should that object contain)

kubectl create -f <yml file> does not exist ->create does exist error
kubectl apply -f <yml file> does not exist ->create does exist update

kubectl describe deployment <deployment name> (contains logs of the stratergy followed)
kubectl edit deployment <deployment name>
kubectl rollout history deployment <deployment name>
kubectl rollout undo deployment <deploymet name>
kubectl rollout undo deployment <deployment name > --to-revision=<revision number>


kubectl dockerfile expose port -> yml container port -> service outside port to container port(target)
kubectl apply -f <directory name> (applies all yml files)
to expose -> eks security group add the ports

