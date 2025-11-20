# Kubernetes cluster on Amazon EKS 

Provision the cluster using *eksctl*, validate nodes, and create  K8's object manifest files &  test deploy on EKS.
## Create EKS Cluster

setup kubernetes cluster via eksctl command line 
```
kubectl version --client
eksctl version

Cluster Creation:
eksctl create cluster \
--name mindtrack \
--region ap-south-1 \
--nodes 2 \
--nodegroup-name linux-ubuntu 
--node-type t3.medium \
--managed
```
![ekscreation](https://github.com/anitodevops/Project-3/blob/main/Images/EKS%20Cluster%20Creation.png)

![mindtrackcluster](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack%20EKS%20Cluster.png)

Cluster Info:

`kubectl cluster-info`

![clusterinfo](https://github.com/anitodevops/Project-3/blob/main/Images/EKS%20Cluster%20in%20AWS%20Console.png)

Node info:

`kubectl get nodes`

![nodeinfo](https://github.com/anitodevops/Project-3/blob/main/Images/Cluster%20Nodes%20.png)

*Note: Update EKS nodegroup Security Group inbound Rule:
Add Rule:
Custom TCP , Port 3000 , Source : SG of ALB*

## Create Manifest Files 

### Deployment.yaml 

Add Strategy : type : Rolling Update to  update pods when a new deployment is made.

[deployment.yaml](https://github.com/anitodevops/Project-3/blob/main/deployment.yaml)

Create deployment:
`kubectl apply -f deployment.yaml`

`kubectl get pods` -> successful deployment shows pods in running state.

### Service.yaml

Choose spec: type: LoadBalancer to access the application  externally

[service.yaml](https://github.com/anitodevops/Project-3/blob/main/service.yaml)

Create Service:
`kubectl apply -f service.yaml`

`kubectl get svc` -> successful creation shows LB  in External IP ,  running on port 80.

![deploysvc](https://github.com/anitodevops/Project-3/blob/main/Images/K8s%20Manifest%20-%20Deploy%20&%20Svc%20.png)


![deploy](https://github.com/anitodevops/Project-3/blob/main/Images/K8s%20deployment%20check.png)

verify LB url :[http://a70ed0f644c19475a858f88b992f2be2-1981579793.ap-south-1.elb.amazonaws.com/]

*Note:by default LB listen to **Port 80.***

![LB](https://github.com/anitodevops/Project-3/blob/main/Images/LB%20creation%20&%20Node%20Health.png)

