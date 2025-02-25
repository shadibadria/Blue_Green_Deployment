# Blue_Green_Deployment

# Java , MySql , EKS ,Terraform
# Zero DownTime + rollback easy
# K8:
- Mysql.pod -> serviec(svc) type of Cluster IP
- App.pod -> svc type of Load Balancer
- user -> LB -> app.pod -> cluster ip -> mysql
- update happen when we create new enviroment and direct traffic to it 

# setting up EKS cluster 
