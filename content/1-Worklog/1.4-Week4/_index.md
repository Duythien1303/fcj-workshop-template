---
title: "Week 4 Worklog"
date: 2026-10-26
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---


### Objectives for Week 4

- Understand the fundamentals of Serverless Computing and its role in application development on Amazon Web Services (AWS).
- Gain foundational knowledge of AWS Lambda and how it enables developers to run code without directly managing servers.
- Explore important AWS Lambda components, including Functions, Runtimes, Triggers, Events, and Execution Roles.
- Understand Amazon API Gateway and how APIs enable communication between client applications and backend services.
- Study Amazon CloudWatch for application monitoring, log collection, and performance analysis.
- Explore how AWS Identity and Access Management (IAM) controls access permissions between AWS services.
- Become familiar with the process of designing, deploying, and testing a basic Serverless application.
- Build foundational knowledge of application deployment to support the development of the final internship project.

### Tasks to Be Completed This Week

| Day | Tasks | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | - Study the fundamentals of Serverless Computing and the characteristics of serverless architectures. <br> - Compare Serverless Computing with traditional application deployment models. <br> - Explore AWS Lambda and its common use cases. <br> - Understand Functions, Runtimes, Events, and Triggers. | 26/10/2026 | 26/10/2026 | [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Tuesday | - Study the architecture and execution process of AWS Lambda. <br> - Learn about Lambda Execution Roles and AWS IAM permissions. <br> - Explore event processing and function invocation in AWS Lambda. <br> - Study how to create and test Lambda Functions using Python. <br> - Practice with an authorized AWS environment if available. | 27/10/2026 | 27/10/2026 | [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) |
| Wednesday | - Explore Amazon API Gateway and the role of APIs in software systems. <br> - Study REST APIs, HTTP Methods, and HTTP Status Codes. <br> - Understand how API Gateway integrates with AWS Lambda. <br> - Learn how HTTP Requests are processed and HTTP Responses are returned. <br> - Explore the design of a simple Serverless REST API. | 28/10/2026 | 28/10/2026 | [Amazon API Gateway Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Thursday | - Study Amazon CloudWatch and its application monitoring capabilities. <br> - Explore CloudWatch Logs, Metrics, and Alarms. <br> - Learn how to monitor Lambda execution duration, invocations, and errors. <br> - Understand how CloudWatch Logs support debugging and troubleshooting. <br> - Research security and cost management principles for Serverless applications. | 29/10/2026 | 29/10/2026 | [Amazon CloudWatch Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) |
| Friday | - Review AWS Lambda, API Gateway, and CloudWatch. <br> - Design a basic Serverless application architecture diagram. <br> - Explore the integration process between Lambda and API Gateway. <br> - Develop or simulate a simple API to examine HTTP Request and Response processing. <br> - Summarize Week 4 and prepare to study Generative AI on AWS in Week 5. | 30/10/2026 | 30/10/2026 | [AWS Serverless](https://aws.amazon.com/serverless/) <br> [AWS Workshops](https://catalog.workshops.aws/) |

### Achievements in Week 4

#### 1. General Knowledge of Serverless Computing

- Developed an understanding of Serverless Computing and its role in modern application development.
- Learned that Serverless Computing enables developers to focus on application code without directly managing the underlying server infrastructure.
- Explored the main characteristics of serverless architectures:

  - **Automatic Scaling:** Computing resources can automatically adapt to changing application workloads.
  - **Event-Driven Architecture:** Functions can be invoked in response to specific events.
  - **Managed Infrastructure:** The cloud provider manages many infrastructure components.
  - **Pay-per-use:** Pricing depends on the resource consumption and billing model of each service.

- Understood the differences between serverless architectures and traditional application deployment models.
- Identified common serverless use cases, including API processing, data processing, and workflow automation.

#### 2. Knowledge of AWS Lambda

- Understood AWS Lambda as a serverless computing service that executes code in response to events.
- Learned about the fundamental components of AWS Lambda:

  - **Lambda Function:** A unit of application code deployed and executed through AWS Lambda.
  - **Runtime:** The execution environment supporting compatible programming languages and versions.
  - **Event:** Input data provided when a Lambda Function is invoked.
  - **Trigger:** A component or service that initiates function execution.
  - **Execution Role:** An IAM Role granting a Lambda Function the permissions required to access AWS resources.

- Studied the basic AWS Lambda execution process:

  1. An event or request invokes a Lambda Function.
  2. AWS Lambda receives the request and prepares an execution environment when necessary.
  3. The function processes input data using the deployed application code.
  4. The processing result is returned or delivered to another component.
  5. Execution information may be recorded for monitoring and troubleshooting.

- Recognized the role of AWS Lambda in developing backend services for modern applications.
- Became familiar with the structure of a Python-based Lambda Function.

#### 3. Knowledge of Amazon API Gateway

- Learned that Amazon API Gateway is a managed service for creating, publishing, maintaining, monitoring, and securing APIs.
- Understood the role of API Gateway in connecting client applications with backend services.
- Studied fundamental API concepts:

  - **REST API:** An API based on REST architectural principles, commonly using HTTP for communication.
  - **API Endpoint:** A URL through which clients can access an API.
  - **HTTP Request:** A message sent by a client to request an operation or resource.
  - **HTTP Response:** A message returned after processing a request.
  - **HTTP Methods:** Common methods such as GET, POST, PUT, and DELETE.
  - **HTTP Status Codes:** Response codes indicating request outcomes, such as 200, 400, 404, and 500.

- Explored the integration between Amazon API Gateway and AWS Lambda.
- Understood how API Gateway receives HTTP requests and invokes Lambda Functions to process them.
- Studied the process of developing simple APIs for web and mobile applications.

#### 4. Knowledge of Amazon CloudWatch

- Understood Amazon CloudWatch and its role in monitoring AWS applications, resources, and services.
- Explored its major components:

  - **CloudWatch Logs:** Collects, stores, and supports the analysis of application and service logs.
  - **CloudWatch Metrics:** Provides measurements for monitoring system activity and performance.
  - **CloudWatch Alarms:** Monitors metrics and performs configured actions when alarm conditions are met.
  - **CloudWatch Dashboards:** Provides visual representations of monitoring data.

- Studied important AWS Lambda metrics:

  - **Invocations:** The number of times a Lambda Function is invoked.
  - **Duration:** The time taken to execute a function.
  - **Errors:** The number of function invocations that result in errors.
  - **Throttles:** The number of invocation requests rejected due to concurrency or other execution limits.

- Understood how CloudWatch supports issue detection, performance monitoring, and application troubleshooting.

#### 5. Knowledge of IAM and Serverless Security

- Explored the role of AWS Identity and Access Management (IAM) in controlling access permissions between AWS services.
- Understood how Lambda Execution Roles determine which AWS resources a function can access.
- Studied the **Principle of Least Privilege** when assigning permissions to serverless applications.
- Recognized the importance of:

  - Granting functions only the permissions necessary to perform their tasks.
  - Protecting credentials and sensitive information.
  - Controlling access to APIs.
  - Monitoring application activities through logs.
  - Tracking resource consumption and service costs.

#### 6. Understanding the Serverless Application Development Process

- Studied a basic serverless architecture involving Amazon API Gateway, AWS Lambda, and Amazon CloudWatch.
- Understood the application request-processing workflow:

  1. A client sends an HTTP Request to an API Endpoint.
  2. Amazon API Gateway receives and routes the request.
  3. API Gateway invokes the integrated Lambda Function.
  4. The Lambda Function processes the request data.
  5. The processing result is returned to API Gateway.
  6. API Gateway sends an HTTP Response to the client.
  7. Execution information is recorded by monitoring services when logging is appropriately configured.

- Identified the components required to develop a simple REST API.
- Became familiar with API testing using HTTP request tools.
- Recognized the importance of result validation, error handling, and log monitoring during application development.

#### 7. Comparison of AWS Serverless and Monitoring Services

| Service | Main Function | Role in an Application |
|---|---|---|
| **AWS Lambda** | Serverless code execution | Processes backend application logic |
| **Amazon API Gateway** | API creation and management | Receives and routes client requests |
| **Amazon CloudWatch** | Application and resource monitoring | Collects metrics, logs, and alerts |
| **AWS IAM** | Identity and access management | Controls permissions between AWS services and resources |

Through studying these services, I developed a clearer understanding of how different AWS components work together to create backend applications without directly managing servers.

#### 8. Week 4 Summary

During the fourth week of my internship, the main focus was on **Serverless Computing** and AWS services used to develop, deploy, and monitor cloud-based applications.

By studying AWS Lambda, I gained a better understanding of event-driven code execution and the benefits of managed computing services.

Exploring Amazon API Gateway helped me understand how client applications communicate with backend services through HTTP-based APIs.

In addition, studying Amazon CloudWatch and AWS IAM highlighted the importance of monitoring, troubleshooting, security, and access management in cloud application development.

Beyond theoretical knowledge, exploring the integration between API Gateway and Lambda provided a clearer understanding of the process of designing, developing, and testing a basic Serverless application.

The knowledge acquired during Week 4 will provide a foundation for studying **Generative AI, Large Language Models (LLMs), AI Agents, and Amazon Bedrock** in Week 5, while preparing for the research and development phase of my final internship project.
