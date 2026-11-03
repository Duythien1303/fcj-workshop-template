---
title: "Week 2 Worklog"
date: 2026-09-28
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Objectives for Week 2

- Understand the fundamental concepts of computer networking and the role of networking in Cloud Computing.
- Gain foundational knowledge of Amazon Virtual Private Cloud (Amazon VPC) and how networks are organized within AWS.
- Explore important VPC components, including Subnets, Route Tables, Internet Gateways, and Security Groups.
- Understand the differences between Public Subnets and Private Subnets in AWS network architecture.
- Study network security principles and access management using AWS Identity and Access Management (IAM).
- Become familiar with the process of designing and configuring a basic VPC network.
- Build a foundation in Networking and Security to support the deployment of applications on AWS in the following weeks.

### Tasks to Be Completed This Week

| Day | Tasks | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | - Study the fundamentals of Networking in Cloud Computing. <br> - Research Amazon Virtual Private Cloud (VPC) and its role within AWS. <br> - Learn about IP addresses, CIDR blocks, and basic network segmentation. <br> - Compare traditional networking with cloud-based networking. | 28/09/2026 | 28/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| Tuesday | - Study Amazon VPC network architecture. <br> - Learn about Public Subnets and Private Subnets. <br> - Research Route Tables and traffic routing within a VPC. <br> - Understand Internet Gateways and their role in connecting a VPC to the Internet. | 29/09/2026 | 29/09/2026 | [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) |
| Wednesday | - Explore network security mechanisms on AWS. <br> - Study Security Groups and Network Access Control Lists (NACLs). <br> - Compare Security Groups and NACLs. <br> - Learn about Inbound Rules and Outbound Rules. <br> - Research the principle of Least Privilege in system security. | 30/09/2026 | 30/09/2026 | [VPC Security](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security.html) |
| Thursday | - Study AWS Identity and Access Management (IAM). <br> - Research IAM Users, Groups, Roles, and Policies. <br> - Learn how to manage access permissions for AWS resources. <br> - Understand the fundamentals of authentication and authorization in cloud environments. | 01/10/2026 | 01/10/2026 | [AWS IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| Friday | - Review Amazon VPC, Subnets, Route Tables, and Internet Gateways. <br> - Practice designing a basic VPC network architecture diagram. <br> - Explore the steps involved in configuring VPCs and Security Groups through the AWS Management Console. <br> - Review and evaluate the components of the network architecture. <br> - Summarize the knowledge gained during Week 2 and prepare to study AWS Storage & Database in Week 3. | 02/10/2026 | 02/10/2026 | [AWS Workshops](https://catalog.workshops.aws/) |

### Achievements in Week 2

#### 1. Knowledge of AWS Networking

- Understood the role of Networking in connecting and managing resources within a cloud computing environment.
- Gained a foundational understanding of Amazon Virtual Private Cloud (VPC) and its role in creating logically isolated virtual networks on AWS.
- Explored the fundamental components of computer networking:
  - **IP Address:** An address used to identify devices and resources within a network.
  - **CIDR (Classless Inter-Domain Routing):** A method for representing and dividing IP address ranges.
  - **VPC:** A logically isolated virtual network within the AWS environment.
  - **Subnet:** A subdivision of an IP address range within a VPC.

#### 2. Knowledge of Amazon VPC Architecture

- Explored the structure of Amazon VPC and how its networking components work together.
- Learned to distinguish between different subnet types:
  - **Public Subnet:** A subnet with a route to an Internet Gateway, allowing appropriately configured resources to communicate directly with the Internet.
  - **Private Subnet:** A subnet that does not have a direct route to an Internet Gateway.
- Understood the functions of important networking components:
  - **Route Table:** Contains routing rules that determine how network traffic is directed.
  - **Internet Gateway:** Enables communication between a VPC and the Internet when routing and security requirements are satisfied.
  - **Network Interface:** A virtual networking component that connects resources to the network.

#### 3. Knowledge of AWS Network Security

- Understood the role of Security Groups in controlling inbound and outbound traffic for AWS resources.
- Learned the differences between Security Groups and Network Access Control Lists:
  - **Security Group:** Operates at the resource or network interface level and is stateful.
  - **Network ACL:** Operates at the subnet level and is stateless.
- Distinguished between two types of traffic rules:
  - **Inbound Rules:** Control incoming network traffic.
  - **Outbound Rules:** Control outgoing network traffic.
- Recognized the importance of restricting network access and allowing only necessary connections.

#### 4. Knowledge of AWS Identity and Access Management

- Understood the role of AWS IAM in managing identities and access permissions for AWS resources.
- Learned to distinguish between the main IAM components:
  - **IAM User:** An identity created within an AWS account.
  - **IAM Group:** A collection of IAM Users used to simplify permission management.
  - **IAM Role:** An identity with a set of permissions that authorized entities can temporarily assume.
  - **IAM Policy:** A document that defines access permissions for AWS resources.
- Understood the **Principle of Least Privilege**, which ensures that users and services receive only the permissions necessary to perform their tasks.
- Recognized the importance of Multi-Factor Authentication (MFA) in strengthening account security.

#### 5. Basic Network Architecture Design Practice

- Studied the process of building a simple Amazon VPC architecture.
- Designed a reference network diagram consisting of:
  - One VPC with a defined CIDR block.
  - One Public Subnet.
  - One Private Subnet.
  - One Internet Gateway.
  - Route Tables for each subnet type.
  - Security Groups to protect resources within the VPC.
- Understood the relationships between networking components when deploying applications on AWS.
- Became familiar with the procedures for configuring and inspecting networking resources through the AWS Management Console.

#### 6. Week 2 Summary

During the second week of the internship, the main focus was on two important areas of Amazon Web Services: **Networking and Security**.

By studying Amazon VPC, Subnets, Route Tables, Internet Gateways, Security Groups, and IAM, I developed a better understanding of how virtual networks are organized, how network connections are managed, and how access permissions are controlled within cloud environments.

In addition to theoretical knowledge, exploring the process of designing a basic network architecture helped me understand the relationships between networking components and the key considerations involved in developing secure cloud-based systems.

The knowledge acquired during Week 2 provides an important foundation for exploring AWS Storage and Database services, including Amazon S3, Amazon EBS, and Amazon RDS, in the following week.
