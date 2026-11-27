---
title: "Project Proposal"
date: 2026-11-27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Driver Drowsiness & Distraction Detection
## An Edge AI and AWS Serverless Solution for Driver-State Monitoring

### 1. Executive Summary

**Driver Drowsiness & Distraction Detection** is a research and prototype-development project that combines Computer Vision, Edge AI, and AWS Cloud to identify observable signs potentially associated with driver drowsiness or distraction. The objective is to support earlier awareness of unusual driver behavior, not to replace certified vehicle-safety systems or determine a driver's medical condition.

The system captures facial images through a webcam and processes the video **locally on an Edge Device**. Python, OpenCV, and MediaPipe Face Mesh (478 facial landmarks, as specified in the project proposal) support the extraction of **Eye Aspect Ratio (EAR)**, **Mouth Aspect Ratio (MAR)**, **Head Pose**, and an experimental **Gaze Direction** feature. Temporal Analysis, CSV-based examination, and rule-based candidates are used to investigate changes over time rather than relying on single-frame decisions.

The proposed cloud architecture sends **event metadata only**, not raw webcam video, to Amazon API Gateway (HTTP API). AWS Lambda validates the events and uses conditional writes to Amazon DynamoDB. Amazon Cognito provides dashboard authentication, while a private Amazon S3 origin and Amazon CloudFront are intended to deliver the web interface. Amazon CloudWatch, IAM, CloudTrail, and AWS Budgets support operations, security, and cost control; AWS WAF remains optional.

**Current status:** The Edge image-processing pipeline has been built and the AWS architecture has been designed. Local Event Buffer/Retry, temporal-analysis refinement, Gaze evaluation, cloud integration, and resilience testing remain to be completed or validated. The proposal describes the *intended system*, not a fully deployed production service.

### 2. Problem Statement

#### What's the Problem?

A driver may display signs such as prolonged eye closure, yawning, changes in head posture, or changes in gaze direction. Detecting and interpreting these signs consistently is challenging because facial behavior varies across people and depends on lighting, camera angle, occlusion, and motion.

A cloud-only design that continuously uploads video can create additional bandwidth usage, latency, operational costs, and privacy risks. A monitoring prototype should therefore distinguish local visual analysis from remote event storage, remain useful during connectivity interruptions, and avoid presenting uncertain observations as definitive diagnoses.

#### The Solution

The project adopts a **hybrid Edge AI + AWS Serverless** architecture:

1. **Local capture and analysis:** The webcam supplies frames to OpenCV and MediaPipe. The Edge pipeline extracts EAR, MAR, Head Pose, and experimental Gaze features.
2. **Temporal assessment:** CSV analysis and rule-based candidates examine patterns across time to identify events worth recording; thresholds and rules require evaluation.
3. **Local buffering:** Each event is associated with an `event_id`. The planned Local Event Buffer retains metadata when the network is unavailable, while Retry attempts synchronization after connectivity returns.
4. **Cloud event ingestion:** The Edge Device sends metadata via HTTPS POST to API Gateway. Lambda Event Writer validates the request and uses DynamoDB `Conditional PutItem` to help prevent duplicate writes by `event_id`.
5. **Protected history access:** The dashboard uses Amazon Cognito and JWT authorization for its protected API routes. Lambda Event Reader queries DynamoDB and returns the permitted event history.
6. **Distribution and monitoring:** CloudFront delivers the Frontend from a private S3 origin using Origin Access Control (OAC). CloudWatch provides operational logs and metrics.

The design keeps video processing at the Edge. Its cloud component is intended to handle **metadata, access, storage, and observability**, rather than remote video inference.

#### Benefits and Practical Value

- **Privacy-oriented design:** Raw video is not transmitted to AWS in the proposed workflow.
- **Reduced network dependence:** Face and feature analysis can continue locally; synchronization is designed to resume after temporary network failures.
- **Manageable infrastructure:** API Gateway, Lambda, and DynamoDB reduce the need to administer application servers.
- **Reviewable events:** The proposed dashboard allows authorized users to retrieve recorded event history.
- **Learning outcomes:** The project connects AI/Computer Vision development with AWS security, serverless services, frontend delivery, and monitoring.

No measured improvement in crash rates, financial return, or operating-cost savings is claimed at this stage.

### 3. Solution Architecture

The design consists of three logical layers: **Edge Processing**, **AWS Event Backend**, and **Web Dashboard**. Only event metadata crosses the Edge-to-Cloud boundary.

```text
EDGE PROCESSING (local device)
Webcam -> OpenCV -> MediaPipe Face Mesh (478 landmarks)
       -> EAR / MAR / Head Pose / experimental Gaze
       -> CSV Analysis + Temporal / Rule-based Candidates
       -> Event Metadata (event_id)
       -> Planned Local Event Buffer + Retry
                      |
                 HTTPS POST
             (metadata only)
                      v
AWS EVENT BACKEND
Amazon API Gateway (HTTP API)
       -> AWS Lambda Event Writer (validation)
       -> Amazon DynamoDB (Conditional PutItem by event_id)

WEB DASHBOARD / HISTORY PATH
Browser -> Amazon Cognito (sign-in / JWT)
        -> API Gateway (JWT Authorizer for protected routes)
        -> AWS Lambda Event Reader
        -> Amazon DynamoDB -> Event History -> Browser

Frontend delivery: private Amazon S3 -> CloudFront (OAC) -> Browser
Observability: CloudWatch | Access control: IAM | Audit: CloudTrail
Cost management: AWS Budgets | Optional additional protection: AWS WAF
```

*Figure 1 – Proposed Edge AI and AWS Cloud architecture (text diagram). This is a design representation, not proof that the cloud components have been deployed.*

#### AWS Services Used

| AWS Service | Intended Responsibility | Status in Source Proposal |
|---|---|---|
| Amazon API Gateway (HTTP API) | Receive Edge event submissions and dashboard requests | Architecture designed |
| AWS Lambda – Event Writer | Validate event metadata and write events | Architecture designed |
| Amazon DynamoDB | Store event history and support conditional writes | Architecture designed |
| AWS Lambda – Event Reader | Retrieve event history for the dashboard | Architecture designed |
| Amazon Cognito | User registration, sign-in, and JWT issuance | Architecture designed |
| Amazon S3 | Private hosting origin for frontend assets | Architecture designed |
| Amazon CloudFront + OAC | Deliver the frontend while restricting direct S3 access | Architecture designed |
| Amazon CloudWatch | API access logs, Lambda logs/errors/duration, DynamoDB metrics | Monitoring design proposed |
| AWS IAM | Service permissions and least-privilege access | Supporting control proposed |
| AWS CloudTrail | AWS account activity auditing | Supporting control proposed |
| AWS Budgets | Budget monitoring and alerts | Supporting control proposed |
| AWS WAF | Additional application-layer protection | **Optional** |

#### Component Design

**Edge AI Processing**
- **Input:** Webcam video, processed locally with OpenCV.
- **Facial analysis:** MediaPipe Face Mesh provides 478 landmarks as described in the project source.
- **Feature extraction:** EAR, MAR, Head Pose, and experimental Gaze Direction.
- **Temporal analysis:** CSV analysis and rule-based candidates; the final algorithm still requires refinement and validation.
- **Event synchronization:** Proposed `event_id`, Local Event Buffer, and Retry handling; not yet confirmed as complete.

**Cloud Event Processing**
- **Ingestion:** API Gateway receives HTTPS POST event requests containing metadata rather than raw video.
- **Validation and persistence:** Lambda Event Writer validates data before DynamoDB conditional writes to help avoid duplicates.
- **History retrieval:** Protected dashboard requests reach Lambda Event Reader through API Gateway and are answered from DynamoDB.

**Frontend, Identity, and Operations**
- **Authentication:** Cognito issues JWTs for dashboard sign-in; API Gateway JWT Authorizer protects designated routes.
- **Distribution:** CloudFront serves static frontend files from a private S3 bucket through OAC.
- **Operations:** CloudWatch monitors service behavior; IAM, CloudTrail, and Budgets support access control, auditing, and cost awareness.

*Security design note:* The source describes JWT authorization for dashboard access but does not specify the final authentication method for Edge ingestion. That control must be defined and tested before external deployment. JWT validation alone also does not establish per-user authorization of every DynamoDB item.

### 4. Technical Implementation

#### Implementation Phases

The project is organized into the following work packages. Their sequence is a planning structure, not a claim that all phases have been completed.

1. **Research and Edge proof of concept:** Study drowsiness/distraction indicators, build webcam processing with OpenCV and MediaPipe, and extract EAR, MAR, Head Pose, and experimental Gaze features. **Status:** Edge pipeline built; Gaze still experimental.
2. **Temporal interpretation and evaluation:** Use CSV-based analysis and rule-based candidates to study changes across frames, refine event criteria, and evaluate false warnings. **Status:** Initial approach established; further work required.
3. **Reliable local event handling:** Define the event metadata contract and `event_id`, implement a Local Event Buffer, and verify retry/resynchronization after network interruption. **Status:** Designed; completion and failure testing pending.
4. **AWS backend and dashboard integration:** Configure API Gateway, Lambda Writer/Reader, DynamoDB, Cognito, private S3/CloudFront OAC, and monitoring. Confirm permissions and end-to-end event history retrieval. **Status:** Cloud architecture designed; full deployment not verified by the source.
5. **Validation and documentation:** Test varied lighting and camera angles, network outages, event duplication, backend failures, access control, monitoring, and budget alerts. Document actual findings and limitations. **Status:** Planned / requires evidence.

#### Technical Requirements

- **Edge equipment:** A webcam and a computer capable of running the local Computer Vision pipeline. The source does not specify required CPU/GPU specifications.
- **Edge software:** Python, OpenCV, MediaPipe Face Mesh, temporal processing and CSV analysis, plus a planned local buffer and retry component.
- **Cloud services:** Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon Cognito, Amazon S3, Amazon CloudFront, and Amazon CloudWatch; supporting IAM, CloudTrail, AWS Budgets, and optional WAF.
- **Data contract:** Metadata-only event submissions with a unique `event_id`; the final schema, retention period, and data access rules are to be finalized.
- **Privacy and security:** No raw video uploads, least-privilege service roles, authenticated dashboard requests, and explicit authorization of event-history access.
- **Evaluation:** Review event recognition quality, false alarms, latency, network resilience, and behavior in difficult visual conditions. Numerical targets are not yet established.

### 5. Timeline & Milestones

The original project document does **not** specify confirmed calendar dates or completed milestones. The following is a **proposed mapping** to the FCAJ Week 6–12 worklog structure; it should be adjusted to match actual work records.

| Proposed Period | Focus | Evidence / Deliverable |
|---|---|---|
| Week 6 | Problem research and requirements | Problem definition, initial features, functional and privacy requirements |
| Week 7 | Architecture and data-flow design | Edge–Cloud diagram, event flow, AWS service responsibilities |
| Week 8 | Core Edge functionality | Webcam processing, feature extraction, initial temporal candidates |
| Week 9 | Integration and testing | Local metadata flow, AWS integration checks, test records |
| Week 10 | Evaluation and optimization | Lighting/angle testing, false-alert analysis, performance observations |
| Week 11 | Finalization and documentation | Improved reliability, setup notes, architecture and test documentation |
| Week 12 | Final report and demonstration | Verified outcomes, limitations, demonstration and internship report |

**Milestone policy:** Mark a milestone complete only after code, logs, screenshots, test records, or other supporting evidence confirms it. The source currently confirms an Edge pipeline and a designed Cloud architecture, not a completed end-to-end deployment.

### 6. Budget Estimation

The project selects a serverless approach to limit fixed server-management overhead at an early stage. **No actual AWS Pricing Calculator estimate or measured monthly AWS bill is included in the source proposal.** Therefore, exact costs are intentionally left unreported rather than copied from the unrelated weather-platform template.

#### Infrastructure Cost Components

| Component | Main Cost Driver to Estimate |
|---|---|
| Amazon API Gateway | Number of API requests |
| AWS Lambda | Requests, memory allocation, and execution duration |
| Amazon DynamoDB | Read/write activity and stored event data |
| Amazon Cognito | Applicable user/authentication pricing model |
| Amazon S3 | Frontend storage and requests |
| Amazon CloudFront | Data transfer and requests |
| Amazon CloudWatch | Logs, retention, metrics, and alarms |
| AWS CloudTrail | Applicable audit logging and storage configuration |
| AWS WAF (optional) | Usage-based protection charges if enabled |
| Edge hardware / network | Existing hardware availability, local electricity, and connectivity |

**Estimate required before deployment:** Define expected devices, events per device/day, API calls, metadata size, stored history, dashboard usage, AWS Region, and log retention; then calculate costs with the [AWS Pricing Calculator](https://calculator.aws/).

**Cost controls:** Configure AWS Budgets and alerts, review CloudWatch log retention, minimize unnecessary requests, and send only required metadata. No ROI or break-even period is claimed without measured inputs.

### 7. Risk Assessment

#### Preliminary Risk Matrix

The classifications below are *planning judgments*, not measured occurrence probabilities.

| Risk | Potential Impact | Planned Response |
|---|---|---|
| Unreliable or missing Internet connection | Event metadata may not reach AWS immediately | Local Event Buffer, Retry, and recovery testing |
| Poor lighting, camera angle, or facial occlusion | Incorrect facial measurements or missed features | Evaluate across varied conditions; allow uncertain/unknown states |
| Inaccurate temporal rules or false warnings | Incorrect driver-state alerts | Refine rules using recorded tests and review false-alarm cases |
| Experimental Gaze Direction | Unreliable distraction indication | Keep Gaze experimental until separately validated |
| Duplicate event submissions | Duplicate history records | Unique `event_id` and DynamoDB conditional writes |
| Unauthorized event-history access | Privacy and security exposure | Cognito/JWT plus data-level authorization and IAM review |
| Cloud outage or service misconfiguration | Event ingestion or dashboard interruption | Retain pending events locally; monitor and test recovery |
| Unexpected AWS cost | Budget overrun | Budgets alerts, usage monitoring, and usage-based estimation |

#### Mitigation Strategies

- **Detection reliability:** Evaluate against varied lighting conditions and camera angles; document failures and uncertainty.
- **Network resilience:** Preserve pending event metadata locally and test delivery after reconnection.
- **Data integrity:** Apply a consistent event identifier and conditional insertion to minimize duplicates.
- **Privacy:** Keep raw video at the Edge; restrict and audit access to stored metadata.
- **Cloud observability:** Review CloudWatch logs, error rates, execution duration, and DynamoDB activity.
- **Cost governance:** Use AWS Budgets and re-check estimates as traffic increases.

#### Contingency Plans

- If the Internet is unavailable, continue local analysis and retain unsynchronized events until transfer is possible, subject to the buffer's eventual tested behavior.
- If facial features are unreliable, avoid definitive interpretation and record the limitation for evaluation.
- If a cloud component fails, inspect logs and permissions, correct the issue, and retest before considering the integration complete.
- If costs increase unexpectedly, reduce nonessential usage and reconsider retention, logging, or optional services.

### 8. Expected Outcomes

#### Technical Improvements

Upon completion and validation, the system is expected to:

- Process webcam video locally for facial feature extraction and temporal driver-state analysis.
- Identify potential drowsiness- or distraction-related events without uploading raw video to AWS.
- Create event metadata and synchronize it reliably through a buffer/retry mechanism.
- Store and retrieve event history using API Gateway, Lambda, and DynamoDB.
- Provide a protected dashboard using Cognito, private S3 hosting, and CloudFront.
- Monitor service health and usage through CloudWatch and AWS Budgets.

#### Long-term Value

- Demonstrate how Edge AI and AWS Serverless components can be combined in one application.
- Provide a modular foundation for improving temporal analysis and studying additional facial indicators.
- Support future evaluation of reliability, privacy, cost, and user experience.
- Serve as a technical learning outcome of the First Cloud AI Journey (FCAJ) internship.

**Scope limitation:** These are expected outcomes. Recognition accuracy, production readiness, and effectiveness in real driving conditions must be established through documented tests rather than assumed from the architecture alone.
