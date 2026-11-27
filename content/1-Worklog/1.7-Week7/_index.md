---
title: "Week 7 Worklog"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

# Week 7: System Analysis and Architecture Design

**Duration:** 16/11/2026 – 20/11/2026  
**Status:** Draft requiring daily-log verification

**Accuracy note:** The day-by-day schedule is an editorial allocation based on the proposal and overall progress, **not a verified daily work record**. Reported project capabilities are not proof that every item was completed in this exact week.

## 1. Weekly Objectives

- Separate the system into Edge Processing, Event Synchronization, AWS Backend, and Web Dashboard layers.
- Design the data flow from webcam frames to event metadata and define privacy boundaries.
- Select AWS components: API Gateway, Lambda, DynamoDB, Cognito, S3, CloudFront, CloudWatch, IAM, CloudTrail, and Budgets.
- Specify planned Local Event Buffer, Retry, duplicate-safe event writing, and event-history retrieval.
- Document the proposed architecture and identify components not yet implemented.

## 2. Weekly Work Schedule

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | Analyze the Edge AI data flow and conditions for generating events. | 16/11/2026 | 16/11/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [OpenCV](https://docs.opencv.org/4.x/) |
| Tuesday | Define modules for feature extraction, temporal analysis, event metadata, and buffering. | 17/11/2026 | 17/11/2026 | [Python](https://docs.python.org/3/), [FastAPI](https://fastapi.tiangolo.com/) |
| Wednesday | Design HTTP API → Lambda Writer → DynamoDB metadata ingestion using event_id. | 18/11/2026 | 18/11/2026 | [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html), [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html) |
| Thursday | Design Cognito/JWT authentication, Lambda Reader, and S3/CloudFront Dashboard delivery. | 19/11/2026 | 19/11/2026 | [Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html), [JWT Authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html), [Cloudfront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html) |
| Friday | Review architecture, privacy, IAM, monitoring, and cost-control requirements. | 20/11/2026 | 20/11/2026 | [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html), [Cloudwatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html), [Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) |

## 3. Research Findings and Recorded Progress

### 3.1. Edge–Cloud Architecture Layers

**Edge Device:** webcam → OpenCV → MediaPipe Face Landmarker → EAR/MAR/Head Pose/Gaze extraction → temporal analysis → event metadata. **Synchronization:** a proposed Local Event Buffer and Retry mechanism handles unreliable connectivity. **AWS Backend:** API Gateway → Lambda → DynamoDB. **Web:** the event-history interface is distributed by CloudFront using a private S3 origin.

This represents a **target architecture**, not evidence that every cloud service has been deployed.

### 3.2. Data Flow and Metadata Contract

Video remains on the Edge Device. The proposed synchronization flow uses HTTPS POST to send event metadata rather than raw video. Each event needs a stable `event_id` across retries to identify duplicates, plus an appropriate timestamp, event type, state, and permitted source attributes.

The exact payload schema, validation rules, and user/device authorization policy must be finalized before implementation. Facial imagery and video are excluded from the illustrative payload.

### 3.3. Event Writer and History Storage Design

Amazon API Gateway HTTP API accepts requests; AWS Lambda Event Writer validates payloads and writes to DynamoDB. The proposed design uses **Conditional PutItem** with `event_id` to reduce duplicate records when an event is resent.

Correct behavior depends on the DynamoDB key schema and conditional expression. Tests must include repeated event IDs, invalid payloads, and connection failures.

### 3.4. Authentication and Dashboard Design

Amazon Cognito is proposed for sign-up, sign-in, and JWT issuance. An API Gateway JWT Authorizer protects restricted endpoints, while Lambda Event Reader queries DynamoDB according to the caller's permissions.

The Frontend is planned for a private S3 bucket distributed through CloudFront Origin Access Control (OAC). **JWT authentication alone does not guarantee record-level authorization**; the backend must enforce data access boundaries.

### 3.5. Monitoring, Security, and Cost Controls

Supporting design components include IAM Least Privilege, CloudWatch logs/metrics for API and Lambda, CloudTrail for account activity, and AWS Budgets for cost monitoring. AWS WAF is marked **optional** in the architecture.

An Internet outage should not stop local detection; event buffering and resubmission must still be validated through actual tests.

### 3.6. Week 7 Summary

The output is a documented separation of modules, data flows, and service responsibilities for the Edge–Cloud system. This is **architecture design** reflected in the proposal; buffering, Dashboard, and AWS infrastructure require implementation or verification and must not be reported as deployed solely based on the diagram.

## 4. References

1. [Mediapipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
2. [Opencv](https://docs.opencv.org/4.x/)
3. [Python](https://docs.python.org/3/)
4. [Fastapi](https://fastapi.tiangolo.com/)
5. [Apig](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
6. [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
7. [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html)
8. [Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)

