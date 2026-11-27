---
title: "Worklog Tuần 10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

# Tuần 10: Đánh giá, tối ưu hóa và hoàn thiện hệ thống

**Thời gian:** 23/11/2026 – 27/11/2026  


## 1. Mục tiêu tuần

- Tổng hợp và đánh giá khả năng nhận diện trạng thái mắt, miệng, Head Pose, các tín hiệu thiếu và sự kiện theo thời gian trên dữ liệu kiểm thử có nhãn.
- Phân tích cảnh báo nhầm, điều chỉnh Temporal Analysis và các điều kiện cảnh báo dựa trên kết quả đánh giá, tránh tối ưu theo một video riêng lẻ.
- Đo FPS, thời gian xử lý từng khung hình, độ trễ phản hồi và mức sử dụng tài nguyên trên phần cứng thử nghiệm.
- Rà soát luồng từ camera/video đến kết quả Backend, cảnh báo cục bộ và metadata; ưu tiên sửa lỗi quan trọng và ổn định bản demo.
- Chuẩn hóa mã nguồn, dependencies, hướng dẫn cài đặt/chạy trên Windows, tài liệu pipeline AI và kiểm thử.
- Đối chiếu kiến trúc Edge–AWS với mức độ triển khai thực tế, bổ sung tài liệu quyền truy cập, chi phí, bảo mật và những giới hạn chưa giải quyết.
- Tổng hợp minh chứng, báo cáo đánh giá cuối kỳ và bộ tài liệu bàn giao dự án trong cùng tuần 10.

## 2. Nội dung công việc

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| Thứ 2 | Rà soát mã nguồn và lỗi ưu tiên; chuẩn bị dữ liệu kiểm thử có nhãn cho mắt, miệng, Head Pose và các trường hợp không nhận diện được khuôn mặt. | 23/11/2026 | 23/11/2026 | [Python](https://docs.python.org/3/), [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker), [pytest](https://docs.pytest.org/en/stable/) |
| Thứ 3 | Đánh giá Precision, Recall, F1-score, Confusion Matrix khi có ground truth; phân tích false positive/false negative và temporal rules. | 24/11/2026 | 24/11/2026 | [Scikit-learn](https://scikit-learn.org/stable/modules/model_evaluation.html), [OpenCV](https://docs.opencv.org/4.x/) |
| Thứ 4 | Kiểm tra cảnh báo nhầm và trạng thái không xác định, đo FPS/latency/CPU/RAM; tối ưu có kiểm chứng và kiểm tra lại các đường xử lý chính. | 25/11/2026 | 25/11/2026 | [OpenCV](https://docs.opencv.org/4.x/), [FastAPI](https://fastapi.tiangolo.com/), [pytest](https://docs.pytest.org/en/stable/) |
| Thứ 5 | Ổn định bản demo và chuẩn hóa hướng dẫn cài đặt, requirements, mô hình/thuật toán; đối chiếu mức độ triển khai AWS, quyền truy cập, bảo mật và chi phí. | 26/11/2026 | 26/11/2026 | [Python](https://docs.python.org/3/), [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| Thứ 6 | Tổng hợp kết quả kiểm thử và giới hạn; hoàn thiện báo cáo kỹ thuật, sơ đồ kiến trúc, bằng chứng thực nghiệm và bộ hướng dẫn bàn giao dự án. | 27/11/2026 | 27/11/2026 | [FastAPI Testing](https://fastapi.tiangolo.com/tutorial/testing/), [GitHub Actions](https://docs.github.com/en/actions), [AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) |

## 3. Kết quả dự kiến và nội dung cần triển khai

### 3.1. Chuẩn bị dữ liệu kiểm thử và đánh giá nhận diện

Lựa chọn ảnh/video được phép sử dụng và xây dựng bộ nhãn kiểm thử cho các nhóm trạng thái mắt (Open, Half-Open, Closed), hành vi miệng (nói chuyện, há miệng bình thường, ngáp), Head Pose (nhìn thẳng, quay, nghiêng, cúi/ngẩng) và tình huống mất landmarks. Nhãn gán thủ công cần được đối chiếu nhất quán trước khi dùng làm **ground truth**.

Trên bộ dữ liệu phù hợp, lập **Confusion Matrix**, tính **Precision**, **Recall**, **F1-score** và **Accuracy** theo từng lớp. Khi có nhãn sự kiện, phân biệt đánh giá theo khung hình (frame-level) và theo chuỗi thời gian/sự kiện (event-level). Không gán các tỷ lệ chính xác hoặc thời gian cảnh báo khi chưa có phép đo thực tế.

### 3.2. Phân tích Temporal Analysis và giảm cảnh báo sai

Kiểm tra các tình huống dễ nhầm: chớp mắt bình thường, nói chuyện/hát, mở miệng, khuôn mặt lệch góc, một mắt bị che, chuyển động đầu đột ngột hoặc mất tín hiệu. Đánh giá cách kết hợp EAR, MAR, Head Pose, phân loại trạng thái mắt và dữ liệu qua nhiều khung hình.

So sánh các phương án ngưỡng, cửa sổ thời gian, thời lượng liên tục và xử lý **Unknown/Uncertain State**. Chỉ điều chỉnh quy tắc khi có bằng chứng từ nhiều tình huống kiểm thử; Gaze vẫn được ghi nhận là tính năng thử nghiệm nếu chưa đủ kiểm chứng.

### 3.3. Đo hiệu năng và ổn định bản demo

Thực hiện đo trên phần cứng thử nghiệm: **FPS**, thời gian xử lý từng khung hình, độ trễ end-to-end từ camera đến kết quả/cảnh báo, mức sử dụng CPU/RAM và điều kiện ghi hình. Cần tách thời gian suy luận mô hình khỏi độ trễ toàn pipeline, đồng thời ghi rõ độ phân giải video và phiên bản code/model.

Rà soát luồng **camera/video → OpenCV/MediaPipe → trích xuất đặc trưng/mô hình → Temporal Analysis → Backend output/cảnh báo cục bộ**. Kiểm tra input sai, không phát hiện khuôn mặt, landmarks thiếu, dữ liệu mô hình không nhất quán và các lần chạy lặp lại. Ưu tiên độ ổn định thay vì bổ sung tính năng chưa kiểm thử.

Nếu cảnh báo cục bộ hoặc đồng bộ Cloud còn chưa hoàn chỉnh, cần nêu đúng trạng thái và giới hạn khi trình diễn.

### 3.4. Chuẩn hóa môi trường và hướng dẫn vận hành

Chuẩn bị tài liệu về cấu trúc repository, phiên bản Python, file `requirements.txt`, cách tạo môi trường ảo trên Windows, lệnh khởi chạy Backend và quy trình sử dụng nguồn webcam/video. Mô tả cách chạy test, xem log/CSV, khắc phục lỗi thường gặp và tái tạo môi trường chạy trên một máy mới.

Bộ bàn giao chỉ nên chứa mã nguồn, cấu hình mẫu không nhạy cảm, dữ liệu thử nghiệm có quyền sử dụng, model/checkpoint được phép chia sẻ và các hướng dẫn cần thiết. Không đóng gói `.venv`, `__pycache__`, mật khẩu, token, API key hoặc video khuôn mặt riêng tư.

### 3.5. Tài liệu thuật toán và bằng chứng đánh giá

Mô tả các thành phần **OpenCV**, **MediaPipe**, **EAR**, **MAR**, **Head Pose**, mô hình phân loại mắt (ví dụ MobileNet nếu có trong bản bàn giao), phân tích theo thời gian, điều kiện phát sự kiện và các trạng thái cảnh báo. Đối với mọi chỉ số đánh giá cần chỉ rõ bộ dữ liệu, phương pháp đo, thiết bị, phiên bản mô hình và mã nguồn tương ứng.

Tổng hợp các trường hợp đã xử lý tốt, các lỗi còn xuất hiện, thay đổi trước/sau tối ưu và những giới hạn như ánh sáng kém, kính mắt, góc quay hoặc tín hiệu Gaze chưa đủ ổn định. Không suy rộng kết quả thử nghiệm trong môi trường đứng yên thành hiệu quả an toàn khi lái xe thật.

### 3.6. Đối chiếu kiến trúc AWS và bảo mật

Tổng hợp sơ đồ **Edge AI + AWS Cloud**, định dạng **event metadata**, cơ chế Local Event Buffer/Retry, API Gateway, Lambda Writer/Reader, DynamoDB, Cognito/JWT, S3 Private + CloudFront OAC, CloudWatch, IAM và AWS Budgets theo proposal.

Với từng dịch vụ hoặc luồng tích hợp, phân loại rõ: **đã triển khai và kiểm thử**, **đã thiết kế nhưng chưa triển khai**, hoặc **chưa xác minh**. Xác nhận nguyên tắc video gốc không được đưa lên Cloud; kiểm soát việc xuất bản token/khóa bí mật trong log và tài liệu. Chỉ đưa con số chi phí khi có cấu hình, lượng sử dụng và nguồn giá hợp lệ.

### 3.7. Tổng kết dự án và chuẩn bị bàn giao

Các đầu ra dự kiến của tuần 10 gồm:

- Bảng kết quả kiểm thử, các trường hợp lỗi và độ tin cậy của nhãn.
- Báo cáo hiệu năng, so sánh trước/sau điều chỉnh và danh sách hạn chế còn lại.
- Bản demo có hướng dẫn chạy và phạm vi chức năng được xác nhận.
- README, tài liệu kiến trúc Edge–Cloud, mô tả pipeline AI và điều kiện cảnh báo.
- Hướng dẫn cài đặt, dependencies, test, danh sách model/checkpoint hợp lệ và dữ liệu mẫu.
- Báo cáo trung thực về tình trạng AWS, các rủi ro còn tồn đọng và công việc cần phát triển tiếp.
- Nội dung tổng kết thực tập FCAJ, kết quả học tập và kinh nghiệm rút ra.

Bộ bàn giao cần giúp người khác có thể thiết lập và kiểm tra dự án mà không phụ thuộc vào môi trường riêng của người phát triển. **Tuần 10 là tuần cuối của Worklog**, đồng thời hoàn tất nội dung tổng kết và chuẩn bị bàn giao dự án.

**Trạng thái tại ngày soạn:** toàn bộ phần này là kế hoạch thực hiện và kết quả mong đợi của tuần 10. Chỉ cập nhật thành kết quả đã hoàn thành khi có minh chứng thực tế.

## 4. Tài liệu tham khảo

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
