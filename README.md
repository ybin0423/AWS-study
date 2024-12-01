# AWS-study
**IAM**
- User; IDs representing human
- Group; Collection of users
- Role; AWS services, granting external access to my account 

Default VPC CIDR = 172.31.00/16
AMI - used to create EC2
- only works in one region 
- can't be edited, update configuration and make new AMI

**HA** = agreed level of operational performance (어느정도 퍼포먼스)
**FT** = operte through faults (다른 부분이 메꿔줌)
**DR** = enable the recovery or continuation (회복탄력성)

**DNS Hierarchy** = Root servers -> .com zone -> amazon.com zone 
SCP = account permissions boundaries 
-> limit what account can do (X grant permission)
-> 권한을 주지 않지만 제한만 한다. 

**Cloudwatch Logs** = accept, store and monitor logging data
CloudTrail = management events 
Logs API calls/ activities = CloudTrail Event 
90days stored by default in Event History 

Control Tower = govern multi-account environment 
Landing zone = well-architected multi-account environment 
Guard Rails = rules for multi-account governance
Account Factory = automated account provisioning 

***Object Versioning & MFA Delete
-> once enabled, can never disable it
-> store multiple versions of objects within bucket 

**S3 Encryption** 
- Client Side Encryption 

  **Server Side Encryption**
-> S3 manage actual encrytpion but client only needs to manage keys
-> When uploading object, provide object and key  

**S3 Bucket Replication**
- CRR: cross-region replication
- SRR: Same-region replication

**S3 Object Lock**
- store objects using WORM model (prevent objects from deletion)

VPC Subnets 
-> AZ resilient 

**IGW**
- region resilient gateway attached to VPC 
- Gateways traffic bw VPC and Internet or AWS public zone (S3, SQS, SNS)

**TCP**
- connection based protocol 
- connection bw two devices using random port& known port on client and server 

**NAT Gateways**
-> use elastic IPs (Static IPv4 Public)
- only support NACLs
- AZ resilient service 

**EC2**
- AZ resilient - very reliant on AZ 

**Virtualization**
- running more than one operating system 
- Kerner is only part of operating system directly interacting with hardware

**EBS (Elastic Block Storage)**
- block level storage volumes with EC2 instance  usage 
- data only exists encrypted from 

**Instance Store**
- provide temporary block-level storage
(instance store vs ebs)

**EBS snapshots**
- backups of data consumed wihtin EBS volumes 

**Elastic Network Interface (ENI)**
- every EC2 instance has at least one ENI
- launching instance with SG, SG is on ENI, not instance itself 
- ENI has Mac address

Every EC2 instance have 2 status check
1. System status 
- loss of system power/ network conenctivity

2. Instance status 
- corrupted file system 

Termination Protection 
- feature to add attribute to EC2 instance 
- protection against unintended termination 
- allows separation 

**Horizontal and Vertical Scaling**
- systems have to deal with increasaing/ decreasing user-side load
- adding or removing resources to system 
Horizontal; adding more instance as load increases
Vertical Scaling; resizing EC2 instance 

**Instance Metadata**
- data about my instance tha I can use to configure or manage 
- Not authenticated or encrypted 

**Image Anatomy**
- running copy of docker image
- made up of multiple layers

**Container Anatomy**
- running copy of docker image with one additional read/write layer 
-> anything happening during running is stored in this layer 
-Dockerfiles used to build images 

**ECS (Elastic Container Service)**
- remove admin overhead of managing containers 
- run in 2 modes ; 1.EC2 2. Fargate 

**1.EC2 Mode**
- EC2 cluser created within VPC
- ASG - Auto Scaling Group -> Horizontal Scaling 
- keep overhead and flexibility

**2. Fargate mode**
- Severless - no servers to manage
- Tasks = services running from shared infrastructure platform
- only pay for the containers i'm using based on resources I consume

**ECR (Elastic Container Registry)**
- managed container image registry service 
- each registry has repositories and each repository hav images

**Kubernetes**
- open-source system for automating deployment, scaling, managemetn of containerized application
- Kubernetes API used for communication bw control plane & kubelet agent 

**Cluster structures**
- Cluster = deployment of Kubernetes, management
- Node = resources
- Pod = 1+ containers; smallest unit
- Service = abstraction, service on one or more pod 
- Job = Adhoc, creates one or more pods until completion 
- Ingress= way to service ( ingress-> routing -> service -> pod)
- Ingress controller
- Persistent storage = volume used for pod 

**Advanced EC2**
- EC2 bootstrapping = process of configuring EC2 instance to perform automated install & configuration steps before instance brought to service 
- bootstrapping = processing allowing system to self-configure
- bootstrappingallow EC2 build automation 

**CFN-INIT**
- helps to set a state for things like package, users, groups 
- enhance bootstrapping

EC2 instance roles & profile 
- how applicaions running on EC2 instance can be given permission to access AWS resource

Reliability = capability of workload to be able to recover successfully from infrastructure 
or service disruption or network failure

Resiliency = capability of system or component to withstand external stresses 
* resilient system designed for high availability operation and recover quickly


**regarding the kuberenetes cluster structure,
inside the cluser there is 
-node
-control plane 
and kubelet is agent component inside the node
and kubernetes api is component inside the control plane used for communication

**Bootstrapping**-> allows to automate self-configuration
self-configuration = adaptive coordination

1.Simple Routing
- directs traffic to single resource

2.Failover Routing
- routes traffic to primary resource

3.Multi-Value Routing
- returns multiple IP addresses in response to DNS query

IAM 
- User; IDs representing human
- Group; Collection of users
- Role; AWS services, granting external access to my account 

Default VPC CIDR = 172.31.00/16
AMI - used to create EC2
- only works in one region 
- can't be edited, update configuration and make new AMI

HA = agreed level of operational performance (어느정도 퍼포먼스)
FT = operte through faults (다른 부분이 메꿔줌)
DR = enable the recovery or continuation (회복탄력성)

DNS Hierarchy = Root servers -> .com zone -> amazon.com zone 
SCP = account permissions boundaries 
-> limit what account can do (X grant permission)
-> 권한을 주지 않지만 제한만 한다. 

Cloudwatch Logs = accept, store and monitor logging data
CloudTrail = management events 
Logs API calls/ activities = CloudTrail Event 
90days stored by default in Event History 

**Control Tower** = govern multi-account environment 
Landing zone = well-architected multi-account environment 
Guard Rails = rules for multi-account governance
Account Factory = automated account provisioning 

**Object Versioning & MFA Delete**
-> once enabled, can never disable it
-> store multiple versions of objects within bucket 

S3 Encryption 
- Client Side Encryption 

- Server Side Encryption 
-> S3 manage actual encrytpion but client only needs to manage keys
-> When uploading object, provide object and key  

S3 Bucket Replication
- CRR: cross-region replication
- SRR: Same-region replication

S3 Object Lock 
- store objects using WORM model (prevent objects from deletion)

VPC Subnets 
-> AZ resilient 

**IGW**
- region resilient gateway attached to VPC 
- Gateways traffic bw VPC and Internet or AWS public zone (S3, SQS, SNS)

**TCP**
- connection based protocol 
- connection bw two devices using random port& known port on client and server 

**NAT Gateways**
-> use elastic IPs (Static IPv4 Public)
- only support NACLs
- AZ resilient service 

EC2 
- AZ resilient - very reliant on AZ 

**Virtualization**
- running more than one operating system 
- Kerner is only part of operating system directly interacting with hardware

**EBS (Elastic Block Storage)**
- block level storage volumes with EC2 instance  usage 
- data only exists encrypted from 

Instance Store
- provide temporary block-level storage
(instance store vs ebs)

**EBS snapshots**
- backups of data consumed wihtin EBS volumes 

**Elastic Network Interface (ENI)**
- every EC2 instance has at least one ENI
- launching instance with SG, SG is on ENI, not instance itself 
- ENI has Mac address

Every EC2 instance have 2 status check
1. System status 
- loss of system power/ network conenctivity

**2. Instance status**
- corrupted file system 

**Termination Protection **
- feature to add attribute to EC2 instance 
- protection against unintended termination 
- allows separation 

**Horizontal and Vertical Scaling**
- systems have to deal with increasaing/ decreasing user-side load
- adding or removing resources to system 
Horizontal; adding more instance as load increases
Vertical Scaling; resizing EC2 instance 

**Instance Metadata**
- data about my instance tha I can use to configure or manage 
- Not authenticated or encrypted 

**Image Anatomy**
- running copy of docker image
- made up of multiple layers

**Container Anatomy**
- running copy of docker image with one additional read/write layer 
-> anything happening during running is stored in this layer 
-Dockerfiles used to build images 

**ECS (Elastic Container Service)**
- remove admin overhead of managing containers 
- run in 2 modes ; 1.EC2 2. Fargate 


