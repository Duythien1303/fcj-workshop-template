---
title: "Worklog Tuần 7"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

# Tuần 7: Phân tích hệ thống và thiết kế kiến trúc

**Thời gian:** 16/11/2026 – 20/11/2026  
**Trạng thái:** Bản nháp cần đối chiếu nhật ký thực tế

**Lưu ý về tính xác thực:** Lịch theo từng ngày dưới đây là bản phân bổ biên tập dựa trên proposal và tiến độ chung, **chưa phải nhật ký công việc từng ngày đã được xác nhận**. Các nội dung mô tả kết quả không nhằm khẳng định đã hoàn thành toàn bộ chức năng trong đúng tuần này.

## 1. Mục tiêu tuần

- Phân tách hệ thống thành các lớp Edge Processing, Event Synchronization, AWS Backend và Web Dashboard.
- Thiết kế luồng dữ liệu từ webcam đến metadata sự kiện và xác định ranh giới bảo mật.
- Lựa chọn các dịch vụ AWS phù hợp: API Gateway, Lambda, DynamoDB, Cognito, S3, CloudFront, CloudWatch, IAM, CloudTrail và Budgets.
- Định nghĩa hướng triển khai Local Event Buffer, Retry, ghi sự kiện không trùng và API đọc lịch sử.
- Hoàn thiện kiến trúc đề xuất và xác định các thành phần chưa triển khai để đưa sang giai đoạn phát triển.

## 2. Nội dung công việc

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| Thứ 2 | Phân tích luồng dữ liệu Edge AI và các điều kiện phát sinh sự kiện. | 16/11/2026 | 16/11/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [OpenCV](https://docs.opencv.org/4.x/) |
| Thứ 3 | Phân chia module: feature extraction, temporal processing, event metadata và local buffer. | 17/11/2026 | 17/11/2026 | [Python](https://docs.python.org/3/), [FastAPI](https://fastapi.tiangolo.com/) |
| Thứ 4 | Thiết kế luồng ghi metadata qua HTTP API, Lambda Writer và DynamoDB với event_id. | 18/11/2026 | 18/11/2026 | [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html), [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html) |
| Thứ 5 | Thiết kế xác thực Cognito/JWT, Lambda Reader và phân phối Dashboard qua S3/CloudFront. | 19/11/2026 | 19/11/2026 | [Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html), [JWT Authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html), [Cloudfront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html) |
| Thứ 6 | Rà soát sơ đồ hệ thống, quyền riêng tư, IAM, giám sát và giới hạn chi phí. | 20/11/2026 | 20/11/2026 | [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html), [Cloudwatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html), [Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) |

## 3. Kết quả đạt được và nội dung nghiên cứu

### 3.1. Phân lớp kiến trúc Edge–Cloud

**Edge Device:** webcam → OpenCV → MediaPipe Face Landmarker → trích xuất EAR/MAR/Head Pose/Gaze → phân tích theo thời gian → tạo metadata sự kiện. **Đồng bộ:** Local Event Buffer và Retry được thiết kế để lưu sự kiện khi mạng không ổn định. **AWS Backend:** API Gateway → Lambda → DynamoDB. **Web:** giao diện đọc lịch sử được phân phối qua CloudFront với nguồn S3 private.

Đây là **kiến trúc mục tiêu**, không phải báo cáo rằng tất cả dịch vụ cloud đã hoạt động thực tế.

### 3.2. Dòng dữ liệu và hợp đồng metadata

Video chỉ được xử lý tại Edge. Luồng đồng bộ dự kiến sử dụng HTTPS POST để gửi event metadata thay vì video. Mỗi bản ghi cần một `event_id` ổn định khi retry để có thể nhận diện sự kiện trùng; ngoài ra cần trường thời điểm, loại sự kiện, trạng thái và thông tin nguồn phù hợp chính sách dữ liệu.

Lược đồ metadata cụ thể, quy tắc kiểm tra dữ liệu và phân quyền theo người dùng/thiết bị cần được chốt trước triển khai. Không đưa dữ liệu khuôn mặt hoặc video vào payload minh họa.

### 3.3. Thiết kế Event Writer và lưu trữ lịch sử

Amazon API Gateway HTTP API tiếp nhận request, AWS Lambda Event Writer kiểm tra payload và ghi vào DynamoDB. Giải pháp đề xuất **Conditional PutItem** dựa trên `event_id` để giảm ghi trùng khi cùng sự kiện được gửi lại.

Tính đúng đắn của tính năng này phụ thuộc vào thiết kế khóa DynamoDB và điều kiện ghi; cần có test thực tế với cùng event_id, payload sai và lỗi kết nối.

### 3.4. Thiết kế xác thực và Dashboard

Amazon Cognito được đề xuất cho đăng ký, đăng nhập và cấp JWT. API Gateway JWT Authorizer bảo vệ những endpoint cần xác thực; Lambda Event Reader thực hiện truy vấn DynamoDB theo phạm vi cho phép.

Frontend dự kiến đặt trong S3 private, phân phối qua CloudFront Origin Access Control (OAC). **JWT xác thực không tự động bảo đảm phân quyền dữ liệu theo người dùng**: tầng xử lý phải kiểm tra quyền truy xuất bản ghi phù hợp.

### 3.5. Giám sát, bảo mật và tối ưu chi phí

Các thành phần bổ trợ được thiết kế gồm IAM Least Privilege, CloudWatch logs/metrics cho API và Lambda, CloudTrail để theo dõi hoạt động tài khoản và AWS Budgets để kiểm soát ngân sách. AWS WAF chỉ là lựa chọn **optional** trong kiến trúc.

Sự cố Internet không nên ngăn pipeline nhận diện tại Edge; khả năng lưu và gửi lại sự kiện phải được kiểm thử sau khi hiện thực.

### 3.6. Tổng kết tuần 7

Kết quả thiết kế là sơ đồ các module, luồng dữ liệu và danh sách dịch vụ/luật tương tác trong kiến trúc Edge–Cloud. Đây là **thiết kế kỹ thuật** đã được trình bày trong proposal; các chức năng lưu đệm, dashboard và hạ tầng AWS vẫn cần triển khai hoặc kiểm chứng, không được ghi là hoàn thành chỉ từ sơ đồ.

## 4. Tài liệu tham khảo

1. [Mediapipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
2. [Opencv](https://docs.opencv.org/4.x/)
3. [Python](https://docs.python.org/3/)
4. [Fastapi](https://fastapi.tiangolo.com/)
5. [Apig](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
6. [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
7. [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html)
8. [Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)

