# Blue_Green_Deployment

# Infrastructure:
- Provider + cred 
- 
# Java , MySql , EKS ,Terraform
# Zero DownTime + rollback easy
# K8:
- Mysql.pod -> serviec(svc) type of Cluster IP
- App.pod -> svc type of Load Balancer
- user -> LB -> app.pod -> cluster ip -> mysql
- update happen when we create new enviroment and direct traffic to it 

# setting up EKS cluster 

# jenkins to install:
- docker 

[ec2-user@ip-11-0-1-28 ~]$ aws eks --region eu-west-1 update-kubeconfig --name main_cluster
Added new context arn:aws:eks:eu-west-1:222634379970:cluster/main_cluster to /home/ec2-user/.kube/config
[ec2-user@ip-11-0-1-28 ~]$ kubectl get nodes
NAME                                       STATUS   ROLES    AGE   VERSION
ip-11-0-1-67.eu-west-1.compute.internal    Ready    <none>   10m   v1.31.5-eks-5d632ec
ip-11-0-2-100.eu-west-1.compute.internal   Ready    <none>   10m   v1.31.5-eks-5d632ec
ip-11-0-2-229.eu-west-1.compute.internal   Ready    <none>   10m   v1.31.5-eks-5d632ec
[ec2-user@ip-11-0-1-28 ~]$

- create token: 