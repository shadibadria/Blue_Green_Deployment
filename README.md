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


[ec2-user@ip-11-0-1-28 ~]$ kubectl get all -n webapps
NAME                                READY   STATUS    RESTARTS        AGE
pod/bankapp-blue-6c75c748cd-659fj   1/1     Running   1 (5m55s ago)   6m20s
pod/mysql-77b9d5d45-6pjgt           1/1     Running   0               6m22s

NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP                                                               PORT(S)        AGE
service/bankapp-service   LoadBalancer   10.100.43.194    a6596ff6951f64952bbbca9818947bce-2053185439.eu-west-1.elb.amazonaws.com   80:31635/TCP   6m21s
service/mysql-service     ClusterIP      10.100.192.212   <none>                                                                    3306/TCP       6m22s

NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/bankapp-blue   1/1     1            1           6m20s
deployment.apps/mysql          1/1     1            1           6m22s

NAME                                      DESIRED   CURRENT   READY   AGE
replicaset.apps/bankapp-blue-6c75c748cd   1         1         1       6m20s
replicaset.apps/mysql-77b9d5d45           1         1         1       6m22s
[ec2-user@ip-11-0-1-28 ~]$ kubectl get all -n webapps
NAME                                 READY   STATUS    RESTARTS       AGE
pod/bankapp-blue-6c75c748cd-659fj    1/1     Running   1 (8m4s ago)   8m29s
pod/bankapp-green-646bc4d8d8-d2q6z   1/1     Running   0              13s
pod/mysql-77b9d5d45-6pjgt            1/1     Running   0              8m31s

NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP                                                               PORT(S)        AGE
service/bankapp-service   LoadBalancer   10.100.43.194    a6596ff6951f64952bbbca9818947bce-2053185439.eu-west-1.elb.amazonaws.com   80:31635/TCP   8m30s
service/mysql-service     ClusterIP      10.100.192.212   <none>                                                                    3306/TCP       8m31s

NAME                            READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/bankapp-blue    1/1     1            1           8m29s
deployment.apps/bankapp-green   1/1     1            1           13s
deployment.apps/mysql           1/1     1            1           8m31s

NAME                                       DESIRED   CURRENT   READY   AGE
replicaset.apps/bankapp-blue-6c75c748cd    1         1         1       8m29s
replicaset.apps/bankapp-green-646bc4d8d8   1         1         1       13s
replicaset.apps/mysql-77b9d5d45            1         1         1       8m31s
[ec2-user@ip-11-0-1-28 ~]$

