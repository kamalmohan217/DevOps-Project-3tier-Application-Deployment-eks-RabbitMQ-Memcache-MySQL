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

To create RabbitMQ cluster of three nodes follow the below procedures.
```
On Node-1 (RabbitMQ-Server-1) open the file /var/lib/rabbitmq/.erlang.cookie using cat command and copy the hash value of cookie and paste it on Node-2 and Node-3 in the file /var/lib/rabbitmq/.erlang.cookie.
Then restart rabbitmq-server service, then stop rabbitmq application using the command rabbitmqctl stop_app on Node-2 (RabbitMQ-Server-2) and Node-3 (RabbitMQ-Server-3). Finally run the command rabbitmqctl join_cluster rabbit@<IP_Address_Node1> and start the rabbitmq application using the command rabbitmqctl start_app on Node-2 and Node-3.
```
**Node-1**
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/6df8640f-b82d-4d16-b74a-644c6173fc5c)
**Node-2**
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/b6be22a9-b8fe-4127-836e-54a7d5979b8c)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/459fce42-e870-4d24-9f18-12e7ddba63e6)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/910d01a4-c6a5-40f5-859b-8a43e8a05614)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/4a32fbda-7c84-4cb1-bc13-fd05e8238ce7)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/422fab16-480e-4d07-a2c3-8c6273a9c605)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/01e2e008-f456-4ca3-b78d-713ebabd8c51)
**Node-3**
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/8cd9f32f-c183-4bb4-b7a2-0237441b7796)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/1f1f1ce5-96d0-4ddf-bf37-6e46fbfdc708)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/c28a1eab-6d35-4eeb-bceb-67156b7e34a3)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/3f1c3963-821c-44b6-8e86-bbd0bb53268c)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/4241368e-6efe-4aaf-a615-0598d241d39d)

Finally copy the DNS Name of the Application LoadBalancer of RabbitMQ and create the Record Set in hosted zone of Route 53. Access the URL and you will see the default console for RabbitMQ, you can use the initial username and password as guest and login into the RabbitMQ console.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/135af4ac-9be6-42de-a735-141214254eed)

On Jenkins Slave node create a file using the file present in Repository https://github.com/singhritesh85/Three-tier-WebApplication.git, at the path Three-tier-WebApplication/src/main/resources/db_backup.sql with the name db.sql and create a database with the name accounts then import it as shown in the screenshot below.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/32fab099-a852-4de7-9d28-7d9cef6c3df7)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/49f487eb-f0c7-4b77-bc1c-e0f2bc6d09ce)



