---
title: "Worklog Tuần 9"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

# Tuần 9: Tích hợp hệ thống và kiểm thử

**Thời gian:** 16/11/2026 – 20/11/2026  
**Trạng thái:** Kế hoạch dự kiến

## 1. Mục tiêu tuần

- Hoàn thiện kết nối giữa kết quả phân tích tại Edge và cấu trúc metadata sự kiện.
- Triển khai thử Local Event Buffer/Retry nếu phạm vi và thời gian cho phép; kiểm tra các tình huống mất mạng.
- Thiết kế và kiểm thử API tiếp nhận sự kiện, các điều kiện xác thực/ghi trùng và đường đọc lịch sử trên môi trường được cấp quyền.
- Chuẩn hóa bộ kiểm thử Backend cho dữ liệu ảnh, video và trạng thái không xác định.
- Ghi lại bằng chứng thực nghiệm, tách rõ phần đã chạy được và phần còn chỉ ở mức thiết kế.

## 2. Nội dung công việc

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| Thứ 2 | Rà soát dữ liệu đầu ra Edge; thống nhất cấu trúc event_id, timestamp, event type và trạng thái. | 16/11/2026 | 16/11/2026 | [Python](https://docs.python.org/3/), [FastAPI](https://fastapi.tiangolo.com/) |
| Thứ 3 | Xây dựng hoặc mô phỏng Local Event Buffer và kiểm tra retry sau khi gửi thất bại. | 17/11/2026 | 17/11/2026 | [Python](https://docs.python.org/3/), [pytest](https://docs.pytest.org/en/stable/) |
| Thứ 4 | Thiết lập thử luồng API Gateway → Lambda Event Writer → DynamoDB nếu có tài khoản/quyền. | 18/11/2026 | 18/11/2026 | [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html), [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html), [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html) |
| Thứ 5 | Kiểm thử trùng event_id, payload sai, mất mạng và quyền truy cập vào API. | 19/11/2026 | 19/11/2026 | [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html), [JWT Authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html), [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/) |
| Thứ 6 | Tổng hợp test cases, log và báo cáo mức độ tích hợp thực tế. | 20/11/2026 | 20/11/2026 | [Cloudwatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html), [pytest](https://docs.pytest.org/en/stable/) |

## 3. Kết quả dự kiến và nội dung cần triển khai

### 3.1. Kế hoạch chuẩn hóa Event Metadata

Xác định schema sự kiện gồm `event_id`, `timestamp`, `event_type`, `state` và các trường bổ sung được phép lưu theo chính sách dữ liệu. Metadata nên có kiểu dữ liệu và quy tắc kiểm tra rõ ràng; video gốc không nằm trong payload.

Cần kiểm tra thời điểm tạo event_id để nhiều lần gửi lại cùng một sự kiện không bị xem là sự kiện mới.

### 3.2. Kế hoạch Local Event Buffer và Retry

Thiết kế hàng đợi cục bộ cho các event chưa đồng bộ; chỉ đánh dấu `synced` khi server xác nhận thành công. Khi kết nối gián đoạn, quá trình phân tích Edge vẫn tiếp tục, còn event được giữ lại để gửi sau.

Bộ kiểm thử dự kiến gồm mất mạng trước khi gửi, timeout, retry lặp, ứng dụng khởi động lại và mất/khôi phục kết nối. Cơ chế này **chưa được coi là hoàn thành trước khi có kết quả test**.

### 3.3. Kế hoạch kiểm thử AWS Backend

Đối với môi trường AWS có quyền sử dụng, kiểm tra HTTP API, Lambda Writer, DynamoDB Conditional PutItem, Lambda Reader và JWT Authorizer theo đúng kiến trúc. Các trường hợp quan trọng: payload hợp lệ, thiếu trường, event_id trùng, token thiếu/sai và truy vấn ngoài phạm vi được phép.

Nếu chưa triển khai Cloud, cần ghi rõ là **thiết kế và kịch bản kiểm thử**, không tạo log hay kết quả giả.

### 3.4. Kiểm thử pipeline ảnh/video

Dùng video mẫu hoặc webcam trong môi trường đứng yên để so sánh luồng xử lý ảnh và video: khả năng tìm mặt, thiếu landmarks, trạng thái hai mắt không đồng nhất, sự kiện miệng và Head Pose. Kiểm tra mã lỗi, dữ liệu CSV và độ ổn định khi xử lý liên tiếp nhiều khung hình.

Không sử dụng bản thử nghiệm như thiết bị cảnh báo an toàn đã được kiểm định.

### 3.5. Kết quả dự kiến và tiêu chí nghiệm thu

Kết quả kỳ vọng: có schema sự kiện nhất quán, bộ test tích hợp có thể tái chạy, log/bằng chứng cho từng trường hợp và danh sách lỗi cần xử lý. Chỉ đánh dấu chức năng hoàn thành khi đã chạy thành công và lưu được bằng chứng tương ứng.

**Trạng thái tại ngày soạn:** đây là nội dung kế hoạch cho tuần 9, không phải kết quả đã đạt được.

## 4. Tài liệu tham khảo

1. [Python](https://docs.python.org/3/)
2. [Fastapi](https://fastapi.tiangolo.com/)
3. [Pytest](https://docs.pytest.org/en/stable/)
4. [Apig](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
5. [Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
6. [Dynamo Cond](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html)
7. [JWT](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html)
8. [Fastapi Testing](https://fastapi.tiangolo.com/tutorial/testing/)

