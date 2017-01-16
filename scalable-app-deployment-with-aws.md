# Deploy to AWS

Let's say we have a web application named `MyApp` and we want to deploy it to AWS in a scalable fashion. How do we do it?

![](/assets/aws_deployment_1.png)

As described in above diagram the deployment architecture of AWS consist of following components:

* MyApp VPC
  * All EC2 instances are placed inside MyApp VPC for security purposes. MyApp VPC consists of 4 subnets:
    * Private-1a (Private subnet in AZ- 1a)
    * Private-1b (Private subnet in AZ- 1b)
    * Public-1a  (Public subnet in AZ- 1a)
    * Public-1b (Public subnet in AZ- 1b)

Where,
Private Subnet = Outer services can not access instance directly. They do not have public IP. While Instances in Private subnet can access internet/outer services via NAT Internet Gateway.
Public Subnet = Outer Services can directly access instances directly through their public IP.

Database Layer
Currently there exists a single node of MongoDB instance which is Primary Node hosted in Private Subnet of VPC.
MongoDB  PrimaryNode is hosted in  AZ 	ap-southeast-1a
Instance Size : M3.medium (1 vCPU, 3.75GiB RAM, 60GiB EBS Volume attached)

TODO
For H.A there should be one more DB instance in another AZ i.e 1b which is replication of PrimaryNode. But this is kept as option for Initially.

MyApp NodeJS Application Layer

This Layer Exists in Private Subnets (1a, 1b) of VPC i.e they are not directly accessible like DB layer.
This is layer where MyApp is deployed via AWS EC2 Container Service.
The Single EC2  instance configuration in this layer is as below
Instance Size : T2.micro (1 vCPU, 1GiB RAM, 20GB EBS)
The instances are kept in AutoScaling Group where desired Instances are 2 and ECS Service desired Running tasks are 2.
Count is kept 2 deliberately for smooth deployment. 

LoadBalancer 

	LoadBalancer is hosted in Public Subnets  of VPC For High Availability.  80 & 443 ports of LB are mapped with 3000 Port of EC2 instances running MyApp.

CloudFront 
	CloudFront is placed for cacheing the static contents like JS and CSS files next to the LB which will serve them  and reduce requests to the Original source.





