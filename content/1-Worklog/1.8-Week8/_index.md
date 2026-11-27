---
title: "Week 8 Worklog"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

# Week 8: Core Edge Feature Development and Implementation

**Duration:** 09/11/2026 – 13/11/2026  
**Status:** Draft requiring daily-log verification

**Accuracy note:** The day-by-day schedule is an editorial allocation based on the proposal and overall progress, **not a verified daily work record**. Reported project capabilities are not proof that every item was completed in this exact week.

## 1. Weekly Objectives

- Develop and review a Python/OpenCV/MediaPipe image/video processing pipeline.
- Integrate eye, mouth, Head Pose, and temporal features within the Backend scope.
- Investigate combining geometric measurements with an eye-state classifier such as MobileNet.
- Study false-positive scenarios, capture CSV analysis traces, and establish local test cases.
- Distinguish locally tested functionality from unverified features such as production gaze analysis, finalized alarms, and Cloud deployment.

## 2. Weekly Work Schedule

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| Monday | Review webcam/video processing, facial landmarks, and EAR/MAR outputs. | 09/11/2026 | 09/11/2026 | [OpenCV](https://docs.opencv.org/4.x/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker) |
| Tuesday | Investigate candidate models for eye-region detection and classification. | 10/11/2026 | 10/11/2026 | [Ultralytics](https://docs.ultralytics.com/), [Python](https://docs.python.org/3/) |
| Wednesday | Integrate or check Open/Half-Open/Closed eye labels and left/right eye handling. | 11/11/2026 | 11/11/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [Python](https://docs.python.org/3/) |
| Thursday | Test neutral Head Pose, mouth/yawning states, and potential false alarms. | 12/11/2026 | 12/11/2026 | [OpenCV](https://docs.opencv.org/4.x/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker) |
| Friday | Review Backend analysis flow, CSV traces, test scenarios, and technical notes. | 13/11/2026 |13/11/2026 | [FastAPI](https://fastapi.tiangolo.com/), [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/) |

## 3. Research Findings and Recorded Progress

### 3.1. Camera Pipeline and Facial Landmarks

Project progress reported by late November includes an Edge image-processing pipeline using a webcam, OpenCV, and MediaPipe. Landmarks support eye, mouth, and head-orientation feature extraction.

The processing is intended to run locally; raw video is not sent to AWS. Landmark quality may still decrease under poor lighting, large head rotations, or facial occlusion.

### 3.2. Eye State Analysis and Model Experiments

The Backend research combines **EAR** with an eye-state classification approach. Experimental labels include **Open, Half-Open, and Closed**; left and right eyes should be evaluated independently because their signals may differ.

YOLOv8n and MobileNet were explored. Some YOLOv8n trial detections were unsuitable for the intended eye monitoring task, and should not be reported as successful eye detections. MobileNet-based classification still requires evaluation using reliable labeled data.

### 3.3. EAR, MAR, Head Pose, and Gaze

**EAR** indicates eye openness; **MAR** characterizes mouth opening and yawning-related movements; **Head Pose** estimates Pitch/Yaw/Roll and may be calibrated against a neutral forward-facing baseline. **Gaze Direction** remains experimental and is not validated as a primary decision signal.

Local checks included prolonged eye closure, head turns, upward/downward head movement, and mouth-opening examples. Such results are useful for development but do not establish real-driving safety performance.

### 3.4. Temporal Analysis and False-Positive Control

Feature sequences can be exported for time-series inspection. CSV traces allow developers to compare frames, feature values, and predictions. The initial approach uses **rule-based candidates**; the temporal algorithm still requires improvement.

Speaking, singing, or ordinary mouth opening can cause false yawning detections. Duration and temporal motion patterns therefore matter; merely raising the MAR threshold may not solve the issue. No Precision, Recall, or F1-score is claimed without a standardized labeled evaluation set.

### 3.5. Backend and Local Testing

By late November, the Backend code had progressed toward organized image/video processing services and driver-state components. FastAPI is part of the backend/API approach, while CSV feature traces support investigation and debugging.

Test scenarios include invalid inputs, missing faces, unavailable landmarks, disagreement between eyes, Head Pose variations, and consecutive-frame handling. A common image/video pipeline is an architectural goal for consistent behavior.

### 3.6. Week 8 Summary

Late-November progress indicates that the **Edge AI pipeline and Backend analysis have been exercised locally**, although classifier and warning quality still need validation. Local Event Buffer/Retry, production AWS deployment, Dashboard, reliable gaze analysis, and GRU/LSTM/Transformer sequence models are not reported as completed. These remain candidates for subsequent integration, testing, or optimization.

## 4. References

1. [Opencv](https://docs.opencv.org/4.x/)
2. [Mediapipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
3. [Ultralytics](https://docs.ultralytics.com/)
4. [Python](https://docs.python.org/3/)
5. [Fastapi](https://fastapi.tiangolo.com/)
6. [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/)

