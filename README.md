# DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/80ac680d-b476-42ac-bc47-47afd2285326)

In the Architecture diagram shown above a basic architecture of three-tier application is shown. In this diagram the first layer or tier is Presentation Layer or web tier. The second layer or tier is Application Layer or Business Tier and third layer or tier is Database Layer or Database tier. For web tier Nginx Service, for Application tier Tomcat and for Database tier MySQL and Memcache(for cache purpose) has been used as shown in the Architecture diagram above.
<br><br/>
The three tier Application is implemented using EKS as shown in the diagram below. It's Architecture diagram is same as explained above but instead of Nginx Sever, Elastic LoadBalancer has been used.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/c59bcbc2-407c-4a30-a7b2-cbfac3108330)

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
<br><br/>
```
Run below command on Node-1 to set the policy for High Availability (HA) in RabbitMQ Cluster.
rabbitmqctl set_policy ha-all ".*" '{"ha-mode":"all","ha-sync-mode":"automatic"}'
```
<br><br/>
Finally copy the DNS Name of the Application LoadBalancer of RabbitMQ and create the Record Set in hosted zone of Route 53. Access the URL and you will see the default console for RabbitMQ, you can use the initial username and password as guest and login into the RabbitMQ console.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/135af4ac-9be6-42de-a735-141214254eed)

On Jenkins Slave node create a file using the file present in Repository https://github.com/kamalmohan217/Three-tier-WebApplication.git, at the path Three-tier-WebApplication/src/main/resources/db_backup.sql with the name db.sql and create a database with the name accounts then import it as shown in the screenshot below.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/32fab099-a852-4de7-9d28-7d9cef6c3df7)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/49f487eb-f0c7-4b77-bc1c-e0f2bc6d09ce)
<br><br/>
Configure the Jenkins Slave Node as shown in the screenshot below.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/3c85546b-fe45-4b0e-91a9-24177bb595fc)
Install the SonarQube Scanner, Nexus Artifact Uploader and Pipeline Utility Step as shown in the screenshot below.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/64eaf5f6-55ff-4d2b-92fe-eac6f92c3799)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/be7f137f-13ab-482e-9490-d7d52b3cede8)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/ba9fff9f-19e6-4550-95c4-4b5bc5803f0a)
<br><br/>
To install nginx ingress controller and ArgoCD follow the below procedure
```
kubectl create ns ingress-nginx
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx

After creating it you need to edit the service and provide ssl certificate details and etc. in annotations as written below:- 
=================================================================
service.beta.kubernetes.io/aws-load-balancer-backend-protocol: http
service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout: "60"
service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled: "true"
service.beta.kubernetes.io/aws-load-balancer-ssl-cert: arn:aws:acm:us-east-2:XXXXXXXX:certificate/XXXXXX-XXXXXXX-XXXXXXX-XXXXXXXX
service.beta.kubernetes.io/aws-load-balancer-ssl-ports: https
service.beta.kubernetes.io/aws-load-balancer-type: elb

===================================================================
You need to change the targetPort for https to http in nginx ingress controller service as written below:-
-------------------------------------------------------------------------------------------------------------------------------
Before:

  ports:
    - name: http
      port: 80
      protocol: TCP
      targetPort: http
    - name: https
      port: 443
      protocol: TCP
      targetPort: https
After:

  ports:
    - name: http
      port: 80
      protocol: TCP
      targetPort: http
    - name: https
      port: 443
      protocol: TCP
      targetPort: http
=================================================================

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

Use the argocd-ingress-rule.yaml file as provided with Repository and create the URL, do the entry for this URL with DNS Name in Record Set of hosted zone of Route53. 

You can get the password of ArgoCD using the command written below-
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d

Now login into ArgoCD using the username admin and password as obtained above. After Login into ArgoCD change the password.

Finally Install ArgoCD cli on your Jenkins Slave.
```
<br><br/>
Create the Jenkins Job using the Jenkinsfile as provided in this Repository and update the file **application.properties** present at the path Three-tier-WebApplication/src/main/resources as shown in the screenshot below.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/762ce0c4-90e1-4e36-abe6-a6ce43f8e746)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/942478ff-11cb-4839-b692-97c89a829f5b)

Now Run the Jenkins Job after providing the parameters. Create the URL using ingress rule for service present in the file ingress-rule.yaml in this repository. Do the entry for this URL with DNS Name in Record Set of Route53. Access the newly created URL and provide username **admin_vp** and password **admin_vp**.   
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/312ba870-9e0a-4983-b55f-e43cdbb458a3)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/d45f64d1-4695-4673-9d3e-1a95db5377a4)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/fe73f4ea-701b-4b9a-833f-59769fbb67fc)
When you click on the User for the first time it will get the values from MySQL Database and store it in Memcache, so that next time when you click on the same user it will provide the values from the Memcache itself.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/894749ee-2144-4d02-856c-724a01dae13f)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/4286d2b9-ec86-4ca8-88f8-291648c068b1)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/56cc5fae-9843-4fe0-83f5-2d649ed24596)
<br><br/>
After running the Jenkins Job the Screenshot for RabbitMQ, SonarQube, Nexus Artifactory and ArgoCD is as shown in the Screenshot below.
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/d5cd5d3b-a84c-4aac-9f57-a5bfdc2ca327)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/30062e21-50b0-4526-929a-89bab7b8f1c7)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/e880ac0b-b379-413e-b892-76edcf6186cd)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/63694700-7400-4bcd-aa87-5c3739e5e4e9)
![image](https://github.com/kamalmohan217/DevOps-Project-3tier-Application-Deployment-eks-RabbitMQ-Memcache-MySQL/assets/128888356/3059bb8e-736e-465f-87aa-b20ed4a6d327)

<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
Source Code:-  https://github.com/kamalmohan217/Three-tier-WebApplication.git
```
<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
Reference:-  https://github.com/logicopslab/vprofile-project.git
```
