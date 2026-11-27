---
title: "Week 10 Worklog"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

# Week 10: System Evaluation, Optimization, and Finalization

**Duration:** 23/11/2026 – 27/11/2026  

**Accuracy note:** Week 10 covers 23/11/2026 – 27/11/2026 and is the final Worklog week. It combines evaluation, application finalization, documentation, and reporting within five working days. The activities and outcomes below are **draft entries not yet confirmed by actual records or evidence**; metrics and deployment claims must be verified.

## 1. Weekly Objectives

- Evaluate eye-state, mouth behavior, Head Pose, missing signals, and temporal events using appropriately labeled test data.
- Analyze false alerts and refine Temporal Analysis and warning rules based on evidence, not on one example video.
- Measure FPS, per-frame processing time, end-to-end latency, and resource usage on test hardware.
- Review the camera/video-to-Backend pipeline, local alert output, and event metadata; fix high-priority defects and stabilize the demo.
- Standardize source code, dependencies, Windows setup instructions, AI-pipeline documentation, and tests.
- Reconcile the Edge–AWS design with actual deployment status and document security, permissions, cost, and unresolved limitations.
- Prepare final evaluation evidence, the internship report, and project handover material within Week 10.

## 2. Weekly Work Schedule

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | Review the codebase and high-priority defects; prepare labeled test cases for eyes, mouth, Head Pose, and missing-face scenarios. | 23/11/2026 | 23/11/2026 | [Python](https://docs.python.org/3/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [pytest](https://docs.pytest.org/en/stable/) |
| Tuesday | Evaluate Precision, Recall, F1-score, and Confusion Matrix when ground truth is available; inspect false positives/negatives and temporal rules. | 24/11/2026 | 24/11/2026 | [Scikit-learn](https://scikit-learn.org/stable/modules/model_evaluation.html), [OpenCV](https://docs.opencv.org/4.x/) |
| Wednesday | Test false alerts and unknown states; measure FPS, latency, CPU/RAM, and validate changes to the main processing paths. | 25/11/2026 | 25/11/2026 | [OpenCV](https://docs.opencv.org/4.x/), [FastAPI](https://fastapi.tiangolo.com/), [pytest](https://docs.pytest.org/en/stable/) |
| Thursday | Stabilize the demo and document setup, requirements, algorithms/models; reconcile AWS deployment status, access controls, security, and cost. | 26/11/2026 | 26/11/2026 | [Python](https://docs.python.org/3/), [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| Friday | Consolidate testing evidence and limitations; finalize the technical report, architecture documentation, and reproducible project handover. | 27/11/2026 | 27/11/2026 | [FastAPI Testing](https://fastapi.tiangolo.com/tutorial/testing/), [GitHub Actions](https://docs.github.com/en/actions), [AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) |

## 3. Expected Outcomes and Planned Implementation

### 3.1. Labeled Tests and Recognition Evaluation

Select images/videos used with permission and establish test labels for eye states (Open, Half-Open, Closed), mouth behaviors (speaking, ordinary opening, yawning), Head Pose (forward, turned, tilted, up/down), and missing-landmark cases. Manually assigned labels should be checked for consistency before treating them as reliable **ground truth**.

For appropriate labeled data, compute a **Confusion Matrix**, **Precision**, **Recall**, **F1-score**, and class-wise **Accuracy**. Where event labels exist, distinguish frame-level metrics from event-level temporal metrics. Do not report numerical accuracy or alerting-time claims without actual reproducible measurements.

### 3.2. Temporal Analysis and False Alert Reduction

Inspect ambiguous conditions such as normal blinking, speaking/singing, mouth opening, unusual face angles, one-eye occlusion, sudden head movements, and missing signals. Evaluate how EAR, MAR, Head Pose, eye-state classification, and multiple-frame evidence are combined.

Compare thresholds, temporal windows, continuous-duration conditions, and **Unknown/Uncertain State** handling. Refine rules only when supported by multiple test scenarios. Keep Gaze labeled as experimental if it has not been sufficiently validated.

### 3.3. Performance Measurement and Demo Stability

On target test hardware, record **FPS**, per-frame processing time, end-to-end camera-to-result/alert latency, CPU/RAM use, and capture conditions. Distinguish model inference time from total pipeline latency; document video resolution and code/model versions.

Review the flow **camera/video → OpenCV/MediaPipe → feature extraction/models → Temporal Analysis → Backend output/local alert**. Check invalid inputs, no-face conditions, missing landmarks, inconsistent model outputs, and repeated runs. Prioritize stability rather than new unvalidated features.

If local warnings or Cloud synchronization are not yet complete, report their actual state and limitations in the demo.

### 3.4. Environment Standardization and Run Instructions

Document repository layout, supported Python version, `requirements.txt`, Windows virtual environment setup, Backend startup commands, and webcam/video input methods. Describe running tests, reading logs/CSV, troubleshooting common issues, and reproducing the environment on another computer.

The handover should include only source code, non-sensitive configuration examples, permitted test data, redistributable model/checkpoint files, and required guides. Exclude `.venv`, `__pycache__`, passwords, tokens, API keys, and private face recordings.

### 3.5. Algorithm Documentation and Evaluation Evidence

Explain **OpenCV**, **MediaPipe**, **EAR**, **MAR**, **Head Pose**, eye-state models (such as MobileNet if included in the handover), temporal processing, event conditions, and warning states. All evaluation figures should identify the dataset, measurement method, hardware, and corresponding code/model versions.

Summarize working scenarios, unresolved failures, changes before and after optimization, and limitations involving lighting, glasses, camera angle, or unvalidated Gaze. Results obtained in stationary tests must not be presented as validated performance in real driving conditions.

### 3.6. AWS Architecture and Security Review

Consolidate the **Edge AI + AWS Cloud** diagrams and proposed **event metadata**, Local Event Buffer/Retry, API Gateway, Lambda Writer/Reader, DynamoDB, Cognito/JWT, private S3 + CloudFront OAC, CloudWatch, IAM, and AWS Budgets architecture.

For every service and integration, use an explicit status: **deployed and tested**, **designed but not deployed**, or **unverified**. Confirm that raw video is not sent to the Cloud and that logs/documentation disclose no sensitive keys or tokens. Report cost estimates only where settings, usage assumptions, and pricing references are available.

### 3.7. Final Internship Summary and Project Handover

Expected Week 10 deliverables include:

- A test-result table, identified failure scenarios, and notes on label reliability.
- Performance measurements, before/after comparisons, and a remaining-limitations list.
- A demonstrable version with reproducible run instructions and a verified feature scope.
- README, Edge–Cloud architecture documentation, AI-pipeline explanation, and warning criteria.
- Setup/dependency/test guides, permitted model/checkpoint inventory, and safe sample data.
- An accurate AWS status report, residual risks, and a prioritized backlog for future development.
- The final FCAJ internship summary, main learning outcomes, and lessons learned.

The handover should allow another team member to set up and inspect the project without relying on the original developer's machine. **Week 10 is the final Worklog week**, including project handover preparation and internship reporting.

**Status at drafting:** all activities above remain the Week 10 plan and expected results. Mark individual items as completed only after evidence is available.

## 4. References

1. [Python Documentation](https://docs.python.org/3/)
2. [MediaPipe Face Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
3. [OpenCV Documentation](https://docs.opencv.org/4.x/)
4. [Scikit-learn Model Evaluation](https://scikit-learn.org/stable/modules/model_evaluation.html)
5. [pytest](https://docs.pytest.org/en/stable/)
6. [FastAPI](https://fastapi.tiangolo.com/)
7. [FastAPI Testing](https://fastapi.tiangolo.com/tutorial/testing/)
8. [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
9. [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
10. [AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)
11. [GitHub Actions](https://docs.github.com/en/actions)
