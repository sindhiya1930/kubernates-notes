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
HPA (replicas of pod auto)



