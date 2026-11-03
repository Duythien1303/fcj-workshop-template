---
title: "Worklog Tuần 4"
date: 2026-10-26
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---



### Mục tiêu tuần 4

- Tìm hiểu tổng quan về kiến trúc Serverless Computing và vai trò của Serverless trong phát triển ứng dụng trên AWS.
- Nắm được những khái niệm cơ bản về AWS Lambda và cách thực thi mã nguồn mà không cần trực tiếp quản lý máy chủ.
- Nghiên cứu các thành phần quan trọng của AWS Lambda như Function, Runtime, Trigger, Event và Execution Role.
- Tìm hiểu Amazon API Gateway và cách xây dựng các API phục vụ giao tiếp giữa ứng dụng với hệ thống Backend.
- Nghiên cứu Amazon CloudWatch để theo dõi hoạt động, thu thập Logs và giám sát hiệu suất ứng dụng.
- Tìm hiểu cách AWS IAM được sử dụng để quản lý quyền truy cập giữa các dịch vụ AWS.
- Làm quen với quy trình thiết kế, triển khai và kiểm thử một ứng dụng Serverless cơ bản.
- Xây dựng nền tảng kiến thức về Application Deployment để phục vụ việc phát triển Project cuối kỳ thực tập.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| 2 | - Tìm hiểu tổng quan về Serverless Computing và các đặc điểm của kiến trúc Serverless. <br> - So sánh mô hình Serverless với phương pháp triển khai ứng dụng truyền thống. <br> - Nghiên cứu AWS Lambda và những trường hợp sử dụng phổ biến. <br> - Tìm hiểu các khái niệm Function, Runtime, Event và Trigger. | 26/10/2026 | 26/10/2026 | [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| 3 | - Nghiên cứu kiến trúc và nguyên lý hoạt động của AWS Lambda. <br> - Tìm hiểu Lambda Execution Role và quyền truy cập thông qua AWS IAM. <br> - Nghiên cứu cách AWS Lambda xử lý các sự kiện và thực thi Function. <br> - Tìm hiểu quy trình tạo và kiểm thử Lambda Function bằng Python. <br> - Thực hành với môi trường AWS được cấp quyền nếu có. | 27/10/2026 | 27/10/2026 | [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) |
| 4 | - Tìm hiểu Amazon API Gateway và vai trò của API trong hệ thống phần mềm. <br> - Nghiên cứu REST API, HTTP Method và HTTP Status Code. <br> - Tìm hiểu cách kết nối API Gateway với AWS Lambda. <br> - Nghiên cứu quy trình tiếp nhận HTTP Request và trả về HTTP Response. <br> - Tìm hiểu cách thiết kế một REST API Serverless đơn giản. | 28/10/2026 | 28/10/2026 | [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| 5 | - Tìm hiểu Amazon CloudWatch và các chức năng giám sát ứng dụng. <br> - Nghiên cứu CloudWatch Logs, Metrics và Alarms. <br> - Tìm hiểu cách theo dõi thời gian thực thi, số lần gọi Function và các lỗi trong AWS Lambda. <br> - Nghiên cứu cách sử dụng CloudWatch Logs để hỗ trợ phát hiện và xử lý lỗi. <br> - Tìm hiểu các nguyên tắc bảo mật và quản lý chi phí khi sử dụng dịch vụ Serverless. | 29/10/2026 | 29/10/2026 | [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) |
| 6 | - Tổng hợp kiến thức về AWS Lambda, API Gateway và CloudWatch. <br> - Thiết kế sơ đồ kiến trúc ứng dụng Serverless cơ bản. <br> - Tìm hiểu quy trình tích hợp Lambda với API Gateway. <br> - Xây dựng hoặc mô phỏng một API đơn giản để kiểm tra cơ chế xử lý Request và Response. <br> - Tổng kết kiến thức tuần 4 và chuẩn bị nghiên cứu Generative AI trên AWS cho tuần 5. | 30/10/2026 | 30/10/2026 | [AWS Serverless](https://aws.amazon.com/serverless/) <br> [AWS Workshops](https://catalog.workshops.aws/) |

### Kết quả đạt được tuần 4

#### 1. Kiến thức tổng quan về Serverless Computing

- Tìm hiểu được khái niệm Serverless Computing và vai trò của mô hình này trong phát triển ứng dụng hiện đại.
- Hiểu rằng Serverless cho phép lập trình viên tập trung vào việc phát triển và vận hành mã nguồn ứng dụng mà không cần trực tiếp quản lý toàn bộ hạ tầng máy chủ.
- Nắm được những đặc điểm nổi bật của kiến trúc Serverless:

  - **Automatic Scaling:** Tài nguyên có thể tự động điều chỉnh để đáp ứng nhu cầu xử lý của ứng dụng.

  - **Event-Driven Architecture:** Các chức năng được kích hoạt và thực thi dựa trên những sự kiện cụ thể.

  - **Managed Infrastructure:** Nhà cung cấp dịch vụ Cloud chịu trách nhiệm quản lý nhiều thành phần của hạ tầng.

  - **Pay-per-use:** Chi phí được tính dựa trên mô hình sử dụng tài nguyên của từng dịch vụ.

- Hiểu được sự khác biệt giữa Serverless và phương pháp triển khai ứng dụng truyền thống.
- Nhận biết những trường hợp sử dụng phù hợp với kiến trúc Serverless, chẳng hạn xử lý API, xử lý dữ liệu và tự động hóa quy trình.

#### 2. Kiến thức về AWS Lambda

- Nắm được khái niệm AWS Lambda và vai trò của dịch vụ này trong việc thực thi mã nguồn theo mô hình Serverless.
- Tìm hiểu các thành phần cơ bản:

  - **Lambda Function:** Đơn vị mã nguồn được triển khai và thực thi trên AWS Lambda.

  - **Runtime:** Môi trường thực thi mã nguồn, hỗ trợ các ngôn ngữ lập trình và phiên bản tương thích.

  - **Event:** Dữ liệu hoặc thông tin được cung cấp khi Function được gọi.

  - **Trigger:** Thành phần hoặc dịch vụ có thể kích hoạt quá trình thực thi Function.

  - **Execution Role:** IAM Role cung cấp các quyền cần thiết cho Lambda Function khi truy cập tài nguyên AWS.

- Nghiên cứu quy trình hoạt động của AWS Lambda:

  1. Một sự kiện hoặc yêu cầu được gửi đến Lambda Function.
  2. AWS Lambda tiếp nhận yêu cầu và chuẩn bị môi trường thực thi khi cần.
  3. Function xử lý dữ liệu đầu vào dựa trên mã nguồn đã được triển khai.
  4. Kết quả xử lý được trả về hoặc chuyển đến thành phần liên quan.
  5. Thông tin thực thi có thể được ghi nhận để hỗ trợ giám sát và xử lý lỗi.

- Hiểu được vai trò của AWS Lambda trong việc xây dựng Backend cho các ứng dụng hiện đại.
- Làm quen với cấu trúc Lambda Function sử dụng ngôn ngữ Python.

#### 3. Kiến thức về Amazon API Gateway

- Tìm hiểu Amazon API Gateway là dịch vụ hỗ trợ tạo, quản lý, triển khai và bảo vệ các API.
- Hiểu vai trò của API Gateway trong việc kết nối Client với các dịch vụ Backend.
- Nắm được những khái niệm cơ bản:

  - **REST API:** Kiểu kiến trúc API cho phép các hệ thống trao đổi dữ liệu thông qua HTTP.

  - **API Endpoint:** Địa chỉ cho phép ứng dụng gửi yêu cầu đến API.

  - **HTTP Request:** Yêu cầu được gửi từ Client đến Server hoặc API.

  - **HTTP Response:** Phản hồi được gửi lại sau khi yêu cầu được xử lý.

  - **HTTP Methods:** Các phương thức phổ biến như GET, POST, PUT và DELETE.

  - **HTTP Status Codes:** Mã trạng thái thể hiện kết quả xử lý yêu cầu, chẳng hạn 200, 400, 404 và 500.

- Nghiên cứu cơ chế tích hợp giữa Amazon API Gateway và AWS Lambda.
- Hiểu cách API Gateway tiếp nhận yêu cầu HTTP và chuyển dữ liệu đến Lambda Function để xử lý.
- Tìm hiểu cách xây dựng một API đơn giản phục vụ các ứng dụng Web hoặc Mobile.

#### 4. Kiến thức về Amazon CloudWatch

- Nắm được khái niệm Amazon CloudWatch và vai trò của dịch vụ trong việc giám sát các ứng dụng, tài nguyên và dịch vụ trên AWS.
- Tìm hiểu các thành phần chính:

  - **CloudWatch Logs:** Thu thập, lưu trữ và phân tích thông tin Log từ ứng dụng và dịch vụ.

  - **CloudWatch Metrics:** Cung cấp các số liệu phục vụ việc theo dõi hoạt động và hiệu suất hệ thống.

  - **CloudWatch Alarms:** Theo dõi các chỉ số và thực hiện những hành động được cấu hình khi điều kiện cảnh báo được đáp ứng.

  - **CloudWatch Dashboards:** Hiển thị và tổng hợp các chỉ số giám sát dưới dạng giao diện trực quan.

- Tìm hiểu các chỉ số quan trọng của AWS Lambda:

  - **Invocations:** Số lần Lambda Function được gọi.

  - **Duration:** Thời gian thực thi Function.

  - **Errors:** Số lần thực thi gặp lỗi.

  - **Throttles:** Số lần yêu cầu thực thi bị giới hạn do các ràng buộc về khả năng xử lý đồng thời.

- Hiểu được cách CloudWatch hỗ trợ phát hiện sự cố, theo dõi hiệu suất và đánh giá hoạt động của ứng dụng.

#### 5. Kiến thức về IAM và bảo mật trong Serverless

- Tìm hiểu vai trò của AWS Identity and Access Management (IAM) trong việc kiểm soát quyền truy cập giữa các dịch vụ.
- Hiểu được cách Lambda Execution Role xác định những tài nguyên mà Lambda Function được phép truy cập.
- Nghiên cứu nguyên tắc Least Privilege trong quá trình cấp quyền cho ứng dụng.
- Nhận thức được tầm quan trọng của việc:

  - Chỉ cấp những quyền thực sự cần thiết cho Function.
  - Bảo vệ thông tin đăng nhập và các dữ liệu nhạy cảm.
  - Kiểm soát truy cập đối với các API.
  - Theo dõi hoạt động ứng dụng thông qua Logs.
  - Giám sát mức sử dụng tài nguyên và chi phí dịch vụ.

#### 6. Tìm hiểu quy trình xây dựng ứng dụng Serverless

- Nắm được mô hình kiến trúc Serverless cơ bản sử dụng Amazon API Gateway, AWS Lambda và Amazon CloudWatch.
- Hiểu quy trình xử lý yêu cầu của ứng dụng:

  1. Client gửi HTTP Request đến API Endpoint.
  2. Amazon API Gateway tiếp nhận và định tuyến yêu cầu.
  3. API Gateway gọi Lambda Function được tích hợp.
  4. Lambda Function thực hiện xử lý dữ liệu.
  5. Kết quả xử lý được chuyển về API Gateway.
  6. API Gateway trả HTTP Response về Client.
  7. Thông tin hoạt động được ghi nhận trong hệ thống giám sát nếu đã cấu hình phù hợp.

- Tìm hiểu các thành phần cần thiết để xây dựng một REST API đơn giản.
- Làm quen với quy trình kiểm thử API thông qua các công cụ gửi HTTP Request.
- Hiểu vai trò của việc kiểm tra kết quả, xử lý lỗi và theo dõi Log trong quá trình phát triển ứng dụng.

#### 7. So sánh các dịch vụ AWS Serverless và Monitoring

| Dịch vụ | Chức năng chính | Vai trò trong ứng dụng |
|---|---|---|
| **AWS Lambda** | Thực thi mã nguồn theo mô hình Serverless | Xử lý logic Backend |
| **Amazon API Gateway** | Tạo và quản lý API | Tiếp nhận và định tuyến các yêu cầu từ Client |
| **Amazon CloudWatch** | Giám sát tài nguyên và ứng dụng | Theo dõi Metrics, Logs và cảnh báo |
| **AWS IAM** | Quản lý danh tính và quyền truy cập | Kiểm soát quyền giữa các dịch vụ và tài nguyên AWS |

Thông qua việc tìm hiểu các dịch vụ trên, em hiểu rõ hơn cách những thành phần AWS có thể phối hợp để xây dựng một hệ thống Backend đơn giản mà không cần trực tiếp quản lý máy chủ.

#### 8. Tổng kết tuần 4

Trong tuần thứ tư, nội dung nghiên cứu tập trung vào kiến trúc **Serverless Computing** và các dịch vụ hỗ trợ xây dựng, triển khai và giám sát ứng dụng trên Amazon Web Services.

Thông qua việc nghiên cứu AWS Lambda, em hiểu rõ hơn mô hình thực thi mã nguồn dựa trên sự kiện và những lợi ích của việc sử dụng dịch vụ tính toán được quản lý.

Bên cạnh đó, việc tìm hiểu Amazon API Gateway giúp em nắm được cách xây dựng giao diện giao tiếp giữa Client và Backend thông qua các phương thức HTTP.

Việc nghiên cứu Amazon CloudWatch và AWS IAM cũng giúp em nhận thức được tầm quan trọng của việc giám sát hệ thống, xử lý lỗi, bảo mật và quản lý quyền truy cập trong quá trình phát triển ứng dụng Cloud.

Ngoài các kiến thức lý thuyết, việc tìm hiểu mô hình tích hợp API Gateway với Lambda giúp em có cái nhìn tổng quan hơn về quy trình xây dựng một ứng dụng Serverless từ khâu thiết kế đến kiểm thử.

Những kiến thức nghiên cứu trong tuần 4 là nền tảng để tiếp tục tìm hiểu **Generative AI, Large Language Models (LLMs), AI Agents và Amazon Bedrock** trong tuần thực tập thứ 5, đồng thời chuẩn bị cho giai đoạn nghiên cứu và phát triển Project cuối kỳ.

