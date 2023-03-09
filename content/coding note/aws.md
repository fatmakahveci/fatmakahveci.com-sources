---
title: AWS cloud practitioner essentials
description: AWS cloud practitioner essentials
summary: "Updated by Fatma, Mar 09, 2023."
date: 09-03-2023
categories:
  - "Coding"
tags:
  - "aws"
  - "coding"
  - "algorithms"
  - "data structures"
---

![aws](/img/aws.png)

## Cloud computing

- _Cloud computing_ is the on-demand delivery of IT resources over the Internet with pay-as-you-go pricing.
- Instead of buying, owning, and maintaining physical data centers and servers, you can access technology services, such as computing power, storage, and databases, on an as-needed basis from a cloud provider.

### Advantages of cloud computing

1. Trade capital expense for variable expense - pay only when you consume
2. Benefit from massive economies of scale - lower pay-as-you-go prices
3. Stop guessing capacity - access as much or little capacity as you need
4. Increase speed and agility - a click away IT resources
5. Stop spending money to run and maintain data centers - focus on projects, not the infrastructure
6. Go global in minutes - low latency with easily deployed application in multiple regions

### Types of cloud computing

1. **Infrastructure-as-a-Service (IaaS)** provides access to networking features, computers, and data storage space. It provides you with the highest level of flexibility and management control over your IT resources.
2. **Platform-as-a-Service (PaaS)** removes the need for management the underlying infrastructure (usually hardware and OS). You don't need to worry about resource procurement, capacity planning, software maintenance, patching, etc.
3. **Software-as-a-Service (SaaS)** provides a completed product that is run and managed by the service provider. i.e., web-based email which you can use to send and receive email without having to manage feature additions or maintain the servers and OS.

### Cloud computing deployment models

- Factors to be considered for selecting a cloud strategy:
  - Required cloud application components
  - Preferred resource management tools
  - Any legacy IT infrastructure requirements.

#### 1. Cloud-based deployment

- Run all parts of the application in the cloud.
- Migrate existing applications to the cloud.
- Design and build new applications in the cloud.

#### 2. On-premises deployment

- Private cloud deployment
- Deploy resources by using virtualization and resource management tools.
- Increase resource utilization by using application management and virtualization technologies.

#### 3. Hybrid deployment

- Connect cloud-based resources to on-premises infrastructure.
- Integrate cloud-based resources with legacy IT applications.

## Serverless computing

- _Serverless_ means that your code runs on servers, but you do not need to provision or manage these servers.
- It gives the flexibility to scale serverless applications automatically.
- Serverless computing can adjust the applications' capacity by modifying the units of consumptions, such as throughput and memory.
- You cannot see or access the underlying infrastructure or instances.

---

## Module 1: Introduction to Amazon Web Services

### 1.1. Purposes of the module

- Summarize the benefits of AWS
- Describe differences between on-demand delivery and cloud deployments
- Summarize the pay-as-you-go pricing model (Key value: Pay for what you need.)

### 1.2. A client-server model

- Most of the modern computing uses a basic client-server model.
- A client can be a web browser or desktop application that a person interacts with to make requests to computer servers.
- A server can be services such as Amazon Elastic Compute Cloud (Amazon EC2), a type of virtual server. It evaluates the details of a request and fulfills it by returning the information to the client.

---

## Module 2: Compute in the Cloud

### 2.1. Purposes of the module

- Describe the benefits of Amazon Elastic Compute Cloud (Amazon EC2) at a basic level
- Identify the different Amazon EC2 instance types
- Differentiate between the various billing options for Amazon EC2
- Describe the benefits of Amazon EC2 Auto Scaling
- Summarize the benefits of Elastic Load Balancing
- Give an example of the uses for Elastic Load Balancing
- Summarize the differences between Amazon Simple Notification Service (Amazon SNS) and Amazon Simple Queue Services (Amazon SQS)
- Summarize additional AWS compute options

### 2.2. Amazon Elastic Compute Cloud (Amazon EC2)

- A web service that provides secure and resizable compute capacity to support virtually any workload in the cloud as Amazon EC2 instances.
- Payment
  - for running instances, not stopped or terminated instances.
  - for the compute time you use when an instance is running, not when it is stopped or terminated.
  - for server capacity that you need or want.
- **Multitenancy** shares underlying hardware between virtual machines. It is managed by AWS.
- **Hypervisor** is responsible for multitenancy. It isolates instances from each other as they share resources from the host. (the host with multiple other instances)
- Instances are resizable. You can give more memory / more CPU.
- **Vertical scaling** makes instances bigger or smaller.
- You can control the networking aspect of EC2.
- Compute-as-a-Service (CaaS)

#### 2.2.1. How EC2 Works

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

#### 2.2.2. EC Instance types

- Each instance type is grouped under an instance family and optimized for different tasks.
- When selecting an instance type, consider the specific needs of your workloads and applications.
- EC2 instance families:
  - General purpose
    - It provides a balance of compute, memory, and networking resources.
  - Compute optimized
    - It is ideal for compute-bound applications that benefit from high-performance processors.
    - i.e., high-performance web servers, compute-intensive applications servers, and dedicated gaming servers.
  - Memory optimized
    - It is ideal for processing large datasets in memory.
    - i.e., In case that you have a workload that requires large amounts of data to be preloaded before running an application.
  - Accelerated computing
    - It uses hardware accelerators, or coprocessors, to perform some functions more efficiently than is possible in software running on CPUs.
    - i.e., floating-point number calculations, graphics processing, and data pattern matching.
  - Storage optimized
    - It is ideal for workloads that require high, sequential read and write access to large datasets on local storage.
    - In computing, the term input/output operations per second (IOPS) is a metric that measures the performance of a storage device. It indicates how many different input or output operations a device can perform in one second. Storage optimized instances are designed to deliver tens of thousands of low-latency, random IOPS to applications.
    - i.e., distributed file systems, data warehousing applications, and high-frequency online transaction processing (OLTP) systems.

#### 2.2.3. Pricing

##### 2.2.3.1. On-demand

- Ideal for short-term, irregular workloads that cannot be interrupted.
- No upfront costs or minimum contracts apply.
- The instances run continuously until you stop them, and you pay for only the compute time you use.
- Sample use cases for _On-Demand Instances_ include developing and testing applications and running applications that have unpredictable usage patterns.
- On-Demand Instances are not recommended for workloads that last a year or longer.

##### 2.2.3.2. Saving Plans

- _Amazon EC2 Savings Plans_ enable you to reduce your compute costs by committing to a consistent amount of compute usage for a 1-year or 3-year term.
- Any usage up to the commitment is charged at the discounted _Savings Plan_ rate (for example, $10 an hour). Any usage beyond the commitment is charged at regular _On-Demand_ rates.

##### 2.2.3.3. Reserved Instances

- _Reserved Instances_ are a billing discount applied to the use of _On-Demand Instances_ in your account.
- You can purchase _Standard Reserved_ and _Convertible Reserved Instances_ for a 1- or 3-year term, and _Scheduled Reserved Instances_ for a 1-year term.
- At the end of a _Reserved Instance_ term, you can continue using the _Amazon EC2_ instance without interruption. However, you are charged _On-Demand_ rates until you do one of the following:
  - Terminate the instance.
  - Purchase a new _Reserved Instance_ that matches the instance attributes (instance type, Region, tenancy, and platform).

##### 2.2.3.4. Spot Instances

- _Spot Instances_ are ideal for workloads with flexible start and end times, or that can withstand interruptions.
- _Spot Instances_ use unused _Amazon EC2_ computing capacity.
- Suppose that you have a background processing job that can start and stop as needed (such as the data processing job for a customer survey). You want to start and stop the processing job without affecting the overall operations of your business. If you make a Spot request and _Amazon EC2_ capacity is available, your Spot Instance launches. However, if you make a Spot request and _Amazon EC2_ capacity is unavailable, the request is not successful until capacity becomes available. The unavailable capacity might delay the launch of your background processing job.
- After you have launched a _Spot Instance_, if capacity is no longer available or demand for _Spot Instances_ increases, your instance may be interrupted. This might not pose any issues for your background processing job. However, in the earlier example of developing and testing applications, you would most likely want to avoid unexpected interruptions. Therefore, choose a different EC2 instance type that is ideal for those tasks.

##### 2.2.3.5. Dedicated Hosts

- Dedicated Hosts are physical servers with Amazon EC2 instance capacity that is fully dedicated to your use.
- You can use your existing per-socket, per-core, or per-VM software licenses to help maintain license compliance. You can purchase On-Demand Dedicated Hosts and Dedicated Hosts Reservations. Of all the Amazon EC2 options that were covered, Dedicated Hosts are the most expensive.

#### 2.2.4. Scaling EC2

- _Scalability_ involves beginning with only the resources you need and designing your architecture to automatically respond to changing demand by scaling out or in.

##### 2.2.4.1. Amazon EC2 Auto Scaling

- It enables you to automatically add or remove Amazon EC2 instances in response to changing application demand so you maintain a greater sense of application availability.
- Two approaches:
    1. _Dynamic scaling_ responds to changing demand.
    2. _Predictive scaling_ automatically schedules the right number of EC2 instances based on predicted demand.
- To scale faster, you can use dynamic scaling and predictive scaling together.
  - When you create an Auto Scaling group, you can set the _minimum capacity_ which is the number of Amazon EC2 instances that launch immediately after you have created the Auto Scaling group.
  - If you do not specify the desired number of Amazon EC2 instances in an Auto Scaling group, the _desired capacity_ defaults to your minimum capacity.
  - The third configuration that you can set in an Auto Scaling group is the _maximum capacity_.

## Messaging and queuing

### Monolithic applications

- Tightly coupled architecture
- In monolithic apps, if a single component fails, other components fail, and possibly the entire application fails.
- Applications are made of multiple components.
- The components communicate with each other to
  - transmit data
  - fulfill requests
  - keep the application running
- The components might include
  - databases
  - servers
  - UI
  - business logic, etc.

### Microservices

- In a microservices approach, application components are loosely coupled.
- If a single component fails, the other components continue to work because they are communicating with each other.
- The loose coupling prevents the entire application from failing.
- When designing applications on AWS, you can take a microservices approach with services and components that fulfill different functions.

### Amazon services facilitate application integration

#### Amazon Simple Notification Service (Amazon SNS)

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

#### Amazon Simple Queue Service (Amazon SQS)

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
      - Think of cashier and barista as two separate components.
      - The process run smoothly unless components are coordinated.
    2. Orders in a queue

## Directing traffic with elastic load balancing

- _Elastic load balancing_ is the AWS service that automatically distributes incoming application traffic across multiple resources, such as EC2 instances.
- A _load balancer_ acts as a single point of contact for all incoming web traffic to your Auto Scaling group.
- Although Elastic Load Balancing and Amazon EC2 Auto Scaling are separate services, they work together to help ensure that applications running in Amazon EC2 can provide high performance and availability.
  1. Low-demand period
  2. High-demand period

### EC2

- If you have applications that you want to run in Amazon EC2, you must do the following:
  1. Provision instances (virtual servers)
  2. Upload your code
  3. Continue to manage the instances while your application is running

### AWS Lambda

- An AWS service for serverless computing is AWS Lambda.
- It allows you to upload your code into lambda function.
- Configure trigger, service waits for the trigger.
- When the trigger is detected, the code is automatically run in a managed environment.
- While using AWS Lambda, you pay only for the compute time that you consume.
- Charges apply only when your code is running.
- You can also run code for virtually any type of application or backend service, all with zero administration.
- For example, a simple Lambda function might involve automatically resizing uploaded images to the AWS Cloud. In this case, the function triggers when uploading a new image.

### Containers

- A package for your code
- In AWS, you can also build and run containerized applications.
- Here the host is the instance.

#### Amazon's container orchestration tools

##### Amazon Elastic Container Service (ECS)

##### Amazon Elastic Kubernetes Service (EKS)

##### Amazon Fargate

- AWS Fargate is a serverless compute engine for containers.
- It works with both Amazon ECS and Amazon EKS.

---

## Module 3: Global Infrastructure and Reliability

### 3.1. Purposes of the module

- Summarize the benefits of the AWS Global Infrastructure
- Describe the basic concept of Availability Zones
- Describe the benefits of Amazon CloudFront and Edge locations
- Compare different methods for provisioning AWS services

---

## Module 4: Networking

### 4.1. Purposes of the module

- Describe the basic concepts of networking
- Describe the difference between public and private networking resources
- Explain a virtual private gateway using a real life scenario
- Explain a virtual private network (VPN) using a real life scenario
- Describe the benefit of AWS Direct Connect
- Describe the benefit of hybrid deployments
- Describe the layers of security used in an IT strategy
- Describe which services are used to interact with the AWS global network

---

## Module 5: Storage and Databases

### 5.1. Purposes of the module

- Summarize the basic concept of storage and databases
- Describe benefits of Amazon Elastic Block Store (Amazon EBS)
- Describe benefits of Amazon Simple Storage Service (Amazon S3)
- Describe the benefits of Amazon Elastic File System (Amazon EFS)
- Summarize various storage solutions
- Describe the benefits of Amazon Relational Database Service (Amazon RDS)
- Describe the benefits of Amazon DynamoDB
- Summarize various database services

## Amazon Simple Storage Service (S3)

- Object storage service
  - An object is uniquely identified.
    - data
    - metadata
      - name-value pairs that describe the object
- `S3 buckets` are containers for objects stored in S3.
- Industry leading
  - Scalability
  - Data availability
  - Security
    - It secures from unauthorized access with
      - Encryption features
      - Access management tools
  - Durability (99.99%)
    - It automatically creates and stores copies of all S3 objects.
  - Performance
- It stores and protects data use cases, such as website, mobile app, enterprise app, backup and restore, archive, IoT devices, and big data analytics.
- It can easily makes fluctuating demands by automatically scales storage resources up. No upfront investment. No resource procurement cycles.
- It blocks public access.

---

## Module 6: Security

### 6.1. Purposes of the module

- Explain the benefits of the shared responsibility model
- Describe multi-factor authentication (MFA)
- Differentiate between the AWS Identity and Access Management (IAM) security levels
- Describe security policies at a basic level
- Explain the benefits of AWS Organizations
- Summarize the benefits of compliance with AWS
- Explain primary AWS security services at a basic level

---

## Module 7: Monitoring and Analytics

### Purposes of the module

- Summarize approaches to monitoring your AWS environment
- Describe the benefits of Amazon CloudWatch
- Describe the benefits of AWS CloudTrail
- Describe the benefits of AWS Trusted Advisor

---

## Module 8: Pricing and Support

### 8.1. Purposes of the module

- Understand AWS pricing and support models
- Describe the AWS Free Tier
- Describe key benefits of AWS Organizations and consolidated billing
- Explain the benefits of AWS Budgets
- Explain the benefits of AWS Cost Explorer
- Explain the primary benefits of the AWS Pricing Calculator
- Distinguish between the various AWS Support Plans
- Describe the benefits of AWS Marketplace

---

## Module 9: Migration and Innovation

### 9.1. Purposes of the module

- Understand migration and innovation in the AWS Cloud
- Summarize the AWS Cloud Adoption Framework (AWS CAF)
- Summarize six key factors of a cloud migration strategy
- Describe the benefits of various AWS data migration solutions, such as AWS Snowcone, AWS Snowball, and AWS Snowmobile
- Summarize the broad scope of innovative solutions that AWS offers

---

## Module 10: The Cloud Journey

### 10.1. Purposes of the module

- Summarize the five pillars of the AWS Well-Architected Framework
- Explain the six benefits of cloud computing

---

## Module 11: AWS Certified Cloud Practitioner Basics

### 11.1. Purposes of the module

- Determine resources for preparing for the AWS Certified Cloud Practitioner examination
- Describe benefits of becoming AWS Certified

---

## How to interact with AWS

- Instead of physically managing infrastructure, you logically manage it, through the AWS Application Programming Interface (AWS API).
- When you create, delete, or change any AWS resource, you will use API calls to AWS to do that.

- **AWS Management Console** is a web application that comprises a broad collection of service consoles for managing AWS resources.
- **The AWS Command Line Interface (AWS CLI)** is an open source tool that enables you to create and configure AWS services using commands in your command-line shell.
- **Integrated Development Environment (IDE)** is to write, run, debug, and deploy applications on AWS using familiar Integrated Development Environments (IDE).
- **Software Development Kit (SDK)** simplifies coding with language-specific abstracted APIs for AWS services.

---

## References

1. [AWS glossary](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html)
2. [AWS white paper](https://d0.awsstatic.com/whitepapers/aws-overview.pdf)
