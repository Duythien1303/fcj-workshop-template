---
title: "Week 9 Worklog"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

# Week 9: System Integration and Testing

**Duration:** 16/11/2026 – 20/11/2026  
**Status:** Planned work


## 1. Weekly Objectives

- Complete the link between Edge analysis output and event metadata structure.
- Prototype a Local Event Buffer/Retry mechanism if time and scope permit, including connectivity failures.
- Design and test event ingestion, authorization, duplicate-safe storage, and history retrieval in an authorized AWS environment.
- Standardize Backend tests for images, videos, and uncertain states.
- Capture actual evidence and separate implemented functionality from design-only elements.

## 2. Weekly Work Schedule

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | Define event_id, timestamp, event type, and state in a consistent metadata schema. | 16/11/2026 | 16/11/2026 | [Python](https://docs.python.org/3/), [FastAPI](https://fastapi.tiangolo.com/) |
| Tuesday | Prototype or simulate Local Event Buffer and retry after failed submissions. | 17/11/2026 | 17/11/2026 | [Python](https://docs.python.org/3/), [pytest](https://docs.pytest.org/en/stable/) |
| Wednesday | Test API Gateway → Lambda Event Writer → DynamoDB if AWS access is available. | 18/11/2026 | 18/11/2026 | [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html), [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html) |
| Thursday | Test duplicate event_id, malformed payloads, network loss, and API permissions. | 19/11/2026 | 19/11/2026 | [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html), [JWT Authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html), [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/) |
| Friday | Consolidate test cases, logs, and actual integration-status evidence. | 20/11/2026 | 20/11/2026 | [Cloudwatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html), [pytest](https://docs.pytest.org/en/stable/) |

## 3. Expected Outcomes and Planned Implementation

### 3.1. Event Metadata Standardization Plan

Define an event schema with `event_id`, `timestamp`, `event_type`, `state`, and any permitted additional fields. Metadata requires clear types and validation rules; raw video must not be included.

Verify when event_id is created so retries for the same event do not become separate events.

### 3.2. Local Event Buffer and Retry Plan

Design a local queue for unsynchronized events; mark an event `synced` only after a successful server response. If the network fails, Edge analysis should continue while metadata remains queued for later submission.

Planned test cases include pre-send outages, timeouts, repeated retries, application restart, and network recovery. This feature **must not be marked complete until validated**.

### 3.3. AWS Backend Testing Plan

In an authorized AWS environment, verify HTTP API, Lambda Writer, DynamoDB Conditional PutItem, Lambda Reader, and JWT Authorizer behavior. Test valid input, missing fields, repeated event_id, missing/invalid JWT, and unauthorized data access.

If Cloud infrastructure is not deployed, describe the work as **architecture and test planning** rather than fabricating logs or outcomes.

### 3.4. Image/Video Pipeline Tests

Use consented recordings or a stationary webcam setup to compare image and video paths: face detection, missing landmarks, left/right eye disagreements, mouth events, and Head Pose variations. Check error handling, CSV traces, and stability over consecutive frames.

The experimental system must not be presented as validated road-safety equipment.

### 3.5. Expected Results and Acceptance Criteria

Expected outputs include a consistent event schema, reproducible integration tests, logs/evidence for each scenario, and an issue list. Mark a capability complete only after successful execution and recorded evidence.

**Status at the drafting date:** this is the Week 9 plan, not an achieved result.

## 4. References

1. [Python](https://docs.python.org/3/)
2. [Fastapi](https://fastapi.tiangolo.com/)
3. [Pytest](https://docs.pytest.org/en/stable/)
4. [Apig](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
5. [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
6. [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html)
7. [JWT](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html)
8. [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/)

