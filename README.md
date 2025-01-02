 ## AWS-study

### **Hierarchy and Relationship**
VPC (Virtual Private Cloud), Subnet, S3 (Simple Storage Service), and ENI (Elastic Network Interface) are fundamental components of AWS networking. Here's an explanation of their structure and how they fit together, along with a simplified diagram.

1. **VPC (Virtual Private Cloud)**:
   - A VPC is a virtual network dedicated to your AWS account.
   - It contains **subnets**, which are subdivisions of the VPC.
   - VPCs also include routing tables, internet gateways, NAT gateways, and other networking resources.

2. **Subnets**:
   - Subnets divide the VPC into smaller networks.
   - Each subnet is associated with a specific Availability Zone (AZ).
   - Subnets can be **public** (accessible from the internet) or **private** (isolated).
     
3. **EC2 Instance**:
   - EC2 인스턴스는 AWS 클라우드의 가상 서버 (인스턴스 유형에 따라 하드웨어가 지정됌)
   - Amazon EC2를 사용하여 원하는 수의 가상 서버를 구축하고 보안 및 네트워킹을 구성하며 스토리지를 관리할 수 있다.
   - 용량을 추가(스케일 업)하여 월간 또는 연간 프로세스 또는 웹 사이트 트래픽 급증 등 컴퓨팅 사용량이 많은 작업을 처리할 수 있다.
   - Used for hosting web applications and APIs and hosting databases or backend applications.


4. **ENI (Elastic Network Interface)**:
   - An ENI is a virtual network card attached to an EC2 instance or other resources in the VPC.
   - It holds IP addresses, MAC addresses, and security groups.
   - It enables communication between resources within the VPC or to external networks.
   - EC2 instance에게 자동으로 생성 (EC2 의 ip address, mac address를 가지고 있다.
   - (EC2의 <ins>서브넷 위치 (address)</ins>와 <ins>보안그룹을 연결</ins>을 담당)

5. **S3 (Simple Storage Service)**:
   - S3 is not part of a VPC but can be accessed from resources within a VPC.
   - S3 buckets are global but can be accessed using VPC endpoints for secure and private connectivity.
   - Amazon S3 is an **<ins>object storage service</ions>** designed for storing and retrieving large amounts of data, including files, backups, and media.

---

### **Diagram Explanation**

Below is a high-level representation of the structure.

```
+-------------------------------------------+
|                 AWS Account                |
|  +--------------------------------------+  |
|  |                VPC                   |  |
|  |                                      |  |
|  |   +------------+    +------------+  |  |
|  |   |  Subnet 1  |    |  Subnet 2  |  |  |
|  |   | (Private)  |    | (Public)   |  |  |
|  |   +------------+    +------------+  |  |
|  |      |                       |       |  |
|  |      |                       |       |  |
|  |   +---------+         +--------------+|  |
|  |   |   ENI   |         |  Internet GW ||  |
|  |   |         |         +--------------+|  |
|  |   +---------+                        |  |
|  |                                      |  |
|  +--------------------------------------+  |
|                                           |
|            S3 (Global Service)           |
+-------------------------------------------+
```

### **What’s Inside and Outside**
- **Inside the VPC**:
  - **Subnets**: Each subnet belongs to a specific AZ and can hold EC2 instances or other resources.
  - **ENIs**: Attached to EC2 instances, ENIs enable communication within the VPC.
  - **Routing Tables, Gateways**: Manage traffic between resources.

- **Outside the VPC**:
  - **S3**: A global service, not physically within the VPC but accessible via endpoints or internet.

![image](https://github.com/user-attachments/assets/3b74a816-4c99-4773-a913-0dbe310f5e3f)
image created by: ChatGPT

--- 

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

**ECS (Elastic Container Service)**
- remove admin overhead of managing containers 
- run in 2 modes ; 1.EC2 2. Fargate 

---

**EC2 vs ECS vs Lambda**
1. EC2
   -> provide virtual servers in cloud, giving users **<ins>full control over operating system and software</ins>**
2. ECS
   -> fully manaaged **<ins>container orchestration service</ins>** to manage docker service on virtual mahchines
3. Lambda
   -> serveless computer service to **<ins>automatically runs code in response to events</ins>** (event driven tasks/ automation task/ backend api)
- **severless** = 클라우드 컴퓨팅 모델중 하나로 개발자가 서버를 직접 관리할 필요가 없음
Here’s a detailed comparison of **EC2**, **ECS**, and **Lambda** based on their features, use cases, and limitations:

### **Comparison Table**

| Feature                | **EC2**                     | **ECS**                      | **Lambda**                  |
|------------------------|-----------------------------|------------------------------|-----------------------------|
| **Compute Type**       | Virtual Machine             | Containers                   | Function-as-a-Service       |
| **Scalability**        | Manual or auto scaling      | Managed container scaling    | Automatic event-based       |
| **State Management**   | Stateful                    | Stateful or stateless        | Stateless                   |
| **Cost Model**         | Pay for uptime             | Pay for cluster (or Fargate) | Pay per request + duration  |
| **Control**            | Full server control         | Partial (containerized apps) | No infrastructure control   |
| **Startup Time**       | Minutes (instance boot)     | Seconds (container launch)   | Milliseconds                |
| **Best For**           | Long-running workloads      | Microservices and batch jobs | Event-driven tasks          |

---

**EBS (Elastic Block Storage)**
- aws 클라우드의 ec2에 사용될 <ins>영구</ins> 블록 스토리지 볼륨 제공. (자동으로 복제되어 보존성 제공)
- ebs는 하드디스크 부분.

**Block Storage VS Object Storage**
- Block Storage = 무엇을 설치할 수 있다
- Object Storage = 파일만 저장할 수 있다.

**EBS vs EFS vs S3**

| Feature/Criteria     | **EFS** (Elastic File System)                         | **EBS** (Elastic Block Store)                      | **S3** (Simple Storage Service)                      |
|-----------------------|------------------------------------------------------|---------------------------------------------------|-----------------------------------------------------|
| **Storage Type**      | Fully managed network file system (NFS).             | Block storage (like a virtual hard drive).        | Object storage for unstructured data.               |
| **Data Access**       | Shared, multi-instance access. Supports concurrent access from multiple EC2 instances. | Single-instance access; attached to one EC2 instance at a time. | Global access via APIs, SDKs, and the web interface. |
| **Use Cases**         | File sharing, content management, home directories, machine learning. | Persistent storage for EC2 instances, databases, or low-latency apps. | Data lakes, backups, archives, content delivery, static websites. |
| **Protocol**          | NFSv4.0 and NFSv4.1                                  | Attached as a block device (via iSCSI).           | REST API, S3 CLI, and SDKs.                         |
| **Performance Modes** | - General Purpose: Low latency. <br> - Max I/O: High throughput for large workloads. | - GP3 (General Purpose): Optimized for general use. <br> - IO1/IO2 (Provisioned IOPS): For high I/O workloads. | - Standard: High durability and availability. <br> - One Zone IA: Lower-cost infrequent access. |
| **Durability**        | 11 nines (99.999999999%) durability, built across multiple AZs. | Durability depends on the specific EBS volume, but backed by replication within an AZ. | 11 nines (99.999999999%) durability, across multiple AZs. |
| **Scalability**       | Scales automatically up to petabytes.                | Fixed size (1 GiB to 64 TiB); resize manually.     | Virtually unlimited storage.                        |
| **Availability**      | High availability across multiple AZs.               | Single AZ by default; can use snapshots for cross-AZ resilience. | High availability across multiple AZs (Standard tier). |
| **Pricing**           | Pay-as-you-go based on storage used.                 | Pay per GB provisioned.                           | Pay per GB stored, and data requests/transfer.      |
| **Latency**           | Low latency, suitable for file operations.           | Lowest latency, suitable for block-level operations. | Higher latency compared to EFS/EBS.                 |
| **Backup & Restore**  | Supports AWS Backup service.                         | Supports snapshots for backups and restore.       | Versioning and lifecycle management for backup.     |
| **Encryption**        | Encryption at rest using KMS.                        | Encryption at rest using KMS.                     | Encryption at rest using KMS or S3-managed keys.    |
| **Access Control**    | IAM, security groups, NFS access rules.              | IAM, security groups.                             | IAM, bucket policies, ACLs.                         |
| **Limitations**       | Limited to NFS-compatible workloads; more expensive than S3 for storage. | Single-instance attachment; scaling requires resizing. | Not suitable for low-latency or transactional workloads. |


### **Key Differences**
1. **EFS (파일)** :
   - Use for shared, scalable, file-level storage (e.g., for web servers or shared app data).
   - Managed service with automatic scaling.
   - More expensive but ideal for multiple EC2 instances requiring file access.
   - 여러 AZ에서 동시 접근, 수천개의 EC2 instance와 연결.

2. **EBS (블록)**:
   - Use for high-performance, block-level storage attached to a single EC2 instance.
   - Requires manual resizing for scaling.
   - Best suited for databases, file systems, or transactional applications.

3. **S3**:
   - Use for scalable object storage, archiving, and content delivery.
   - Ideal for unstructured data like images, videos, backups, and logs.
   - Cost-effective for large data volumes but not suitable for low-latency transactional access.

 대기시간 빠른 순서: EBS > EFS > S3

 ### Block Storage vs File Storage vs Object Storage

**Block Storage**
-> 빠른 액세스 및 검색에 최적화된 방식.
- 파일과 데이터베이스같은 데이터를 가져와 블록 (동일한 크기)으로 나눔 -> 기본 물리적 스토리지에 데이터 블록을 저장
- 빠르고 신뢰할 수 있는 데이터 액세스가 필요한 애플리케이션에 사용됨.
- 정형 (미리 정의된 구조를 따르는 데이터) 데이터베이스 스토리지, VM 파일 시스템 볼륨, 대량의 읽기 및 쓰기 로드에 유용

**Object Storage**
-  대량의 비정형 데이터에 적합.
-  각 객체에 고유 식별 코드가 제공되고 그 객체에 대한 설명 (= <ins>메타데이터</ins>)가 포함됨.

**File Storage**
- 파일 및 폴더의 계층 구조로 데이터를 저장.
- 특정 환경에 데이터를 저장한다. (블록은 운영체제와 통합.)
- 최종 사용자 컴퓨팅을 위한 직관적 인터페이스 사용.

---

### **Summary of Use Cases**
| **Scenario**                  | **Recommended Service**          |
|--------------------------------|-----------------------------------|
| Shared storage across instances | EFS                              |
| High-performance storage for a single instance | EBS                              |
| Large-scale object storage, backups, or archives | S3                              |
| Hosting a static website        | S3                              |
| Machine learning input/output   | EFS or S3                       |
| Low-latency database storage    | EBS                             |

---

**ELB**
- EC2 인스턴스, IP 주소, 컨테이너에 트래픽을 분산함.
- 등록된 대상의 상태를 모니터링하며 양호한 상태인 경우 트래픽을 routing 함.
- 수신 트래픽의 변화에 따라 load balancer의 용량을 자동으로 조절함.

**TLS/SSL** - 전송 계층 보안 
- securing an internet connection by <U>encrypting data</U> sent between a website and a browser (or between two servers)
- HTTPS: website secured by using TLS or SSL (HTTPS 작동 방식 공부)
- **SNI**: TLS 암호 프로토콜의 확장버전, TLS 핸드쉐이크의 첫 단계에서 클라이언트가 어느 호스트명에 접속하려는지 서버에 알리는 역할.
  (클라이언트가 서버에서 어떤 호스트이름과 대화하는지 표시하는 방법)
- ***호스트이름: 네트워크에 연결되는 장치의 이름*** (인터넷에서 도메인 이름 또는 웹 사이트 이름은 호스트 이름의 한 유형)
- **TLS 핸드쉐이크** = 통신을 하는 브라우저와 웹 서버가 서로 <ins>암호화 통신</ins> 을 시작할 수 있도록 신분을 확인하고, 필요한 정보를 클라이언트와 서버가 주고 받는 과정

---
### 웹 브라우저 vs 웹 서버 

- Web browser = Stands on the user-side, displays the web page and process the requests from server
- Web server = Stands on the server-side, process teh request if the user clicks or searchs for something
  
AWS SDK - 언어별 API를 제공하고, 서명 계산, 요청 재시도 처리 및 오류 처리와 같은 많은 연결 세부 정보를 관리.
AWS RDS - 관계형 데이터베이스 (Relational Database)를 클라우드에서 설정하도록 하는 웹 서비스. 

---
**ASG (Auto Scaling Group)**
- 애플리케이션의 수요에 따라 EC2 인스턴스의 수를 자동으로 조정하는 기능.

**Scaling Policy**
- 스케일링이 발생하는 조건과 스케일 아웃/인을 수행하는 작업

**Scaling In** = Reduce numbers of instances in ASG

**Scaling Out** = Increase numbers of instances in ASG

**Amazon Aurora** 
-> 완전 관리형 관계형 데이터베이스 엔진
+ 데이터 베이스 클러스터링 및 복제를 자동화.

+ **ElastiCache** =  완전 관리형 (Fully Managed) 인 메모리 데이터 저장소 및 캐시 서비스.
-> 백엔드 스토리지에서 가져오는 데이터를 캐싱 (Cache) 하여 엑세스 속도를 향상시킴.
- 데이터를 더 빨리 가져오기 위한 메모리 기반의 저장소 서비스. 
- 액세스 속도가 빠른 특성상 성능이 중요한 애플리케이션에서 사용됨. 

**In-Memory 데이터 베이스**
-> 데이터를 메모리에 저장하고 처리하는 방식. (보통은 디스크에 저장하고 꺼내쓴다.)
- Key: Value 형태로 저장됨.
  
장점: 100~ 1000배 가량 빠름
단점: 데이터 저장이 휘발성이라 DB 서버 전원이 꺼지면 안에 있는 자료들이 즉시 삭제됨.

**인메모리 DB 종류**
1. ***Redis***:
   - 고급 기능
   - S3와 연결돼 백업 / 복원할 수 있고 데이터를 영구적으로 보존할 수 있음.
   - Single Thread: 한번에 한 작업만 처리.
   - 보안 기능 有.

2. ***Memcached***:
   - 심플한 버젼.
   - Multi- Thread; 여러 스레드가 동시에 요청 처리가능. 
   - 주로 빠른 캐싱 서비스가 필요한 애플리케이션에서 사용되고 다른 중요한 DB는 다른 스토리지에 저장되거나 하면서 사용됨.
---
### Route 53
-> DNS 웹 서비스 (확장성과 가용성이 뛰어남.)

**DNS 작용방식**
-> 도메인을 IP 주소로 변환시켜 주는 서비스. 
- 쿼리가 전송되면 각각 루트 서버, TLD 서버를 거쳐 해당 도메인에 해당하는 IP주소를 받고 해당 주소로 접근함.

### S3 
-> 클라우드 스토리지 서비스.

**S3 Bucket / S3 Object**
- 버킷의 이름은 유일하게 함 (unique).
- S3 버킷안에 저장되는 데이터는 모두 객체라고 불림. (버킷 = 마트, 객체= 상품)
- S3는 데이터를 <ins>인터넷</ins>을 통해 객체 형태로 저장하는 서비스.
- 객체를 업/다운로드 하는데 HTTP/HTTPS를 통한 API가 사용됨.

**Route53**
- DNS서비스 중 하나로 도메인을 IP로 변환하여 목적지 Ip를 찾아가는 과정

**ASG** (Auto Scaling Group)
- collection of EC2 instances, sharing similar characteristics and treated as logical grouping for management and dynamic scaling.

**CloudFront**
- 낮은 지연시간

**Snow Family**
- 데이터 마이그레이션 기능

**Kinesis**
- 실시간 스트리밍 데이터 수집, 처리, 분석 기능
- Kinesis Data Stream: 데이터 스트림 수집하여 처리 및 저장.
- Kinesis Data Firehose: 오토 스케일링 및 데이터 형식 변환.
- Kinesis Data Analytics: SQL 등으로 데이터 스트림 분석.

**EFS**
- 관리형 NFS, 많은 EC2에 마운트

**ELB**
- 단일 액세스 지점 제공.
---
### 오답

- On-Premise = 가상의 공간에 서버 저장 x, 자체적으로 시스템을 구축해 서버 저장
- **AWS Snowball Edge** = Data Transport service that can put data in/out to the cloud **[파일 migration의 용도]**
- Amazon SQS = 메세지를 프로그래밍적으로 보내는 것.
- AWS Athena = S3에 쿼리하는 것.
- 복원력과 확장성을 극대화하기 위한 최상의 솔루션 -> Amazon SQS 대기열을 작업의 대상으로 사용; 컴퓨팅 노드에서 기본 서버가 분리되어 독립적으로 확장
- 
---
- Cloud Trail = AWS에서 발생한 API 요청을 로그를 모두 기록해놓은 것.
- 낮은 지연시간 접근, DDoS 공격 보호, 파일 분산 및 캐싱, S3/ALB/EC2/S3 웹사이트 가능
- Resilience = 복원력있는 
