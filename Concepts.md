# Concepts
**Namespace** 

***example*** 2 people having same name - differentiate with surname.\
call internally - by name , cross call - by name and surname

***3 namespace on creation of cluster*** \
kubesystem: System related resources \
default : User initiated resources - current context is set to default
kubepublic: 

we can create separate namespace for environments . dev, qa, uat if same cluster is handled for lower envs

***Create namespace***
imperative: kubectl create namespace dev
declarative : YAML file

1.kubectl get pods ***--namespace=kube-system***
2.***Set context*** : kubectl config set-context $(kubectl config current-context) --namespace=dev
3.Allnamespaces : kubectl get pods --all-namespaces

