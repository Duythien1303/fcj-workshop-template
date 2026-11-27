---
title: "Worklog Tuần 8"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

# Tuần 8: Phát triển các tính năng cốt lõi tại Edge

**Thời gian:** 09/11/2026 – 13/11/2026  
**Trạng thái:** Bản nháp cần đối chiếu nhật ký thực tế

**Lưu ý về tính xác thực:** Lịch theo từng ngày dưới đây là bản phân bổ biên tập dựa trên proposal và tiến độ chung, **chưa phải nhật ký công việc từng ngày đã được xác nhận**. Các nội dung mô tả kết quả không nhằm khẳng định đã hoàn thành toàn bộ chức năng trong đúng tuần này.

## 1. Mục tiêu tuần

- Phát triển và rà soát pipeline xử lý ảnh/video bằng Python, OpenCV và MediaPipe.
- Tích hợp việc phân tích mắt, miệng, Head Pose và các đặc trưng theo thời gian ở phạm vi Backend.
- Nghiên cứu cách kết hợp chỉ số hình học với mô hình phân loại trạng thái mắt như MobileNet.
- Kiểm tra các tình huống gây nhận diện nhầm, lưu dấu vết phân tích bằng CSV và xây dựng bộ kiểm thử cục bộ.
- Phân biệt rõ tính năng đã chạy thử với các phần chưa được xác nhận như Gaze chính thức, cảnh báo hoàn thiện và Cloud production.

## 2. Nội dung công việc

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| Thứ 2 | Rà soát pipeline webcam/video, phát hiện landmarks và đầu ra EAR/MAR. | 09/11/2026 | 09/11/2026 | [OpenCV](https://docs.opencv.org/4.x/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker) |
| Thứ 3 | Khảo sát và thử nghiệm các mô hình phát hiện/phân loại liên quan đến vùng mắt. | 10/11/2026 | 10/11/2026 | [Ultralytics](https://docs.ultralytics.com/), [Python](https://docs.python.org/3/) |
| Thứ 4 | Tích hợp hoặc kiểm tra các trạng thái mắt Open/Half-Open/Closed và cách xử lý hai mắt. | 11/11/2026 | 1/11/2026 | [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [Python](https://docs.python.org/3/) |
| Thứ 5 | Kiểm thử Head Pose trung tính, trạng thái miệng/ngáp và các trường hợp dễ cảnh báo nhầm. | 12/11/2026 | 12/11/2026 | [OpenCV](https://docs.opencv.org/4.x/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker) |
| Thứ 6 | Rà soát luồng phân tích Backend, dữ liệu CSV, kịch bản kiểm thử và tài liệu kỹ thuật. | 13/11/2026 | 13/11/2026 | [FastAPI](https://fastapi.tiangolo.com/), [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/) |

## 3. Kết quả đạt được và nội dung nghiên cứu

### 3.1. Pipeline Camera và Facial Landmarks

Theo tiến độ dự án ghi nhận đến cuối tháng 11, hệ thống đã có pipeline xử lý hình ảnh tại Edge sử dụng webcam, OpenCV và MediaPipe. Các landmarks tạo cơ sở trích xuất đặc trưng mắt, miệng và tư thế đầu.

Phần thực hiện được định hướng chạy trên thiết bị cá nhân, không gửi luồng video lên AWS. Chất lượng landmarks vẫn có thể giảm khi ánh sáng kém, đầu quay mạnh hoặc khuôn mặt bị che.

### 3.2. Phân tích trạng thái mắt và thử nghiệm mô hình

Backend đã được nghiên cứu theo hướng kết hợp **EAR** với mô hình phân loại trạng thái mắt. Các nhãn thử nghiệm gồm **Open, Half-Open, Closed**; việc đánh giá hai mắt độc lập là quan trọng vì mắt trái và mắt phải có thể cho tín hiệu khác nhau.

Đã có quá trình khảo sát YOLOv8n và MobileNet. Một số thử nghiệm YOLOv8n cho kết quả phát hiện không phù hợp với mục tiêu, nên không được ghi nhận là mô hình mắt đạt chất lượng. Việc sử dụng MobileNet còn cần đánh giá trên tập dữ liệu có nhãn đáng tin cậy.

### 3.3. EAR, MAR, Head Pose và Gaze

**EAR** mô tả mức độ mở mắt; **MAR** hỗ trợ nhận diện biểu hiện mở miệng/ngáp; **Head Pose** cung cấp Pitch/Yaw/Roll có thể hiệu chỉnh theo hướng nhìn thẳng. **Gaze Direction** mới mang tính thử nghiệm và chưa được xác nhận đủ tin cậy để làm tiêu chí chính.

Một số kiểm tra cục bộ đã sử dụng các tình huống mắt nhắm lâu, quay đầu, cúi/ngẩng đầu và mở miệng. Những kết quả này có giá trị cho nghiên cứu nhưng chưa chứng minh hiệu quả trong môi trường lái xe thực tế.

### 3.4. Temporal Analysis và kiểm soát cảnh báo nhầm

Các chuỗi đặc trưng có thể được ghi lại để phân tích thay đổi theo thời gian, trong đó CSV giúp kiểm tra quan hệ giữa khung hình, giá trị đặc trưng và trạng thái dự đoán. Hướng tiếp cận ban đầu sử dụng **rule-based candidates**; phần thuật toán thời gian vẫn cần hoàn thiện.

Các trường hợp nói chuyện, hát hoặc mở miệng thông thường có thể gây cảnh báo ngáp nhầm. Vì vậy, cần xem xét thời lượng và diễn biến hình học theo thời gian, không chỉ tăng một ngưỡng MAR. Chưa công bố Precision, Recall hay F1-score khi chưa có tập kiểm thử được chuẩn hóa.

### 3.5. Backend và kiểm thử cục bộ

Trong giai đoạn cuối tháng 11, mã nguồn Backend đã được phát triển theo hướng tổ chức dịch vụ xử lý ảnh/video và các thành phần phân tích trạng thái. FastAPI được sử dụng trong định hướng API/backend, kết hợp tính năng ghi đặc trưng vào CSV để phục vụ kiểm tra.

Các kịch bản cần kiểm tra gồm input sai, không thấy mặt, thiếu landmarks, chênh lệch giữa hai mắt, thay đổi Head Pose và xử lý liên tục nhiều khung hình. Việc tái sử dụng một pipeline chung cho ảnh và video là mục tiêu duy trì tính nhất quán khi mở rộng.

### 3.6. Tổng kết tuần 8

Tiến độ cuối tháng 11 cho thấy **pipeline Edge AI và phần phân tích Backend đã có cơ sở hoạt động cục bộ**, nhưng chất lượng phân loại và cảnh báo vẫn cần đánh giá thêm. Chưa coi Local Event Buffer/Retry, AWS deployment, dashboard, Gaze chính thức hoặc mô hình chuỗi GRU/LSTM/Transformer là đã hoàn thiện. Các công việc này được chuyển sang kế hoạch tích hợp, kiểm thử và tối ưu các tuần tiếp theo.

## 4. Tài liệu tham khảo

1. [Opencv](https://docs.opencv.org/4.x/)
2. [Mediapipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
3. [Ultralytics](https://docs.ultralytics.com/)
4. [Python](https://docs.python.org/3/)
5. [Fastapi](https://fastapi.tiangolo.com/)
6. [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/)

