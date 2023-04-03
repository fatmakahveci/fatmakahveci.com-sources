---
title: AWS Certified Solutions Architect - Associate (SAA-C03)
description: AWS Certified Solutions Architect - Associate (SAA-C03)
summary: "Updated by Fatma, Apr 03, 2023."
date: 03-04-2023
categories:
  - "Coding"
tags:
  - "aws"
  - "coding"
  - "cloud computing"
---

![aws](/img/aws.png)

## 1. Cloud computing

- _Cloud computing_ is the on-demand delivery of IT resources over the Internet with pay-as-you-go pricing.
- Instead of buying, owning, and maintaining physical data centres and servers, you can access technology services, such as computing power, storage, and databases, on an as-needed basis from a cloud provider.

### 1.1 Advantages of cloud computing

1. Trade capital expense for variable expense - pay only when you consume
2. Benefit from massive economies of scale - lower pay-as-you-go prices
3. Stop guessing capacity - access as much or as little capacity as you need
4. Increase speed and agility - a click away from IT resources
5. Stop spending money to run and maintain data centres - focus on projects, not the infrastructure
6. Go global in minutes - low latency with easily deployed applications in multiple regions

### 1.2 Types of cloud computing

1. **Infrastructure-as-a-Service (IaaS)** provides access to networking features, computers, and data storage space. It provides you with the highest level of flexibility and management control over your IT resources.
2. **Platform-as-a-Service (PaaS)** removes the need for managing the underlying infrastructure (usually hardware and OS). You don't need to worry about resource procurement, capacity planning, software maintenance, patching, etc.
3. **Software-as-a-Service (SaaS)** provides a completed product that is run and managed by the service provider. i.e., web-based email which you can use to send and receive email without having to manage feature additions or maintain the servers and OS.

### 1.3 Cloud computing deployment models

- Factors to be considered for selecting a cloud strategy:
  - Required cloud application components
  - Preferred resource management tools
  - Any legacy IT infrastructure requirements.

#### 1.3.1 Cloud-based deployment

- Run all parts of the application in the cloud.
- Migrate existing applications to the cloud.
- Design and build new applications in the cloud.

#### 1.3.2 On-premises deployment

- Private cloud deployment
- Deploy resources by using virtualization and resource management tools.
- Increase resource utilization by using application management and virtualization technologies.

#### 1.3.3 Hybrid deployment

- Connect cloud-based resources to on-premises infrastructure.
- Integrate cloud-based resources with legacy IT applications.

### 1.4 Serverless computing

- _Serverless_ means that your code runs on servers, but you do not need to provision or manage these servers.
- It gives the flexibility to scale serverless applications automatically.
- Serverless computing can adjust the applications' capacity by modifying the units of consumption, such as throughput and memory.
- You cannot see or access the underlying infrastructure or instances.

### 1.5 A client-server model

- Most modern computing uses a basic client-server model.
- A client can be a web browser or desktop application that a person interacts with to make requests to computer servers.
- A server can be a service such as Amazon Elastic Compute Cloud (Amazon EC2), a type of virtual server. It evaluates the details of a request and fulfils it by returning the information to the client.

### 1.6 Cloud computing architecture

- It consists of two fundamental components, frontend and backend.

#### 1.6.1 Frontend platform

- The _frontend_ contains the client infrastructure—UIs, client-side applications, and the client device or network that enables users to interact with and access cloud computing services. It communicates with the backend and sends queries via the middleware.

#### 1.6.2 Backend platform

- The _backend_ contains the cloud architecture components that make up the cloud itself, including computing resources, storage, security mechanisms, management, and more. It empowers the frontend.
- The followings are the main backend components:
  - **Application** is what the client is accessing from the frontend to coordinate or fulfil client requests and requirements.
  - **Service** takes care of all the tasks being run on the cloud. It manages which resources you can access, including storage, application development environments, and web applications.
  - **Runtime cloud** provides the environment where services are run, acting as an operating system that handles the execution of service tasks and management.
  - **Storage** is where data to operate applications is stored.
  - **Infrastructure** is the engine that steers all the cloud software services.
  - **Management** allocates specific resources to specific tasks and is responsible for the flawless functioning of any cloud environment.
  - **Security** refers to the implementation of different security mechanisms in the backend for secure cloud resources, systems, files, and infrastructure to end users.

### 1.7 Scalability

- It is the ability to handle greater loads by adapting.
  - **Vertical scalability** is to increase the performance of an instance. It is limited by the hardware.
  - **Horizontal scalability** is to increase the number of instances of an application. It is used in distributed systems. It is easier to achieve than vertical scalability.

### 1.8 Domain Name System (DNS)

- It translates human readable domain names to machine readable IP addresses.

### 1.9 Unicast vs Anycast IP

- **Unicast** identifies a single unique host and it sends data to a single destination.
- **Anycast** allows multiple servers to become accessible from a single IP address. All servers are accessible from the same IP address and the client is routed to the nearest one.

### 1.10 Application communication

- **Synchronous** can be problematic if there are sudden spikes of traffic and one of the services gets overwhelmed.
- **Asynchronous** allows applications to scale independently to handle spikes in traffic.

### 1.11 Kubernetes

- It is open-source software that allows you to deploy and manage containerized applications at scale.
- It manages clusters of Amazon EC2 compute instances and runs containers on those instances with processes for deployment, maintenance, and scaling.

### 1.12 IPv6

- It uses 128-bit addresses, which allows for a virtually unlimited number of unique addresses.
- Every IPv6 address is public and Internet-routable.

## 2. Domain 1: Design resilient architectures

**A serverless architecture** is a way to build and run applications and services without having to manage infrastructure. Your application still runs on servers, but all the server management is done by AWS.

### 2.1 Design a multi-tier architecture solutions

- **Multi-tier architecture** pattern provides a general framework to ensure decoupled and independently scalable application components can be separately developed, managed, and maintained.

- Solutions based on access patterns
  - Consider access patterns with regards to who and what needs access, and how they will access the services and architectures
    - Where the connections and requests are coming from
    - What the access pattern looks like from time to time
- Scaling (changes to traffic patterns) strategies for components
  - Consider ways to implement scaling, how various services handle elasticity, methods to automate scaling needs, and services limitations in those considerations
    - Horizontal and vertical scaling methods
- Determining database needs and selecting appropriate computing and storage services
  - Evaluate how architecture requirements will affect the selection of database, storage, and computing services

### 2.2 Design highly-available and fault-tolerant architectures

- Designing for **high availability** means designing for minimal downtime.
  - It focuses on reducing the negative impacts on the end user by prioritizing the restoration of essential services when a component or application fails.
- Designing for **fault tolerance** means designing for zero downtime and service interruption.
  - It generally means higher costs due to much more replication and redundancy.
  - It involves much more complex because of the management of data replication and component redundancy.

- Determine the number of resources needed
  - It includes the redundancy of your normal operational components (servers, databases, etc.), and the usage of the AWS global infrastructure components needed to handle data replication, traffic management, and failure detection.
- Determine which AWS services can be used to improve reliability
- Select highly available configurations to mitigate single points of failure, and select appropriate disaster recovery strategies
  - When looking at an environment, take each component and assess what happens when that component fails.
  - Disaster recovery objectives [(*Ref)](https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-options-in-the-cloud.html)
  ![aws](/img/aws_rec.png)
    - **Recovery time objective (RTO)** is a measure of how quickly can your application recover after an outage.
    - **Recovery point objective (RPO)** is a measure of the maximum amount of data loss that your application can tolerate.
  - Disaster recovery strategies
    - **Active/passive** strategy uses an active site to host the workload and serve traffic. The passive site is used for recovery and does not actively serve traffic until a failover event is triggered.
      - **Backup and restore** strategy is suitable for mitigating against data loss or corruption.
      - **Pilot light** strategy is to replicate data from one region to another and provisions a copy of your core workload infrastructure.
      - **Warm standby** strategy involves ensuring that there is a scaled-down, but fully functional, copy of your production environment in another region.
    - **Active/active** strategy runs your workload simultaneously in multiple regions.
      - **Multi-site active/active** strategy serves traffic from all regions to which it is deployed. Users can access your workload in any of the Regions in which it is deployed.
- Understanding key performance indicators (KPIs)
  - It is important to determine when to take action.
  - Monitoring and benchmarking are the primary ways you can know what normal operations look like.

### 2.3 Design decoupling mechanisms using AWS services

- **Decoupling** refers to components remaining autonomous and unaware of each other as they complete their work as part of a larger system.
- Services in achieving loose decoupling of components
- Decoupling techniques
  - _Synchronous decoupling_ involves at least two components, both must always be available for things to function properly.
    - All instances are unaware of each other and doing the same type of work, but they are doing it independently.
  - _Asynchronous decoupling_ involves communication between components through durable components.

### 2.4 Choose appropriate resilient storage

- Define your strategy to ensure the durability of data
- Identify how data service consistency will affect operations
- Know how to implement across a variety of architectures, including hybrid or non-cloud-native applications.
- Identify storage services that can be used with hybrid and non-cloud-native applications

## 3. Domain 2: Design high-performing architectures

### 3.1 Identify elastic and scalable compute solutions for a workload

- AWS Lambda is scalable and elastic by nature.
  - You can adjust concurrency to meet scaling needs.
- Amazon EC2 is not inherently scalable, but there are ways to do it.
  - You can use Amazon EC2 AutoScaling to meet scaling needs.
  - First, you should choose the right type of Amazon EC2 instance.
    - Identify the needs in terms of CPU, memory, storage, and networking.
    - Choose the instance type family based on app needs
      - `M`: general purposes, such as web servers and databases
      - `C`: compute-intensive apps, such as HPC and gaming
      - `R`: memory-intensive apps, such as enterprise databases and big data analytics
      - `T`: burstable workloads that are spikey in nature, such as small databases
    - Experiment with different instances sizes in the same instance family
      - Start with the basics and upgrade if needed.
  - Choose the appropriate architecture and services that scale to meet performance requirements
  - Know the use cases, benefits, and limitations of AWS compute services
    - i.e. AWS Lambda functions can only run up to 15 mins at a time.
    - Know how to choose what metrics to monitor for scaling
      - i.e. CPU utilization is a common Amazon EC2 metric.
      - Elastic Load Balancing is another option for scaling.

### 3.2 Select high-performing and scalable storage solutions for a workload

- Determine which storage solution is the best fit based on future storage needs
- Know general upper bounds for the capacity of storage solutions
- Determine which solution would be the most appropriate for a situation based on performance
- Be familiar with different Amazon EBS volume types and their performance implications
- Familiarize yourself with Amazon S3
  - Basic API calls
  - Multipart uploads
  - Amazon S3 accelerator
  - Caching with Amazon CloudFront
- Consider using multipart uploads for objects that are over 100 MB instead of uploading the object in a single operation.
  - Using multipart upload can improve throughput, and it could also allow for quick recovery.

### 3.3 Select high-performing networking solutions for a workload

### 3.4 Choose high-performing database solutions for a workload

## 4. Domain 3: Design secure applications and architectures

- Design secure access to AWS resources
- Design secure application tiers
- Select appropriate data security options

## 5. Domain 4: Design cost-optimized architectures

- Identify cost-effective storage solutions
- Identify cost-effective compute and database services
- Design cost-optimized network architectures

## 6. AWS services and features

### 6.1 Analytics

#### 6.1.1 <span id="1">Amazon Athena</span>

- [Amazon Athena](https://docs.aws.amazon.com/athena/latest/ug/what-is.html) is an interactive query service that makes it easy to analyze data directly in Amazon S3 using standard SQL.

#### 6.1.2 <span id="2">AWS Data Exchange</span>

- [AWS Data Exchange](https://docs.aws.amazon.com/data-exchange/latest/userguide/what-is.html) is a service that makes it easy for AWS customers to find, subscribe to, and use third-party data in the AWS Cloud.

#### 6.1.3 <span id="3">AWS Data Pipeline</span>

- .

#### 6.1.4 <span id="4">Amazon EMR</span>

#### 6.1.5 <span id="5">AWS Glue</span>

#### 6.1.6 <span id="6">Amazon Kinesis</span>

- Amazon Kinesis cost-effectively processes and analyzes streaming data at any scale as a fully managed service. With Kinesis, you can ingest real-time data, such as video, audio, application logs, website clickstreams, and IoT telemetry data, for machine learning (ML), analytics, and other applications.

#### 6.1.7 <span id="7">AWS Lake Formation</span>

#### 6.1.8 <span id="8">Amazon Managed Streaming for Apache Kafka (Amazon MSK)</span>

#### 6.1.9 <span id="9">Amazon OpenSearch Service (Amazon Elasticsearch Service)</span>

#### 6.1.10 <span id="10">Amazon QuickSight</span>

#### 6.1.11 <span id="11">Amazon Redshift</span>

### 6.2 Application Integration

#### 6.2.1 <span id="12">Amazon AppFlow</span>

- [Amazon AppFlow](https://docs.aws.amazon.com/appflow/latest/userguide/what-is-appflow.html) is a fully-managed integration service that enables you to securely exchange data between software as a service (SaaS) applications, such as Salesforce, and AWS services, such as Amazon Simple Storage Service (Amazon S3) and Amazon Redshift.

#### 6.2.2 <span id="13">AWS AppSync</span>

- [Aws AppSync](https://docs.aws.amazon.com/appsync/latest/devguide/what-is-appsync.html) provides a robust, scalable GraphQL interface for application developers to combine data from multiple sources, including Amazon DynamoDB, AWS Lambda, and HTTP APIs.

#### 6.2.3 <span id="14">Amazon EventBridge (Amazon CloudWatch Events)</span>

- [Amazon EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html) is a serverless service that uses events to connect application components together, making it easier for you to build scalable event-driven applications.

#### 6.2.4 <span id="15">Amazon MQ</span>

- [Amazon MQ](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/welcome.html) is a managed message broker service that makes it easy to migrate to a message broker in the cloud.

#### 6.2.5 <span id="16">Amazon Simple Notification Service (Amazon SNS)</span>

- A channel for messages to be delivered.
- A publish/subscribe service
- Using Amazon SNS topics, a publisher publishes messages to subscribers. This is similar to the coffee shop; the cashier provides coffee orders to the barista who makes the drinks.
- In Amazon SNS, subscribers can be
  - web servers
  - email addresses
  - AWS Lambda functions, etc.
- How it works:
    1. Publish updates from a single topic
    2. Publish updates from multiple topics
        - Instead of having a single newsletter for all topics, it has broken it up into three separate newsletters.
        - Each newsletter is devoted to a specific topic.

#### 6.2.6 <span id="17">Amazon Simple Queue Service (Amazon SQS)</span>

- Messages are placed until they are processed.
- You can send, store, and receive messages between software components, without losing messages or requiring other services to be available.
- In Amazon SQS, an application sends messages into a queue. A user or service retrieves a message from the queue, processes it, and then deletes it from the queue.
- SQS allows to
  - send messages
  - store messages
  - receive messages
  - between software components
  - at any volume
- How it works:
    1. Fullfiling an order:
      - Think of the cashier and barista as two separate components.
      - The process runs smoothly unless components are coordinated.
    2. Orders in a queue

- **Amazon SQS standard queues** support a nearly unlimited number of API calls per second. They provide best-effort ordering which ensures that messages are generally delivered in the same order as they're sent.

- **Amazon SQS FIFO queues** have all the capabilities of the standard queues, but are designed to enhance messaging between applications when the order of operations and events is critical, or where duplicates can't be tolerated.

#### 6.2.7 <span id="18">AWS Step Functions</span>

- [Amazon step functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html) is a serverless orchestration service that lets you integrate with AWS Lambda functions and other AWS services to build business-critical applications.

### 6.3 AWS Cost Management

#### 6.3.1 <span id="19">AWS Budgets</span>

#### 6.3.2 <span id="20">AWS Cost and Usage Report</span>

#### 6.3.3 <span id="21">AWS Cost Explorer</span>

#### 6.3.4 <span id="22">Savings Plans</span>

### 6.4 Compute

#### 6.4.1 <span id="23">AWS Batch</span>

#### 6.4.2 <span id="24">Amazon EC2</span>

- [Amazon EC2](https://aws.amazon.com/ec2/) provides secure and resizable compute capacity to support virtually any workload in the cloud as Amazon EC2 instances.
- Payment
  - for running instances, not stopped or terminated instances.
  - for the compute time you use when an instance is running, not when it is stopped or terminated.
  - for server capacity that you need or want.
- **Multitenancy** shares underlying hardware between virtual machines. It is managed by AWS.
- **Hypervisor** is responsible for multitenancy. It isolates instances from each other as they share resources with the host. (the host with multiple other instances)
- Instances are resizable. You can give more memory / more CPU.
- **Vertical scaling** makes instances bigger or smaller.
- You can control the networking aspect of EC2.
- Compute-as-a-Service (CaaS)

##### 6.4.2.1 How EC2 Works

- If you have applications that you want to run in Amazon EC2, you must do the following:
  1. Provision instances (virtual servers)
  2. Upload your code
  3. Continue to manage the instances while your application is running

1. Launch
   - Launch an instance. Select a template with basic configurations for your instance.
   - Configurations:
     - OS
     - Application server/Applications
     - Instance type (specific hardware configuration of your instance)
     - Security settings to control the network traffic that can flow into and out of your instance.
2. Connect
   - Connect to the instance.
   - Your programs and applications have multiple methods to connect directly to the instance and exchange data.
   - Users can also connect to the instance by logging in and accessing the computer desktop.
3. Use
   - You can run commands to install software, add storage, copy and organize files, etc.

##### 6.4.2.2 EC Instance types

- Each instance type is grouped under an instance family and optimized for different tasks.
- When selecting an instance type, consider the specific needs of your workloads and applications.
- EC2 instance families:
  - **General purpose instance (GPI)** provides a balance of computing, memory, and networking resources.
    - i.e. enterprise-level apps, mobile, and game dev environments
    - **A1 instance**
    - **M5 instance**
    - **T3/T3a instance**
    - **Mac instance**
  - **Compute-optimized instance** is ideal for compute-bound applications that benefit from high-performance processors.
    - i.e. processor with high computing power, scientific modelling, complex calculations
    - **C5/C5n instance**
    - **C6/C6g instance**
    - **HPC instance**
  - **Memory-optimized instance** is ideal for processing large datasets in memory.
    - i.e. processing large datasets, big data analytics
    - **R5/R5a/R5n instance**
    - **R6g/R6gn instance**
    - **X1/X1e instance**
    - **High memory instance**
  - **Accelerated computing instance** uses hardware accelerators, or coprocessors, to perform some functions more efficiently than is possible in software running on CPUs.
    - i.e. GPU, FPGA (graphic cards)
    - **P3 instance**
    - **P2 instance**
    - **Inf1 instance**
    - **G3 instance**
    - **G4 instance**
    - **F1 instance**
    - **Trn1 instance**
    - **DL1 instance**
    - **VT1 instance**
  - **Storage optimized instance** is ideal for workloads that require high, sequential read and write access to large datasets on local storage. In computing, the term input/output operations per second (IOPS) is a metric that measures the performance of a storage device. It indicates how many different input or output operations a device can perform in one second. Storage-optimized instances are designed to deliver tens of thousands of low-latency, random IOPS to applications.
    - i.e., data caching, low latency, high speed, data analytics, data warehousing
    - **D2 instance**
    - **H1 instance**
    - **I3/I3en instance**

##### 6.4.2.3 Pricing

###### 6.4.2.3.1 On-demand

- Ideal for short-term, irregular workloads that cannot be interrupted.
- No upfront costs or minimum contracts apply.
- The instances run continuously until you stop them, and you pay for only the computing time you use.
- Sample use cases for _On-Demand Instances_ include developing and testing applications and running applications that have unpredictable usage patterns.
- On-Demand Instances are not recommended for workloads that last a year or longer.

###### 6.4.2.3.2 Saving Plans

- _Amazon EC2 Savings Plans_ enable you to reduce the compute costs by committing to a consistent amount of compute usage for a 1-year or 3-year term.
- Any usage up to the commitment is charged at the discounted _Savings Plan_ rate (for example, $10 an hour). Any usage beyond the commitment is charged at regular _On-Demand_ rates.

###### 6.4.2.3.3 Reserved Instances

- _Reserved Instances_ are a billing discount applied to the use of _On-Demand Instances_ in your account.
- You can purchase _Standard Reserved_ and _Convertible Reserved Instances_ for a 1- or 3-year term, and _Scheduled Reserved Instances_ for a 1-year term.
- At the end of a _Reserved Instance_ term, you can continue using the _Amazon EC2_ instance without interruption. However, you are charged _On-Demand_ rates until you do one of the following:
  - Terminate the instance.
  - Purchase a new _Reserved Instance_ that matches the instance attributes (instance type, Region, tenancy, and platform).

###### 6.4.2.3.4 Spot Instances

- _Spot Instances_ are ideal for workloads with flexible start and end times, or that can withstand interruptions.
- _Spot Instances_ use unused _Amazon EC2_ computing capacity.
- Suppose that you have a background processing job that can start and stop as needed (such as the data processing job for a customer survey). You want to start and stop the processing job without affecting the overall operations of your business. If you make a Spot request and _Amazon EC2_ capacity is available, your Spot Instance launches. However, if you make a Spot request and _Amazon EC2_ capacity is unavailable, the request is not successful until capacity becomes available. The unavailable capacity might delay the launch of your background processing job.
- After you have launched a _Spot Instance_, if capacity is no longer available or demand for _Spot Instances_ increases, your instance may be interrupted. This might not pose any issues for your background processing job. However, in the earlier example of developing and testing applications, you would most likely want to avoid unexpected interruptions. Therefore, choose a different EC2 instance type that is ideal for those tasks.

###### 6.4.2.3.5 Dedicated Hosts

- Dedicated Hosts are physical servers with Amazon EC2 instance capacity that is fully dedicated to your use.
- You can use your existing per-socket, per-core, or per-VM software licenses to help maintain license compliance. You can purchase On-Demand Dedicated Hosts and Dedicated Hosts Reservations. Of all the Amazon EC2 options that were covered, Dedicated Hosts are the most expensive.

##### 6.4.2.4 Messaging and queuing

###### 6.4.2.4.1 Monolithic applications

- Tightly coupled architecture
- In monolithic apps, if a single component fails, other components fail, and possibly the entire application fails.
- Applications are made of multiple components.
- The components communicate with each other to
  - transmit data
  - fulfil requests
  - keep the application running
- The components might include
  - databases
  - servers
  - UI
  - business logic, etc.

###### 6.4.2.4.2 Microservices

- In a microservices approach, application components are loosely coupled.
- If a single component fails, the other components continue to work because they are communicating with each other.
- The loose coupling prevents the entire application from failing.
- When designing applications on AWS, you can take a microservices approach with services and components that fulfil different functions.

##### 6.4.2.5 Directing traffic with elastic load balancing

- _Elastic load balancing_ is the AWS service that automatically distributes incoming application traffic across multiple resources, such as EC2 instances.
- A _load balancer_ acts as a single point of contact for all incoming web traffic to your Auto Scaling group.
- Although Elastic Load Balancing and Amazon EC2 Auto Scaling are separate services, they work together to help ensure that applications running in Amazon EC2 can provide high performance and availability.
  1. Low-demand period
  2. High-demand period

- <span id="129">Scalability</span> involves beginning with only the resources you need and designing your architecture to automatically respond to changing demand by scaling out or in.

##### 6.4.2.6 Amazon EC2 Auto Scaling

- It enables you to automatically add or remove Amazon EC2 instances in response to changing application demand so you maintain a greater sense of application availability.
- Two approaches:
    1. _Dynamic scaling_ responds to changing demand.
    2. _Predictive scaling_ automatically schedules the right number of EC2 instances based on predicted demand.
- To scale faster, you can use dynamic scaling and predictive scaling together.
  - When you create an Auto Scaling group, you can set the _minimum capacity_ which is the number of Amazon EC2 instances that launch immediately after you have created the Auto Scaling group.
  - If you do not specify the desired number of Amazon EC2 instances in an Auto Scaling group, the _desired capacity_ defaults to your minimum capacity.
  - The third configuration that you can set in an Auto Scaling group is the _maximum capacity_.
- Auto Scaling groups can span multiple availability zones.

##### 6.4.2.7 Placement groups

- When you launch a new EC2 instance, the EC2 service attempts to place the instance in such a way that all of your instances are spread out across underlying hardware to minimize correlated failures.
- Depending on the type of workload, you can create a placement group using one of the following placement strategies:
  - A **cluster placement group** is a logical grouping of instances within a single Availability Zone.
  - **Partition placement groups**
  - **Spread placement groups**

#### 6.4.3 <span id="25">AWS Elastic Beanstalk</span>

#### 6.4.4 <span id="26">AWS Outposts</span>

#### 6.4.5 <span id="27">AWS Serverless Application Repository</span>

#### 6.4.6 <span id="28">VMware Cloud on AWS</span>

#### 6.4.7 <span id="29">AWS Wavelength</span>

### 6.5 Containers

- A package for your code
- In AWS, you can also build and run containerized applications.
- Here the host is the instance.

#### 6.5.1 <span id="30">Amazon Elastic Container Registry (Amazon ECR)</span>

#### 6.5.2 <span id="31">Amazon Elastic Container Service (Amazon ECS)</span>

- [Amazon Elastic Container Service](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)  is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications.

#### 6.5.3 <span id="32">Amazon ECS Anywhere</span>

#### 6.5.4 <span id="33">Amazon Elastic Kubernetes Service (Amazon EKS)</span>

#### 6.5.5 <span id="34">Amazon EKS Anywhere</span>

#### 6.5.6 <span id="35">Amazon EKS Distro</span>

### 6.6 Database

#### 6.6.1 <span id="36">Amazon Aurora</span>

#### 6.6.2 <span id="37">Amazon Aurora Serverless</span>

#### 6.6.3 <span id="38">Amazon DocumentDB (with MongoDB compatibility)</span>

#### 6.6.4 <span id="39">Amazon DynamoDB</span>

- [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) is a fully managed, serverless, key-value NoSQL database designed to run high-performance applications at any scale.

#### 6.6.5 <span id="40">Amazon ElastiCache</span>

#### 6.6.6 <span id="41">Amazon Keyspaces (for Apache Cassandra)</span>

#### 6.6.7 <span id="42">Amazon Neptune</span>

#### 6.6.8 <span id="43">Amazon Quantum Ledger Database (Amazon QLDB)</span>

#### 6.6.9 <span id="44">Amazon RDS</span>

#### 6.6.10 <span id="45">Amazon Timestream</span>

### 6.7 Developer Tools

#### 6.7.1 <span id="46">AWS X-Ray</span>

### 6.8 Frontend Web and Mobile

#### 6.8.1 <span id="47">AWS Amplify</span>

#### 6.8.2 <span id="48">Amazon API Gateway</span>

- [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) is an AWS service for creating, publishing, maintaining, monitoring, and securing REST, HTTP, and WebSocket APIs at any scale.
- You choose an API _integration type_ according to the types of integration endpoint you work with and how you want data to pass to and from the integration endpoint.
  - For a **Lambda function**, you can have the Lambda proxy integration, or the Lambda custom integration.
  - For an **HTTP endpoint**, you can have the HTTP proxy integration or the HTTP custom integration.
  - For an **AWS service action**, you have the AWS integration of the non-proxy type only.
  - **Mock integration** is where API Gateway serves as an integration endpoint to respond to a method request.
- API Gateway supports multiple mechanisms for controlling and managing access to your API.
  - **Resource policies** let you create resource-based policies to allow or deny access to your APIs and methods from specified source IP addresses or VPC endpoints.
  - **Standard AWS IAM roles and policies** offer flexible and robust access controls that can be applied to an entire API or individual methods.
  - **IAM tags** can be used together with IAM policies to control access.
  - **Endpoint policies** for interface VPC endpoints allow you to attach IAM resource policies to interface VPC endpoints to improve the security of your private APIs.
  - **Lambda authorizers** are Lambda functions that control access to REST API methods using bearer token authentication—as well as information described by headers, paths, query strings, stage variables, or context variables request parameters.
  - **Amazon Cognito user pools** let you create customizable authentication and authorization solutions for your REST APIs.
  - **Cross-origin resource sharing (CORS)** lets you control how your REST API responds to cross-domain resource requests.
  - **Client-side SSL certificates** can be used to verify that HTTP requests to your backend system are from API Gateway.
  - **AWS WAF** can be used to protect your API Gateway API from common web exploits.

#### 6.8.3 <span id="49">AWS Device Farm</span>

#### 6.8.4 <span id="50">Amazon Pinpoint</span>

### 6.9 Machine Learning

#### 6.9.1 <span id="51">Amazon Comprehend</span>

#### 6.9.2 <span id="52">Amazon Forecast</span>

#### 6.9.3 <span id="53">Amazon Fraud Detector</span>

#### 6.9.4 <span id="54">Amazon Kendra</span>

#### 6.9.5 <span id="55">Amazon Lex</span>

#### 6.9.6 <span id="56">Amazon Polly</span>

#### 6.9.7 <span id="57">Amazon Rekognition</span>

#### 6.9.8 <span id="58">Amazon SageMaker</span>

#### 6.9.9 <span id="59">Amazon Textract</span>

#### 6.9.10 <span id="60">Amazon Transcribe</span>

#### 6.9.11 <span id="61">Amazon Translate</span>

### 6.10 Management and Governance

#### 6.10.1 <span id="62">AWS Auto Scaling</span>

#### 6.10.2 <span id="63">AWS CloudFormation</span>

#### 6.10.3 <span id="64">AWS CloudTrail</span>

- [AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) is an AWS service that helps you enable operational and risk auditing, governance, and compliance of your AWS account.

#### 6.10.4 <span id="65">Amazon CloudWatch</span>

- [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) monitors your AWS resources and the apps you run on AWS in real-time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and apps.

#### 6.10.5 <span id="66">AWS Command Line Interface (AWS CLI)</span>

#### 6.10.6 <span id="67">AWS Compute Optimizer</span>

#### 6.10.7 <span id="68">AWS Config</span>

#### 6.10.8 <span id="69">AWS Control Tower</span>

#### 6.10.9 <span id="70">AWS License Manager</span>

#### 6.10.10 <span id="71">Amazon Managed Grafana</span>

#### 6.10.11 <span id="72">Amazon Managed Service for Prometheus</span>

#### 6.10.12 <span id="73">AWS Management Console</span>

#### 6.10.13 <span id="74">AWS Organizations</span>

#### 6.10.14 <span id="75">AWS Personal Health Dashboard</span>

#### 6.10.15 <span id="76">AWS Proton</span>

#### 6.10.16 <span id="77">AWS Service Catalog</span>

#### 6.10.17 <span id="78">AWS Systems Manager</span>

#### 6.10.18 <span id="79">AWS Trusted Advisor</span>

#### 6.10.19 <span id="80">AWS Well-Architected Tool</span>

### 6.11 Media Services

#### 6.11.1 <span id="81">Amazon Elastic Transcoder</span>

#### 6.11.2 <span id="82">Amazon Kinesis Video Streams</span>

### 6.12 Migration and Transfer

#### 6.12.1 <span id="83">AWS Application Discovery Service</span>

#### 6.12.2 <span id="84">AWS Application Migration Service (CloudEndure Migration)</span>

#### 6.12.3 <span id="85">AWS Database Migration Service (AWS DMS)</span>

#### 6.12.4 <span id="86">AWS DataSync</span>

#### 6.12.5 <span id="87">AWS Migration Hub</span>

#### 6.12.6 <span id="88">AWS Server Migration Service (AWS SMS)</span>

#### 6.12.7 <span id="89">AWS Snow Family</span>

- [AWS Snow Family](https://aws.amazon.com/snow/) is a group of devices that transport data in and out of AWS. Its devices are physical devices.

#### 6.12.8 <span id="90">AWS Transfer Family</span>

### 6.13 Networking and Content Delivery

#### 6.13.1 <span id="91">Amazon CloudFront</span>

- [Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html) is a web service that speeds up distribution of your static and dynamic web content, such as `.html`, `.css`, `.js`, and image files, to your users.

#### 6.13.2 <span id="92">AWS Direct Connect</span>

#### 6.13.3 <span id="93">Elastic Load Balancing (ELB)</span>

- [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html) automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer capacity automatically in response to changes in incoming traffic.

#### 6.13.4 <span id="94">AWS Global Accelerator</span>

#### 6.13.5 <span id="95">AWS PrivateLink</span>

#### 6.13.6 <span id="96">Amazon Route 53</span>

- [Amazon Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html) is a highly available and scalable Domain Name System (DNS) web service. It performs three main functions in any combination.
  - Domain registration
  - DNS routing
  - Health checking
    - When you have more than one resource performing the same function—for example, more than one HTTP server or mail server—you can configure Amazon Route 53 to check the health of your resources and respond to DNS queries using only the healthy resources.
    - You can use Route 53 health checking to configure active-active and active-passive failover configurations.
      - **Active-active failover** is chosen when you want all of your resources to be available the majority of the time. When a resource becomes unavailable, Route 53 can detect that it's unhealthy and stop including it when responding to queries.
      - **Active-passive failover** is chosen when you want a primary resource or group of resources to be available the majority of the time and you want a secondary resource or group of resources to be on standby in case all the primary resources become unavailable. If all the primary resources are unhealthy, Route 53 begins to include only the healthy secondary resources in response to DNS queries.

#### 6.13.7 <span id="97">AWS Transit Gateway</span>

#### 6.13.8 <span id="98">Amazon VPC</span>

#### 6.13.9 <span id="99">AWS VPN</span>

### 6.14 Security, Identity, and Compliance

#### 6.14.1 <span id="100">AWS Artifact</span>

#### 6.14.2 <span id="101">AWS Audit Manager</span>

#### 6.14.3 <span id="102">AWS Certificate Manager (ACM)</span>

#### 6.14.4 <span id="103">AWS CloudHSM</span>

#### 6.14.5 <span id="104">Amazon Cognito</span>

#### 6.14.6 <span id="105">Amazon Detective</span>

#### 6.14.7 <span id="106">AWS Directory Service</span>

#### 6.14.8 <span id="107">AWS Firewall Manager</span>

#### 6.14.9 <span id="108">Amazon GuardDuty</span>

#### 6.14.10 <span id="109">AWS Identity and Access Management (IAM)</span>

- [Amazon IAM](https://aws.amazon.com/iam/) is used to specify who or what can access services and resources in AWS, centrally manage fine-grained permissions, and analyze access to refine permissions across AWS.

#### 6.14.11 <span id="110">Amazon Inspector</span>

#### 6.14.12 <span id="111">AWS Key Management Service (AWS KMS)</span>

#### 6.14.13 <span id="112">Amazon Macie</span>

#### 6.14.14 <span id="113">AWS Network Firewall</span>

#### 6.14.15 <span id="114">AWS Resource Access Manager (AWS RAM)</span>

#### 6.14.16 <span id="115">AWS Secrets Manager</span>

#### 6.14.17 <span id="116">AWS Security Hub</span>

#### 6.14.18 <span id="117">AWS Shield</span>

#### 6.14.19 <span id="118">AWS Single Sign-On</span>

#### 6.14.20 <span id="119">AWS WAF</span>

### 6.15 Serverless

#### 6.15.1 <span id="120">AWS Fargate</span>

- AWS Fargate is a serverless compute engine for containers.
- It works with both Amazon ECS and Amazon EKS.

#### 6.15.2 AWS Lambda

- <span id="121"></span>[AWS Lambda](https://aws.amazon.com/lambda/) is a serverless compute service that runs your code in response to events and automatically manages the underlying compute resources for you. These events may include changes in state or an update, such as a user placing an item in a shopping cart on an e-commerce website. When the trigger is detected, the code is automatically run in a managed environment.
- While using AWS Lambda, you pay only for the computing time that you consume. Charges apply only when your code is running.
- It allows you to upload your code into the Lambda function. You can also run code for virtually any type of application or backend service, all with zero administration.
  - For example, a simple Lambda function might involve automatically resizing uploaded images to the AWS Cloud. In this case, the function triggers when uploading a new image.

### 6.16 Storage

#### 6.16.1 <span id="126">Amazon Simple Storage Service S3 (Amazon S3)</span>

- [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide//Welcome.html) is an object storage service offering industry-leading scalability, data availability, security, and performance.
- Object storage service
  - An object is uniquely identified.
    - data
    - metadata
      - name-value pairs that describe the object
- `S3 buckets` are containers for objects stored in S3.
- Industry-leading
  - Scalability
  - Data availability
  - Security
    - It secures unauthorized access with encryption features and access management tools.
  - Durability
    - It automatically creates and stores copies of all S3 objects.
  - Performance
- It stores and protects data use cases, such as websites, mobile apps, enterprise apps, backup and restore, archive, IoT devices, and big data analytics.
- It can easily make fluctuating demands by automatically scaling storage resources up. No upfront investment. No resource procurement cycles.
- It blocks public access.
- AWS S3 commands automatically perform multipart uploading and downloading based on the file size.
- Uploading files into S3 from the Management Console does not provide any protection from network problems.

#### 6.16.2 <span id="122">AWS Backup</span>

- [AWS Backup](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html) is a fully-managed service that makes it easy to centralize and automate data protection across AWS services, in the cloud, and on-premises.

#### 6.16.3 <span id="123">Amazon Elastic Block Store (Amazon EBS)</span>

- [Amazon EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html) provides block level storage volumes for use with EC2 instances.
- EBS volumes behave like raw, unformatted block devices.
- You can mount these volumes as devices on your instances.
- It scales by changing the volume size or attaching more volumes.

##### 6.16.3.1 Amazon EBS volume types

- They differ in performance characteristics and price.

- **Solid state drive (SSD) volumes** are optimized for transactional workloads involving frequent read/write operations with small I/O size.
- **Hard disk drive (HDD) volumes** are optimized for large streaming workload where the dominant performance attribute is throughput.
- **Previous generation volumes** are suited for workloads with small datasets where data is accessed infrequently and performance is not of primary importance.

#### 6.16.4 <span id="124">Amazon Elastic File System (Amazon EFS)</span>

- [Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html) provides serverless, fully elastic file storage so that you can share file data without provisioning or managing storage capacity and performance.
- It scales automatically.

#### 6.16.5 <span id="125">Amazon FSx</span>

- [Amazon FSx](https://docs.aws.amazon.com/fsx/) makes it easy and cost-effective to launch, run, and scale feature-rich, high-performance file systems in the cloud.

#### 6.16.6 <span id="127">Amazon S3 Glacier</span>

- [Amazon S3 Glacier](https://docs.aws.amazon.com/amazonglacier/latest/dev/introduction.html) is a secure and durable service for low-cost data archiving and long-term backup.

#### 6.16.7 <span id="128">AWS Storage Gateway</span>

- [Amazon Storage Gateway](https://aws.amazon.com/storagegateway/) is a set of hybrid cloud storage services that provide on-premises access to virtually unlimited cloud storage.
  - In the hybrid cloud, some parts of your infrastructure are on the cloud, and the rest is on-premises.
    - It might be preferred for long cloud migrations, security reasons, or compliance requirements.

## 7. How to interact with AWS

- Instead of physically managing infrastructure, you logically manage it, through the AWS Application Programming Interface (AWS API).
- When you create, delete, or change any AWS resource, you will use API calls to AWS to do that.

- **AWS Management Console** is a web application that comprises a broad collection of service consoles for managing AWS resources.
- **The AWS Command Line Interface (AWS CLI)** is an open-source tool that enables you to create and configure AWS services using commands in your command-line shell.
- **Integrated Development Environment (IDE)** is to write, run, debug, and deploy applications on AWS using familiar Integrated Development Environments (IDE).
- **Software Development Kit (SDK)** simplifies coding with language-specific abstracted APIs for AWS services.
  - i.e. [Boto3]() is the AWS SDK for Python

## 8. Resources

1. [Exam guide](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf)
1. [What does a solutions architect do?](https://www.coursera.org/articles/solutions-architect)
1. [Coursera](https://www.coursera.org/learn/aws-certified-solutions-architect-associate/home/week/1)
1. [AWS glossary](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html)
1. [AWS white paper](https://d0.awsstatic.com/whitepapers/aws-overview.pdf)
