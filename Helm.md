#Helm
Templating engine for manifest files
Why?
similar workloads on various infrastructure. 
Managing files specific to envs is huge
cant change all manifest files everytime wth respect to envs if application is huge
something can always go wrong human error

What?
Reusable templates accross Envs.templatise
helm templates -> helm charts
is not a single file, is a directory with multiple files
records the configuration
renders the config env specific and provide deployable yml file

How to use 
Portal: https://helm.sh/
Install: https://helm.sh/docs/intro/install/
eg: debian
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm

Prequesite
Valid kubernates cluster
install kubectl
kubectl to communicate with eks cluster

Which version to use 3 or 2
VERSION 2: nov 2016-no external or RBAC install Tiller utility in cluster 
helm ->tiller->kubernatescontrller->worker nodes.
Problem: Tiller had God access ie root access. if managed to pass instruction to tiller -> ddos attack or cluster delete

VERSION 3 - SAFE to USE nov 2019
RBAC in Kubernates was itroduced. Only required access
Removed Tiller. communication via kubectl (safe and proactive)

default - latest version is installed

How it works
helm open source tool - maninated by CNCF
helm charts are cetrally hosted in artifact hub : Artifacthub.io(Recommened place)
  Official: CNCF
  Verified: third part / individual verified
  CNCF: Linux

Hosted in many places(bitnami server, github) but listed in Artifacthub.io not like dockerhub

1. helm repo add <name> <link>
   helm repo list
   helm repo remove

2.helm pull (if we want to modify)/ helm install (pulls and deploys) <releasename> <chartname> --version <version number> 
any modifications it updates the revision of deployment

--set variablename=value
helm pull --untar <helmchart> unzips
DIRECTORY STRUCTUR
1. Templates: all manifest files
2. Charts: All dependencoes
3. chart.yml details of chart
4. values.yml config values evs 

rollback 
Creates new version of deloyed version
and also we need to use pv pvc

Owncharts-our project-needs dir structure
Manually or helm to create structure
1.helm create <chartname>
2.remove from template dir if to cerate from scratch
3.templates now contains deployment and service.

Charts are two types:
application -> application gets deployed
library -> supporting lib if they want to use eg:Python

Variables to be used - jinja templates(template directives)
{{ .Release.Name }} - refer to release name in chart install 

DEFAULT OBJECT
Release - Name, Namespace, isUpgrade, isInstall, Revision, Service (release)
Chart -  Name, ApiVersion, Version, Type, Keywords, Home (charts.yml)
Capabilities - KubeVersion, ApiVersion, HelmVersion, GitCommit, GitTreeState, GoVersion (kubernates cluster)

All above are sentence Case
Values - our config values user defined (values.yml) - Any Case

BESTPRACTICE: update chart version and app versiob for our history
after change in file give helm upgrade releasename chartname (update release names too )





