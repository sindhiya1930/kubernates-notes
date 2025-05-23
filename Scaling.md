Scaling
1.vertical -> storage increase\
EC2
stop->Actions->change instance type (manual)
there is limit to memery increase

2.horizontal -> count
EC2
AutoScaling group(monitor all instances in that group)
1-60 2 40 : avg = 60+40/2 :50 percent
Scaling up policy : CPU >70 per add one machine (min-1 and max-10 to be set since clod spending will be enormous)
Scaling down policy : CPU  < 20 per delete one machine
scaled machine is vanilla flavour so we have launch configuration (all details of ec2)
traffic is only to one machibe -> if scaled up (loadbalancer)

cluseter Auto scaler (add more nodes) - Cloud comes with by default cluster autoscalar
HPA (replicas of pod auto) (only replivable objects)
aws -> cloudwatch has logs of cluster -> uses this for cluster autoscaling

sxaleTargetRef:
  apiVersion:
  Kind:
  name:
minReplicas: 1
maxReplicas: 10
targetCPUUtilizationPercentage: 50 (if >50 up, if <50 down)

How it will cometo know -> someone should watch 
Kubernates has a metric server 
Monitors health of cluster 
https://github.com/kubernetes-sigs/metrics-server -> kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/high-availability-1.21+.yaml
Deploy the YAML file where HPA and pods are created.
itd a Kubernates object -> deploys in namespace kube-system

loadbalancer distributes.
warming up is upto 5 mins. if threshold is constantly below 50 perc. it brings down slowly.(to avoid sudden spike)

one-one mapping of HPA

How?
1.hpa controll loop not conituous default to 15 seconds
edit -> in mem file 
automatically edits the inmemory manifest file. it updates the replicas.

vertical scalar-> limits and mem to be modified.(do not use , stateless workload-> we may loose inplace data in pod since it restarts)



