# Concepts
**Namespace** 

***example*** 2 people having same name - differentiate with surname.\
call internally - by name , cross call - by name and surname

***3 namespace on creation of cluster*** \
kubesystem: System related resources \
default : User initiated resources - current context is set to default \
kubepublic:

we can create separate namespace for environments . dev, qa, uat if same cluster is handled for lower envs

***Create namespace*** \
imperative: kubectl create namespace dev
declarative : YAML file
Resource limiting or quota
spec:
  hard:
    pod: "10"
    request.cpu: "4"
    request.memory: "5Gi" (sigle resource)
    limits.cpu: "10"
    limits.memory: "10Gi" (overallnamesoace)

1.kubectl get pods ***--namespace=kube-system***
2.***Set context*** : kubectl config set-context $(kubectl config current-context) --namespace=dev
3.Allnamespaces : kubectl get pods --all-namespaces

namespace field under metadata \
preference is to cli.


**Overwrite  DockerFile**

CMD ["python", "app.py"] \
in yaml, spec containers give args:["app1.py"] replaces in docker image
Command : ["npm"]

**Env Variables** \
Env variavle to be passed to image \
3 ways to pass from outside: \

1.env: \
  - name: \
    value: 

2.ConfigMap \
  Storing env into object. Use same object across all pods \
  imoerative: kubectl create configmap my-config \
              --from-literal=POSTGRESS_PASSWORD=postgress_password --from-literal=POSTGRESS_PASS=posgress_pass \
              --from-file=test.properties / to directory with properties file \
  declarative: \
            data: \
              postgress_user: postgress \
              postgress_pass: postgress_pass \

  Call configmap in objects yml \
  envFrom in yaml \
    - configMapRef: \
        name: myconfig1 \
        name: myconfig2 \
        or \
    - configMapRef: \
        selector: \
          - matchLabels \
but Best practice is to have single config file.and also it creates only namespace specific

3.Secretfile - for sensitive information

kubectl create secret generic my-secret --from-literal=user=test --from-literal=password=password
kubectl create secret generic my-secret --from-file=secret.properties [BEST PRACTOICE TO STORE NAME AS .PROPERTIES FOR OUR READABLE PURPOSE]

data:
  user: test / encryted string to be passed
  password: pwd / encrypted string to be passed

Secrets to be in encrypted way, Kubernates will not encrypt it. - base64 encrypted string to be used.
echo -n "test" | base64

envFrom:
  - secretRef:
    name: mysecret

default decryptuin fron k8 is base64


**Persitent Volume**
Pods are volatile. so store it outside . common data storage getting attsached to nodes where pods gets scheduled.

spec:
  accessModes:
    ReadOnlyMany 
    ReadWriteOnce(many containers-> request queued)
    ReadWriteMany (consistency can be tampered)
  capacity:
    stoorage: 10Gi
  awsElasticBlockStore: (example only -> can use any)
    volumeID: (ebs volume id)
    fsType: ext4

  PVC-> claim at once for all (how much i want to claim from PV)
  resources:
    requests:
      storage: 500Mi

volumeMounts: (under containers section)
  - mountPath: (path on pod)
    name: (volume name)
volumes:
  -name: (volume name)
    persitentVolumeClaim:
      claimname: (pvc name)

  
    









