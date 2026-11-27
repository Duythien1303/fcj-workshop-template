---
title: "Week 6 Worklog"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

# Week 6: Project Research and System Requirements Definition

**Duration:** 09/11/2026 – 13/11/2026  
**Status:** Draft requiring daily-log verification

**Accuracy note:** The day-by-day schedule is an editorial allocation based on the proposal and overall progress, **not a verified daily work record**. Reported project capabilities are not proof that every item was completed in this exact week.

## 1. Weekly Objectives

- Investigate the **Driver Drowsiness & Distraction Detection** problem, observable signs potentially related to drowsiness or distraction, and limitations of camera-based inference.
- Define an **Edge AI + AWS Cloud** direction: process video locally and transmit event metadata only.
- Survey Python, OpenCV, MediaPipe Face Landmarker, and the EAR, MAR, Head Pose, and Gaze Direction features.
- Identify functional/non-functional requirements, expected inputs/outputs, and the initial prototype scope.
- Establish a research basis for system architecture design in Week 7.

## 2. Weekly Work Schedule

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | Study the road-safety context and frame the problem of detecting observable drowsiness/distraction-related behaviors. | 09/11/2026 | 09/11/2026 | [Safety](https://www.nhtsa.gov/risky-driving/drowsy-driving) |
| Tuesday | Review webcam frame acquisition, image processing, and facial landmark detection. | 10/11/2026 | 10/11/2026 | [OpenCV](https://docs.opencv.org/4.x/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker) |
| Wednesday | Study EAR, MAR, Head Pose, Gaze, and the importance of temporal analysis. | 11/11/2026 | 11/11/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [Python](https://docs.python.org/3/) |
| Thursday | Draft functional and non-functional requirements and define permissible cloud event metadata. | 12/11/2026 | 12/11/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| Friday | Consolidate research scope, proposed test cases, and questions to resolve in system design. | 13/11/2026 | 13/11/2026 | [Safety](https://www.nhtsa.gov/risky-driving/drowsy-driving), [OpenCV](https://docs.opencv.org/4.x/) |

## 3. Research Findings and Recorded Progress

### 3.1. Problem Analysis and System Limitations

Driver Drowsiness & Distraction Detection is intended to **support the observation of behaviors potentially associated with driver state**, not to diagnose alertness conclusively. Features of interest include prolonged eye closure, mouth activity, head orientation, and experimental gaze information.

A single frame is insufficient to determine whether a driver is drowsy or distracted. The research therefore considers signals over multiple frames and possible false alarms caused by speaking, head turns, or changing illumination.

### 3.2. Rationale for Edge AI and AWS Cloud

The proposed approach separates **local image processing at the Edge** from **cloud-based event-history management**. Camera frames enter the local pipeline; raw video is not uploaded to AWS. When a relevant event occurs, the intended mechanism creates an `event_id` and sends controlled metadata.

This design aims to reduce video transfers, limit dependence on Internet access during inference, and support privacy. Local buffering, retry, and AWS resources remain **proposed architecture components**, not claims of completed deployment.

### 3.3. Computer Vision Feature Research

- **MediaPipe Face Landmarker:** provides facial landmarks (up to 478 in the relevant configuration) for analyzing eye, mouth, and facial geometry.
- **EAR (Eye Aspect Ratio):** a geometric indicator of eye openness and eye-state transitions.
- **MAR (Mouth Aspect Ratio):** a measure of mouth openness that may help characterize yawning-related movements.
- **Head Pose:** represents head orientation through Pitch, Yaw, and Roll.
- **Gaze Direction:** an experimental research direction, not a validated feature.

These features must be interpreted with temporal context and capture conditions rather than treating one threshold as a final diagnosis.

### 3.4. Functional and Non-functional Requirements

**Proposed functional requirements:** accept webcam/video input; detect faces; analyze eye state and other facial features; track state over consecutive frames; display status and confidence where available; record event metadata; and eventually provide event history through a Dashboard.

**Non-functional requirements:** responsive demo performance; no confident output when landmarks are missing; graceful input error handling; limited storage of personal imagery; access control for protected APIs; and logs that support debugging and evaluation.

### 3.5. Inputs, Outputs, and Scope

**Inputs:** webcam frames and consented sample videos in a stationary testing setting. **Proposed Edge outputs:** face-detection state, EAR/MAR/Head Pose features, and monitoring results. **Proposed Cloud output:** event metadata containing `event_id`, timestamp, and event type, without video.

Evaluation cases should include open/closed eyes, head turns, speaking, lighting changes, camera-angle variation, and missing data. Accuracy and FPS targets should not be invented without measurements.

### 3.6. Week 6 Summary

Week 6 lays the foundation for transitioning from AWS/Generative AI study to a Driver Monitoring project. The deliverables at this stage are an **initial scope and requirements**, not an accepted production system. Week 7 will focus on processing flows, Edge AI components, and the AWS Serverless architecture.

## 4. References

1. [Safety](https://www.nhtsa.gov/risky-driving/drowsy-driving)
2. [Opencv](https://docs.opencv.org/4.x/)
3. [Mediapipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
4. [Python](https://docs.python.org/3/)
5. [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

