---
title: "Worklog Tuần 6"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

# Tuần 6: Nghiên cứu đề tài và xác định yêu cầu hệ thống

**Thời gian:** 26/10/2026 – 30/10/2026  
**Trạng thái:** Bản nháp cần đối chiếu nhật ký thực tế

**Lưu ý về tính xác thực:** Lịch theo từng ngày dưới đây là bản phân bổ biên tập dựa trên proposal và tiến độ chung, **chưa phải nhật ký công việc từng ngày đã được xác nhận**. Các nội dung mô tả kết quả không nhằm khẳng định đã hoàn thành toàn bộ chức năng trong đúng tuần này.

## 1. Mục tiêu tuần

- Tìm hiểu bài toán **Driver Drowsiness & Distraction Detection**, các dấu hiệu có thể liên quan đến buồn ngủ hoặc mất tập trung và giới hạn của việc phân tích qua camera.
- Định hướng giải pháp **Edge AI + AWS Cloud**: video được xử lý tại thiết bị; Cloud chỉ nhận metadata của sự kiện.
- Khảo sát Python, OpenCV, MediaPipe Face Landmarker và các đặc trưng EAR, MAR, Head Pose, Gaze Direction.
- Xác định yêu cầu chức năng, phi chức năng, dữ liệu đầu vào/đầu ra và phạm vi bản thử nghiệm.
- Chuẩn bị cơ sở nghiên cứu để thiết kế kiến trúc hệ thống ở tuần 7.

## 2. Nội dung công việc

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| Thứ 2 | Nghiên cứu bối cảnh an toàn giao thông, đặt vấn đề phát hiện dấu hiệu buồn ngủ và mất tập trung qua camera. | 26/10/2026 | 26/10/2026 | [Safety](https://www.nhtsa.gov/risky-driving/drowsy-driving) |
| Thứ 3 | Khảo sát quy trình đọc webcam, xử lý khung hình và nhận diện landmarks trên khuôn mặt. | 27/10/2026 | 27/10/2026 | [OpenCV](https://docs.opencv.org/4.x/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker) |
| Thứ 4 | Tìm hiểu đặc trưng EAR, MAR, Head Pose, Gaze và sự cần thiết của phân tích theo thời gian. | 28/10/2026 | 28/10/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [Python](https://docs.python.org/3/) |
| Thứ 5 | Phác thảo yêu cầu chức năng/phi chức năng; làm rõ dữ liệu sự kiện được phép đồng bộ lên Cloud. | 29/10/2026 | 29/10/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| Thứ 6 | Tổng hợp phạm vi nghiên cứu, tiêu chí kiểm thử đề xuất và những điểm cần xác minh ở giai đoạn thiết kế. | 30/10/2026 | 30/10/2026 | [Safety](https://www.nhtsa.gov/risky-driving/drowsy-driving), [OpenCV](https://docs.opencv.org/4.x/) |

## 3. Kết quả đạt được và nội dung nghiên cứu

### 3.1. Phân tích bài toán và giới hạn của hệ thống

Driver Drowsiness & Distraction Detection được định hướng là hệ thống **hỗ trợ quan sát các dấu hiệu có thể liên quan đến trạng thái tài xế**, không phải công cụ chẩn đoán chính xác mức độ tỉnh táo. Các tín hiệu quan tâm gồm mắt nhắm kéo dài, trạng thái miệng, hướng và tư thế đầu, cùng thông tin hướng nhìn ở mức nghiên cứu.

Một khung hình đơn lẻ không đủ để kết luận tài xế buồn ngủ hoặc mất tập trung. Vì vậy, bài toán cần xem xét diễn biến các tín hiệu qua nhiều khung hình và khả năng xảy ra cảnh báo nhầm khi nói chuyện, quay đầu hoặc thay đổi ánh sáng.

### 3.2. Lý do lựa chọn kiến trúc Edge AI kết hợp AWS

Phương án đề xuất phân tách **xử lý hình ảnh tại Edge** và **quản lý lịch sử trên Cloud**. Camera truyền khung hình vào pipeline cục bộ; video gốc không được đưa lên AWS. Nếu phát sinh sự kiện, thiết bị dự kiến tạo `event_id` và gửi metadata có kiểm soát.

Lựa chọn này nhằm giảm nhu cầu truyền video, hạn chế phụ thuộc Internet khi phân tích và tạo cơ sở bảo vệ quyền riêng tư. Các bước lưu đệm, retry và dịch vụ AWS lúc này chỉ là thành phần **thiết kế**, chưa được coi là đã triển khai.

### 3.3. Khảo sát các đặc trưng Computer Vision

- **MediaPipe Face Landmarker:** cung cấp hệ thống điểm đặc trưng khuôn mặt (theo cấu hình phù hợp có thể nhận 478 landmarks), làm cơ sở xác định vị trí mắt, miệng và hình học khuôn mặt.
- **EAR (Eye Aspect Ratio):** tỷ lệ hình học mô tả độ mở của mắt, có thể hỗ trợ phân tích thay đổi mở/nhắm.
- **MAR (Mouth Aspect Ratio):** đặc trưng mô tả độ mở miệng, có thể hỗ trợ phân tích biểu hiện ngáp.
- **Head Pose:** ước lượng các chuyển động Pitch, Yaw và Roll để mô tả hướng đầu.
- **Gaze Direction:** là hướng nghiên cứu thử nghiệm; không được xem là tính năng đã được kiểm định.

Các đặc trưng phải được kết hợp với ngữ cảnh thời gian và điều kiện quay, thay vì sử dụng một ngưỡng duy nhất như kết luận cuối cùng.

### 3.4. Yêu cầu chức năng và phi chức năng

**Yêu cầu chức năng đề xuất:** thu nhận webcam/video; tìm khuôn mặt; phân tích trạng thái mắt và một số đặc trưng khác; theo dõi liên tiếp theo thời gian; hiển thị trạng thái/độ tin cậy; ghi nhận metadata của sự kiện; cung cấp phương án xem lịch sử trên Dashboard trong giai đoạn sau.

**Yêu cầu phi chức năng:** phản hồi đủ nhanh cho bản demo; không khẳng định kết quả khi thiếu landmarks; xử lý đầu vào lỗi; hạn chế ghi lại hình ảnh cá nhân; có cơ chế xác thực với API cần bảo vệ; ghi log phục vụ kiểm thử và phân tích lỗi.

### 3.5. Đầu vào, đầu ra và phạm vi nghiên cứu

**Đầu vào:** khung hình từ webcam và video mẫu được sử dụng trong môi trường thử nghiệm có sự cho phép. **Đầu ra dự kiến tại Edge:** trạng thái phát hiện khuôn mặt, các đặc trưng EAR/MAR/Head Pose và kết quả theo dõi. **Đầu ra dự kiến lên Cloud:** metadata sự kiện có `event_id`, thời điểm và loại sự kiện, không gửi video.

Việc đánh giá phải xét các trường hợp mắt mở/nhắm, quay đầu, nói chuyện, ánh sáng thay đổi, camera lệch góc và thiếu dữ liệu. Chưa đặt ra chỉ số Accuracy hoặc FPS cụ thể khi chưa có phép đo.

### 3.6. Tổng kết tuần 6

Nội dung tuần 6 tạo nền tảng để chuyển từ nghiên cứu AWS/Generative AI sang bài toán Driver Monitoring. Sản phẩm của giai đoạn này là **phạm vi nghiên cứu và bộ yêu cầu ban đầu**, không phải một hệ thống đã nghiệm thu. Tuần 7 tiếp tục cụ thể hóa luồng xử lý, module Edge AI và kiến trúc AWS Serverless.

## 4. Tài liệu tham khảo

1. [Safety](https://www.nhtsa.gov/risky-driving/drowsy-driving)
2. [Opencv](https://docs.opencv.org/4.x/)
3. [Mediapipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
4. [Python](https://docs.python.org/3/)
5. [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

