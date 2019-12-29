* Regions are geography locations and availability zones are data centers.
* Edge locations has webservers.
* [AWS global infrastructure](http;//aws.amazon.com/about-aws/global-infrastructure)
* Hardware refresh cycle to avoid component failure probably every 4 years.
* Always on monitoring systems. hardware, network, components etc. If not, they will loose money for not meeting SLA's
* [Security certifications](https://aws.amazon.com/compliance)

### Shared security responsibility

#### AWS Responsibility
* Virtual host security
* Storage security
* Network Security
* Data Center Security
* Database Security

#### Our Responsibility
* AWS account security -MFA, API
* Operating System
* Database
* Applications
* Data encrption
* Authentication
* Network Integrity

### Security Methods and Connectivity
* Direct Connect - Gigabit ethernet connctivity into their DCs
* Security Groups - Which servers have access to which others
* VPC - ACLs
* Dedicated Server - where you cannot share hardward because of some compliance reasons.

### Identity and Access Managmement
* Users and Service management controls access to AWS resources
* Multifactor Authentication
* API Access - [IAM](https://aws.amazon.com/iam/)

### Storage
* Ephermal storage is storage on the instace. Its data is lost, if the instance is terminated. It is free and storage could be shard by other services on the instance. Perfect usage for replication. Rebooting doesn't loose data.
* Elastic block storage is a persistant storage for Ec2. This can be attached to EC2. You can take snapshot of the storage, and it will stored in S3, but not visible for us. Unlike S3, not internet accessible.
* Glacier is a cheap storage. Ideal for backup. very very slow.

### Pricing
Pricing is per hour
* On-demand instances/per hour
* Reserved Instances - 1 to 3 years contract. low per hour price.
* Spot instances are unused AWS capacity. cheap hourly rate. not guaranteed. bidding

### Route 53 
It is a DNS Service and it is available everywhere and its uptime is 100%

### AWS Cloud Watch
* Basic monitoring - 7 metrics, 5 min
* Set alarms and alerts
* Notifications via SES, SNS
* Auto scale integrates with CloudWatch

### Amazon Database Options
* [Running databases](https://aws.amazon.com/running_databases)
* You can have both relational and non relationa databases. you can bring your own licenses. CDRS is supported.

### Amazon Lambda
* It is a event-driven compute service
* Runs code triggered by events on compute platform.
* Does not require an instance or infrastructure.

## Amazon Simple Services
* SES-Simple Email Service - For sending bulk emails, ad campaigns
* SQS-Simple Queueing Service-Fast, reliable, scalable and unlimited messages and queue size.
* Simple Notification Service.

### CloudFront 
Global CDN. Caches static content and proxies dynamic content.

### Cloud Formation 
Automate AWS resource provisionning through templates.

### Elastic Beanstalk 
More for developers. Uses Cloud Formation templates. Ex: IIS app.

### CloudTrail 
Records API Calls. request, response, etc.

### Virtual Private Cloud(VPC)
* Logically isolated network in the AWS cloud. Little more control. ACLs.
* Enhanced security with access control list.
* Control of network architecture, subnets, networking etc.
* Ability to assign elastic public IP addresses.
* VPC itself is free.
* VPC Elements: Subnets, Route Tables, Internet Gateways, Elastic IPs, Endpoints (Call doesn't go through internet. Ex: S3 call) and NAT Gateway.
* Peering Connections, Network ACLs, Security Groups, VPNs.
* VPC Characteristics
    *AWS reserves 5 IP addresses per subnet. first 4 and last one.
    * Security Groups: Resource level traffic firewall, instance, ELB, etc
    * Ingress and egress traffic
    * Stateful - Return traffic allowed.

* Configuring NAT Instances, Nat Gateways and VPC endpoints. Single NAT can lead to bottlenecks, if too much traffic passes through. Instead use NAT Gateway
* 1 Subnet can have 1 NAT, to scale out you need to break subnets.

### NAT Instances: 
* Use a script to manage failover between instances
* Depends on the bandwidth of the instance type.
* Managed by you.
* A generic Amazon Linux AMI thats configured to perform NAT
* Manual port forwarding. 
* Use a bastion server.
* View CloudWatch alarms.

### NAT Gateways: 
* Since it is a service, highly available with redundancy.
* Supports bursts upto 10gbps
* Managed by AWS
* Software is optimized for handling NAT traffic
* Port forwarding is not supported.
* Bastion server not supported.
* Traffic metrics not supported.

### EC2 instance types
* On-demand: highest hourly rate. no commitment. Ideal for auto scaling.
* Reserved: standard - lower hourly rated based on commitment.Ideal for predictable usage.
* Reserved: Scheduled - Instannces can be purchased during specific times. Like end of everymonth or christmas.
* Spot : Excessive AWS capacity. Dramatically cheap. Autioned prices.
* Dedicated: Host - Good for bring your own licenses. Also satisfies regulatory compliance requirements. High price.
* Dedicated: Instance - No visibiliy into cores or hardware.

### Placement Groups: 
* A logical grouping of instaces in a single availability zone. low latency and high performance.
* Existing instances cannot be moved into a placemennt group.

### Load Balancers
ELB, Classic LB, Application LB
#### Elastic Load Balancer
* Health checks and load balancing
* Integrates with Route53
* Supported Ports: 25(SMTP), 80/443(HTTP, HTTPS), 1024-65535
* Does not support EIP
* Supports domain zone apex.
#### CLB
* region wide load balancer, SSL termination and processing. Layer4 and Layer 7.
* Cookie-based sticky session.
* Integrates with Auto Scaling.
#### Application load balancer characteristics:
* Layer 7 only.
* Content-based routing.
* support for microservices and containers.
* Integrates with ECS
* Better performance for real-time streaming.
* Reduced hourly cost.
* Path based routing: Intelligent routing.
```
abc.com/orders - One target group
              /images - Other group
```

### Auto Scaling Components
* Auto Scaling Groups
* Launch Configuration
* Scaling Plans.

### Elastic Block Storage
* GP-SSD
* PIOPS
* Throughput Optimized HDD
* Cold HDD
* Magnetic - Being phased out.
* Does not need to be attached to an instance
* Cannot be attached to more than one instance at the same time.
* Can be transferred between AZs
* EBS volumne data is replicated across multiple servers in an AZ

### Elastic File System- EFS
* Network attached storage
* Simple, petabyte scalable file storage for use with EC2 instances.
* Good usages for BigData, streaming etc.

### Storage and Archive services
* S3-Object based storage
* Glacier - Cheap longterm storage - Archiving
* EBS - Block based storage
* EFS - NAS type file based storage
* AWS Import/Export - Ship storage arrays.
* AWS Snowball - Encrypted storage device for shipping. For transferring petabytes of data.
* Storage Gateway 

### S3 Features:
* Versioning, Cross-Region replication, Data lifecylce management, MFA delete, Permissions, Time-limited access to objects.

### CloudFront-CDN from edge locations
* Distribution types: Web static content, RTMP
* Geo Restriction: Whitelist or backlist countries, Custom error pages, console or API access.
* HTTP Methods: GET, PUT, POST, PATCH, DELETE and OPTIONS
* Caches responses for only GET.
* Zone Apex: Route 53 Alias record mapping to cloudfront distribution. Use smaller DNS names.
* Wildcard CNAME: Support subdomains
* SSL: Supports wildcard SSL certs, Dedicated IP custom SSL, SNI Custom SSL.
* Edge Caching can cache dynamic content.

### AWS Relational Database Services
* Database engine managed by AWS
* Multi-AZ deployment options
* On-demand and reserved instance pricing.
* Magnetic, GP-SSD, or PIOPS
* Continuously track changes and backs up DB
* Volume snapshot of entire DB instance, not just DBs
* One day backups retained by default.
* Automated backups happen in 30 min window.
* You cannot restore into existing DB instance.
* Read replica's, writes happen async. Standby replica, writes happen synchronously.

### Dynamo DB
* Fully managed, HA, NoSQL DB
* Synchronously replicates data across 3 AZs
* SSKs and limiting indexing on attributes. Provides high throughput.
* ElasticCache can be used in front of DynamoDB for reads.

### DynamoDB integration
* Amazon Elastic MapReduce
* Amazon Redshift
* Amazon Data pipeling
* Amazon S3
* Management Console and APIs
#### Features
* Secondary Indexes
* Streams- Changes happend
* Cross-region Replication
* Triggers - Integrates with Lambda
* Schema-less

### ElastiCache 
* Memcached or Redis
* Memcached is multithreaded and supports horizontal scaling.

### Amazon Redshift
* Fast and fully managed petabyte scale relational data warehouse service
* Analyze data using existing business intelligence tools
* HDD and SSD platforms
* Columnar store
* Continuous and incremental backups to s3 across regions

### Route 53
* Worldwide distributed DNS
* Its a database of name and IP mappings
* 100% SLA uptime.
#### Routing policies
Geolocation, round robin, etc

### AWS Monitoring
* CloudTrail: Log every action, not enabled by default. History of API calls.
* CloudWatch: Monitoring service, collects and track metrics, monitors logs, set alarms, automatically reach to changes in AWS resources.
* CloudWatch Logs: These are stored indefinitely. Alarm history stored for 14 days.
* Trusted Advisor: A service that helps to reduce cost, increase performance, etc. Automated AWS audits.
* Kinesis Streams: For streaming data. Producer consumer pattern. Default data is stored for 24 hours.

### AWS CloudFormation
* Programmatic way to create and manage AWS resources.
* CludFormation templates written in JSON. templates are architectural designs. Its free.

### Elastic Beanstalk
Geared towards developers. Upload code. It will figure how to deploy, cpacity, provisioning, etc.




















































