---
title: "Week 3 Worklog"
date: 2026-10-05
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---



### Objectives for Week 3

- Gain an overview of data storage and management methods on Amazon Web Services (AWS).
- Understand the differences between three common storage models: Object Storage, Block Storage, and File Storage.
- Explore AWS storage services, including Amazon Simple Storage Service (Amazon S3), Amazon Elastic Block Store (Amazon EBS), and Amazon Elastic File System (Amazon EFS).
- Understand the fundamentals of relational databases and non-relational (NoSQL) databases.
- Study Amazon Relational Database Service (Amazon RDS) and Amazon DynamoDB.
- Explore data protection, access control, and backup methods on AWS.
- Become familiar with data management through the AWS Management Console.
- Build foundational knowledge of Storage and Database services to support Cloud and AI applications in the following weeks.

### Tasks to Be Completed This Week

| Day | Tasks | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | - Explore Storage in Cloud Computing. <br> - Differentiate between Object Storage, Block Storage, and File Storage. <br> - Study Amazon S3 and the concepts of Buckets, Objects, Keys, and Storage Classes. <br> - Explore real-world use cases of Amazon S3. | 05/10/2026 | 05/10/2026 | [Amazon S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html) |
| Tuesday | - Study Amazon S3 features. <br> - Explore S3 Versioning, Lifecycle Rules, and Bucket Policies. <br> - Research access management and data protection methods in Amazon S3. <br> - Learn how to create S3 Buckets and upload, download, and manage Objects. <br> - Practice basic S3 operations if an authorized AWS environment is available. | 06/10/2026 | 06/10/2026 | [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) |
| Wednesday | - Study Amazon Elastic Block Store (EBS) and its role in Amazon EC2. <br> - Explore EBS Volumes, Snapshots, and commonly used EBS Volume types. <br> - Learn about Amazon Elastic File System (EFS). <br> - Compare Amazon S3, EBS, and EFS in terms of storage methods, capabilities, and use cases. | 07/10/2026 | 07/10/2026 | [Amazon EBS](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html) <br> [Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html) |
| Thursday | - Explore Database services in Cloud Computing. <br> - Differentiate between Relational Databases and NoSQL Databases. <br> - Study Amazon RDS, supported database engines, and basic management features. <br> - Explore Amazon DynamoDB and the NoSQL data model. <br> - Compare Amazon RDS and DynamoDB in terms of data structure, scalability, and use cases. | 08/10/2026 | 08/10/2026 | [Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) <br> [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Friday | - Review AWS Storage and Database services studied during the week. <br> - Explore data backup and recovery methods, including S3 Versioning, EBS Snapshots, and RDS Backups. <br> - Study data security principles and access management. <br> - Create a comparison table of Amazon S3, EBS, EFS, RDS, and DynamoDB. <br> - Summarize Week 3 and prepare to study AWS Serverless services in Week 4. | 09/10/2026 | 09/10/2026 | [AWS Documentation](https://docs.aws.amazon.com/) |

### Achievements in Week 3

#### 1. General Knowledge of Cloud Storage

- Developed an understanding of the role of storage services in managing and processing data in cloud computing environments.
- Learned to distinguish between three fundamental storage models:

  - **Object Storage:** Stores data as objects and is suitable for images, videos, documents, unstructured data, and applications requiring scalability.

  - **Block Storage:** Stores data in blocks and is commonly used as disk storage for servers and systems requiring block-level access.

  - **File Storage:** Organizes data into files and directories, supporting data access and sharing across multiple systems.

- Understood the fundamental characteristics of each storage model and their appropriate use cases.

#### 2. Knowledge of Amazon Simple Storage Service (Amazon S3)

- Understood the concept of Amazon S3 and its role as an object storage service.
- Explored the fundamental components of Amazon S3:

  - **Bucket:** A container used to store objects.

  - **Object:** The fundamental unit of data stored in Amazon S3.

  - **Object Key:** A unique identifier for an object within a bucket.

  - **Storage Class:** A storage option designed for specific data access patterns and cost requirements.

- Studied important Amazon S3 features:

  - **S3 Versioning:** Maintains multiple versions of objects to support data recovery and management.

  - **S3 Lifecycle Rules:** Automatically transitions or expires objects based on configured rules.

  - **Bucket Policies:** Define access permissions for resources stored in S3 buckets.

  - **S3 Encryption:** Protects stored data using encryption mechanisms.

- Understood the basic process of creating buckets, uploading and downloading files, and managing objects through the AWS Management Console.
- Recognized the importance of configuring appropriate access permissions and preventing unnecessary public access to stored data.

#### 3. Knowledge of Amazon EBS and Amazon EFS

**Amazon Elastic Block Store (EBS)**

- Learned that Amazon EBS provides block storage commonly used with Amazon EC2.
- Understood the following concepts:

  - **EBS Volume:** A block-level storage device that can be attached to a compatible EC2 instance.

  - **EBS Snapshot:** A backup of an EBS volume that supports data protection and recovery.

  - **Volume Types:** Different storage options optimized for specific performance and cost requirements.

- Understood the role of EBS in providing persistent storage for applications running on EC2 instances.

**Amazon Elastic File System (EFS)**

- Understood Amazon EFS as a managed file storage service on AWS.
- Explored its capability to share file data across multiple compatible computing resources.
- Learned about common use cases involving applications that require a shared file system.

#### 4. Knowledge of Amazon RDS

- Understood the fundamentals of relational databases and how data is organized into tables.
- Learned about Amazon Relational Database Service (RDS) and its role in simplifying the deployment and management of relational databases on AWS.
- Explored several database engines supported by Amazon RDS:

  - MySQL.
  - PostgreSQL.
  - MariaDB.
  - Microsoft SQL Server.
  - Oracle Database.

- Studied important Amazon RDS features:

  - **Automated Backups:** Automatically creates database backups according to the configured retention settings.

  - **Multi-AZ Deployment:** Improves database availability and supports recovery from infrastructure failures.

  - **Read Replicas:** Helps scale read workloads for supported database engines and configurations.

  - **Monitoring:** Provides metrics for observing database performance and operational health.

- Recognized the importance of relational databases in applications that require structured data management and data consistency.

#### 5. Knowledge of Amazon DynamoDB

- Learned that Amazon DynamoDB is a fully managed NoSQL database service provided by AWS.
- Understood fundamental DynamoDB concepts:

  - **Table:** A collection of stored data items.

  - **Item:** An individual data record within a table.

  - **Attribute:** A data element describing an item.

  - **Primary Key:** A key used to uniquely identify each item within a table.

- Explored the role of DynamoDB in applications requiring low latency and high scalability.
- Understood the main differences between Amazon RDS and DynamoDB:

  - **Amazon RDS:** Suitable for relational data models and applications requiring SQL queries.

  - **Amazon DynamoDB:** Suitable for NoSQL applications requiring high scalability and fast access based on predefined query patterns.

#### 6. Knowledge of Data Security and Backup

- Explored the importance of data security in cloud computing environments.
- Studied fundamental data protection methods:

  - **Encryption:** Protects data during storage and transmission.

  - **Access Control:** Restricts access to authorized users and services.

  - **Backup:** Creates recoverable copies of data to support disaster recovery.

  - **Versioning:** Maintains historical versions of stored data to support recovery when necessary.

- Understood the role of AWS IAM in controlling access to Storage and Database services.
- Recognized the importance of choosing appropriate storage, backup, and recovery methods based on application requirements.

#### 7. Comparison of AWS Storage and Database Services

| Service | Service Type | Primary Use Cases |
|---|---|---|
| **Amazon S3** | Object Storage | Storing images, videos, documents, backups, and unstructured data |
| **Amazon EBS** | Block Storage | Providing persistent disk storage for Amazon EC2 |
| **Amazon EFS** | File Storage | Providing shared file systems for compatible computing resources |
| **Amazon RDS** | Relational Database | Managing relational data and SQL-based applications |
| **Amazon DynamoDB** | NoSQL Database | Storing and retrieving NoSQL data with high scalability |

By comparing these services, I developed a better understanding of how different AWS storage and database solutions address different technical requirements.

Selecting an appropriate service depends on factors such as data structure, access patterns, performance, scalability, security, and operational costs.

#### 8. Week 3 Summary

During the third week of my internship, the main focus was on two important categories of Amazon Web Services: **Storage and Database**.

By studying Amazon S3, Amazon EBS, and Amazon EFS, I gained knowledge of common cloud storage models and how to select suitable storage solutions for different application requirements.

In addition, exploring Amazon RDS and Amazon DynamoDB helped me understand the differences between relational and non-relational databases, their fundamental characteristics, and their roles in modern application development.

The week also covered data protection principles, access management, and backup methods, emphasizing the importance of maintaining data security and system recoverability.

The knowledge acquired during Week 3 provides a foundation for exploring how applications are developed, deployed, and managed on AWS, particularly through Serverless services such as AWS Lambda, Amazon API Gateway, and Amazon CloudWatch in the following week.
