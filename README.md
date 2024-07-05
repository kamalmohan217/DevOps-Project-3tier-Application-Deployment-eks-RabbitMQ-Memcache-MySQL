# DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/80ac680d-b476-42ac-bc47-47afd2285326)

In the Architecture diagram shown above a basic architecture of three-tier application is shown. In this diagram the first layer or tier is Presentation Layer or web tier. The second layer or tier is Application Layer or Business Tier and third layer or tier is Database Layer or Database tier. For web tier Nginx Service, for Application tier Tomcat and for Database tier MySQL and Memcache(for cache purpose) has been used as shown in the Architecture diagram above.
<br><br/>
The three tier Application is implemented using EKS as shown in the diagram below. It's Architecture diagram is same as explained above but instead of Nginx Sever, Elastic LoadBalancer has been used.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/2ad6c5c1-3816-4bd0-b07d-dce3b24c364c)

I have used terraform script as provided in this repository to create the EC2 Instances, ALBs, EKS, Memcached and RDS. 
<br><br/>
I have created RabbitMQ cluster with three instances. Follow below procedures to achieve the same.
```
Using the above terraform script and the bootstrap script used with terraform three EC2 Instances for RabbitMQ will be created along with the Application LoadBalancer.
The Bootstrapping script will install RabbitMQ on three EC2 Instances. Then list the plugins, enable rabbitmq_management plugin and restart the rabbitmq-server on the three EC2 Instances. To achieve this I have used below commands.
(a) rabbitmq-plugins list
(b) rabbitmq-plugins enable rabbitmq_management
(c) systemctl restart rabbitmq-server
Finally you can ensure that rabbitmq_management plugin is enabled or not using the command rabbitmq-plugins list
```
**First Node, Consider it as Node-1**
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/463f7852-aaec-4cdc-8c3f-970c729ebfd5)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/4e0fdeed-6420-4cd6-9ec3-6c3fe482287c)
**Second Node, Consider it as Node-2**
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/04c8ee6e-f8c1-4eaf-97f1-0389977827d8)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/6c5c3283-a98b-4b55-8cb6-262e1a454aba)
**Third Node, Consider it as Node-3**
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/a04bb81d-4d5b-43fc-8a74-a701b8a5ad4a)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/fe6d3034-9d21-459e-b9f5-bf63573b6126)



