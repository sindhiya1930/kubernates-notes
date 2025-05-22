**IAM Roles to be created**
***1. Roles: EKS***
   
   EKS:Cluster
   
   Policy:
   
     AmazonEKSClusterPolicy
   
***3. Roles: EC2***
   
   Policy:
   
     AmazonEKS_CNI_Policy
   
     AmazonEKSWorkerNodePolicy
   
     AmazonEc2ContainerRegistryReadOnlyPOlicy

**EKS Service-Create Cluster**

1.Custom Configuration (No Auto mode)

2.Clustername

3.Choose the two roles

4.Kubernates version

5.Cluster Access: EKS API

6.Subnet 

  Note: N.virginia subnet1e should be deselected . it doesnt have kubernates support
  
6.Security group


**K8 Architechture flow**

***Creation or scheduling pod***

User ->(Commands)->Apiserver->Schedular->etcd(to get clusterinfo)->Schedular(based on policies we set)->ApiServer->kubelet->container runtime->api Server ->Schedular->etcd(updated the information).

**Automode vs custom**
Automode - Serverless (no need to worry about upgrade of K8s with no downtime ,Costlier)
Custom - infra ( We initiate with downtime)

**Nodes add**
1.nodegroup - Adding EC2 (patching we need to do)

AMI type
capacity OnDemand
instance type t3.medium(atleast one gb ram and 2 cores)
scaling - (2-8)

2.Fargate - serverless (its taken care of)

Setup kubectl -> kubernates.io
env variable -> path to exe file(windows)

local->eks
security cred -> access key(cli) (safe)

aws cli install
aws configure -> add access secret json region
aws eks update-kubeconfig --name <name of cluster>
kubectl cluster-info




   
   
