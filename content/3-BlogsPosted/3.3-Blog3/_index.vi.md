---
title: "Blog 3"
date: 2026-11-23
weight: 3
---

# AMAZON EVENTBRIDGE SCHEDULER – MỘT DỊCH VỤ NHỎ NHƯNG CÓ VÕ KHI XÂY DỰNG PROJECT TRÊN AWS

Trong quá trình phát triển ứng dụng, có nhiều tác vụ không cần phải thực hiện ngay lập tức mà cần được chạy vào một thời điểm cụ thể hoặc lặp lại theo chu kỳ nhất định. Ví dụ như gửi thông báo nhắc lịch hẹn, cập nhật dữ liệu mỗi 30 phút, xóa các bản ghi hết hạn hoặc kiểm tra trạng thái hệ thống vào cuối ngày.

Nếu sử dụng một máy chủ EC2 để xử lý những tác vụ này, chúng ta cần duy trì máy chủ, cấu hình môi trường và tự quản lý cơ chế lập lịch. Điều này có thể gây lãng phí tài nguyên khi một tác vụ chỉ mất vài giây để hoàn thành.

Để giải quyết vấn đề trên, Amazon Web Services (AWS) cung cấp **Amazon EventBridge Scheduler** – một dịch vụ lập lịch theo mô hình Serverless, cho phép tự động kích hoạt các dịch vụ AWS tại những thời điểm được xác định trước mà không cần duy trì máy chủ riêng.

Trong bài viết này, chúng ta sẽ tìm hiểu cách EventBridge Scheduler hoạt động, các phương pháp lập lịch, những tính năng quan trọng và cách sử dụng dịch vụ để tự động kích hoạt AWS Lambda trong một dự án thực tế.
### 1. Amazon EventBridge Scheduler là gì?

Amazon EventBridge Scheduler là dịch vụ lập lịch do AWS quản lý, cho phép người dùng tạo và quản lý các tác vụ được thực thi một lần tại thời điểm cụ thể hoặc lặp lại theo lịch trình đã thiết lập.

Thay vì phải viết một chương trình liên tục kiểm tra thời gian và gọi API, chúng ta chỉ cần tạo một Schedule, xác định thời điểm thực thi và lựa chọn dịch vụ đích (Target). EventBridge Scheduler sẽ tự động gửi yêu cầu đến dịch vụ đó khi lịch trình được kích hoạt.

Một số dịch vụ AWS có thể được kích hoạt thông qua EventBridge Scheduler bao gồm:

- **AWS Lambda:** Thực thi mã nguồn để xử lý dữ liệu hoặc logic nghiệp vụ.
- **Amazon ECS / AWS Fargate:** Khởi chạy các Container để thực hiện những tác vụ cần nhiều tài nguyên tính toán hơn.
- **AWS Step Functions:** Khởi chạy các Workflow bao gồm nhiều bước xử lý.
- **Amazon SNS:** Gửi thông báo đến những người dùng hoặc hệ thống đã đăng ký nhận thông tin.
- **Amazon SQS:** Đưa các thông điệp vào hàng đợi để xử lý sau.
- **Amazon EventBridge Event Bus:** Phát sự kiện đến các thành phần khác trong hệ thống.

Với tính năng Universal Targets, EventBridge Scheduler có thể gọi hơn 6.000 thao tác API trên hơn 270 dịch vụ AWS. Điều này mang lại khả năng tích hợp linh hoạt với nhiều thành phần khác nhau trong kiến trúc Cloud.

  ![Amazon EventBridge Scheduler architecture](/fcj-workshop-template/images/Flowblog3.jpg)

  Hình 1 - Minh họa cách Amazon EventBridge Scheduler tạo lịch trình và kích hoạt các dịch vụ đích trên AWS.

  [Post Amazon EventBridge Scheduler architecture](https://www.facebook.com/groups/awsstudygroupfcj/posts/2347158249382467/?notif_id=1795445892388748&notif_t=group_post_approved&ref=notif)

### 2. Các loại lịch trình trong EventBridge Scheduler

Một trong những tính năng hữu ích nhất của EventBridge Scheduler là khả năng hỗ trợ nhiều loại lịch trình khác nhau, cho phép nhà phát triển lựa chọn phương pháp phù hợp nhất với yêu cầu của ứng dụng.

**2.1. One-time Schedule**

One-time Schedule cho phép kích hoạt một tác vụ duy nhất tại ngày và giờ đã được chỉ định.

Ví dụ:

- Gửi thông báo nhắc lịch hẹn cho người dùng.
- Tự động gửi thông báo sau 24 giờ kể từ khi người dùng đăng ký tài khoản.
- Kích hoạt một tác vụ vào ngày đơn hàng hết hạn.

Phương pháp này phù hợp với những tác vụ chỉ cần được thực hiện một lần thay vì lặp lại theo chu kỳ.

**2.2. Rate-based Schedule**

Rate-based Schedule cho phép thực thi các tác vụ lặp lại theo những khoảng thời gian cố định.

Ví dụ:

```text
rate(30 minutes)
```

Biểu thức này yêu cầu EventBridge Scheduler kích hoạt dịch vụ đích sau mỗi 30 phút.

Một số trường hợp sử dụng phổ biến bao gồm:

- Cập nhật dữ liệu ứng dụng theo định kỳ.
- Kiểm tra trạng thái hệ thống.
- Tổng hợp dữ liệu theo các khoảng thời gian cố định.
- Tự động đồng bộ thông tin giữa các dịch vụ.

**2.3. Cron-based Schedule**

Cron-based Schedule sử dụng biểu thức Cron để xác định thời điểm thực thi dựa trên phút, giờ, ngày hoặc thứ trong tuần.

Ví dụ:

```text
cron(0 8 ? * MON *)
```

Biểu thức này có nghĩa là tác vụ sẽ được thực thi vào lúc 8 giờ sáng thứ Hai hằng tuần, theo múi giờ đã được cấu hình cho Schedule.

Một tính năng hữu ích khác là khả năng hỗ trợ múi giờ địa phương. Ví dụ:

```text
Asia/Ho_Chi_Minh
```

Điều này cho phép nhà phát triển cấu hình lịch trình theo giờ Việt Nam mà không cần phải chuyển đổi thủ công thời gian thực thi sang UTC.

### 3. Những tính năng nổi bật của EventBridge Scheduler

EventBridge Scheduler không chỉ đơn thuần là một công cụ hẹn giờ. Dịch vụ còn cung cấp các cơ chế tích hợp giúp cải thiện độ tin cậy của hệ thống và giảm công việc vận hành.

**3.1. Không cần duy trì máy chủ (Serverless)**

Đây là một trong những ưu điểm nổi bật nhất khi sử dụng EventBridge Scheduler.

Hãy tưởng tượng một ứng dụng cần thực hiện một tác vụ trong vài giây sau mỗi 30 phút. Nếu sử dụng EC2, máy chủ có thể vẫn phải hoạt động liên tục mặc dù phần lớn thời gian không thực hiện công việc nào.

Với EventBridge Scheduler, AWS chịu trách nhiệm quản lý hạ tầng lập lịch bên dưới. Nhà phát triển chỉ cần cấu hình Schedule và Target mà không phải vận hành máy chủ riêng.

Điều này giúp:

- Giảm các công việc quản trị máy chủ.
- Không cần viết chương trình liên tục kiểm tra thời gian.
- Giảm lượng tài nguyên hạ tầng không được sử dụng.
- Dễ dàng mở rộng khi số lượng lịch trình tăng lên.

**3.2. Retry Policy – Tự động thử lại khi kích hoạt thất bại**

Trong các ứng dụng thực tế, dịch vụ đích có thể tạm thời không khả dụng, gặp tình trạng giới hạn số lượng yêu cầu (Throttling) hoặc không thể xử lý một request.

EventBridge Scheduler hỗ trợ Retry Policy để tự động thử lại khi việc kích hoạt dịch vụ đích thất bại.

Một số giới hạn cấu hình quan trọng bao gồm:

- Thời gian lưu giữ tối đa của một sự kiện chưa được xử lý có thể được cấu hình lên đến 24 giờ.
- Số lần thử lại tối đa có thể được cấu hình lên đến 185 lần.
- Các lần thử lại sử dụng cơ chế Exponential Backoff, tức là tăng dần khoảng thời gian chờ giữa các lần thử.

Cơ chế này giúp hệ thống có thêm cơ hội hoàn thành tác vụ khi dịch vụ đích gặp sự cố tạm thời.

**3.3. Dead-letter Queue (DLQ)**

Nếu Scheduler vẫn không thể gửi sự kiện đến dịch vụ đích sau các lần thử lại đã được cấu hình, nhà phát triển có thể thiết lập một Amazon SQS Queue làm Dead-letter Queue.

Những sự kiện không được gửi thành công sẽ được chuyển đến DLQ để tiếp tục kiểm tra và xử lý.

Ví dụ, một tác vụ gửi thông báo có thể thất bại do Lambda Function tạm thời không khả dụng. Thay vì mất thông tin về sự kiện, dữ liệu của sự kiện đó có thể được lưu trong DLQ để đội ngũ phát triển tìm hiểu nguyên nhân và thực hiện biện pháp xử lý phù hợp.

**3.4. Flexible Time Window**

Hãy tưởng tượng có hàng nghìn lịch trình được cấu hình để chạy vào lúc 12 giờ đêm. Nếu tất cả yêu cầu đều được gửi đến hệ thống đích cùng một thời điểm, hệ thống có thể gặp tình trạng tải tăng đột ngột.

Flexible Time Window cho phép AWS phân bổ các lần kích hoạt trong một khoảng thời gian đã được cấu hình.

Ví dụ, nếu lựa chọn khoảng thời gian linh hoạt là 5 phút, Scheduler có thể kích hoạt dịch vụ đích trong vòng 5 phút sau thời điểm đã lên lịch.

Tính năng này phù hợp với những tác vụ không yêu cầu thực thi vào một thời điểm chính xác tuyệt đối. Nếu tác vụ cần chạy gần với thời điểm đã lên lịch, có thể tắt Flexible Time Window.

**3.5. Hỗ trợ múi giờ và quản lý tập trung**

EventBridge Scheduler cho phép quản lý lịch trình thông qua AWS Management Console, AWS CLI và SDKs.

Người dùng cũng có thể lựa chọn múi giờ địa phương khi tạo Schedule, chẳng hạn `Asia/Ho_Chi_Minh`.

Đối với những dự án có nhiều tác vụ tự động, Schedule Groups có thể được sử dụng để tổ chức các lịch trình theo mục đích:

- `development-schedules`
- `production-schedules`
- `notification-schedules`

Cách tổ chức này giúp việc quản lý và theo dõi lịch trình trở nên dễ dàng hơn khi quy mô dự án tăng lên.

### 4. Ví dụ thực tế: Tự động kích hoạt AWS Lambda mỗi 30 phút

Giả sử dự án của chúng ta có một chức năng thu thập dữ liệu định kỳ. Cứ sau 30 phút, hệ thống cần kích hoạt một Lambda Function để lấy dữ liệu mới và cập nhật vào cơ sở dữ liệu.

Có hai phương pháp có thể áp dụng:

**4.1. Phương pháp truyền thống: Sử dụng EC2 và Crontab**

Nếu sử dụng EC2, chúng ta cần thực hiện các công việc sau:

1. Khởi tạo một EC2 Instance và cấu hình hệ điều hành.
2. Cài đặt môi trường cần thiết như Python, Node.js hoặc AWS CLI.
3. Viết Script để kích hoạt Lambda Function.
4. Cấu hình `crontab` để thực thi Script sau mỗi 30 phút.
5. Quản lý Log, xử lý lỗi và duy trì máy chủ.
6. Gắn IAM Role cho EC2 để cấp quyền kích hoạt Lambda.

Phương pháp này có thể hoạt động, nhưng yêu cầu duy trì máy chủ liên tục ngay cả khi tác vụ thực tế chỉ mất vài giây để hoàn thành.

**4.2. Sử dụng EventBridge Scheduler**

Với EventBridge Scheduler, quy trình trở nên đơn giản hơn và có thể được cấu hình trực tiếp thông qua AWS Management Console.

**Bước 1: Tạo Schedule**

Truy cập AWS Management Console, tìm đến dịch vụ Amazon EventBridge và chọn Scheduler để tạo một Schedule mới.

Chọn Recurring Schedule, sau đó chọn Rate-based Schedule và nhập:

```text
rate(30 minutes)
```

Nếu tác vụ cần chạy theo múi giờ Việt Nam, chọn `Asia/Ho_Chi_Minh` trong phần cấu hình Schedule.

**Bước 2: Lựa chọn Target**

Chọn AWS Lambda làm dịch vụ đích và chỉ định Lambda Function cần được kích hoạt.

**Bước 3: Cấu hình Execution Role**

Tạo hoặc lựa chọn một IAM Execution Role cho phép EventBridge Scheduler kích hoạt Lambda Function.

AWS có thể hỗ trợ tạo Role trong quá trình cấu hình. Tuy nhiên, nhà phát triển cần kiểm tra các quyền được cấp và đảm bảo rằng Role chỉ có những quyền thực sự cần thiết.

**Bước 4: Cấu hình xử lý lỗi**

Tùy theo yêu cầu của dự án, nhà phát triển có thể thiết lập:

- Retry Policy để tự động thử lại khi việc kích hoạt dịch vụ đích thất bại.
- Amazon SQS DLQ để lưu trữ những sự kiện không thể gửi thành công.
- Flexible Time Window khi tác vụ không yêu cầu thực thi tại một thời điểm chính xác tuyệt đối.

Sau khi hoàn thành cấu hình, EventBridge Scheduler sẽ tự động kích hoạt Lambda theo lịch trình đã xác định mà không cần sử dụng một EC2 Instance riêng.

**4.3. Giám sát quá trình thực thi**

Để kiểm tra hệ thống có hoạt động chính xác hay không, nhà phát triển có thể sử dụng:

- **Amazon CloudWatch Metrics:** Theo dõi số lần kích hoạt, số lần kích hoạt thất bại và các chỉ số khác liên quan đến Scheduler.
- **AWS Lambda Monitor:** Kiểm tra số lần Lambda được gọi, thời gian thực thi và các lỗi phát sinh.
- **CloudWatch Logs:** Kiểm tra Log được tạo bởi Lambda Function và những Log của Scheduler đã được cấu hình.
- **Amazon SQS DLQ:** Kiểm tra những sự kiện không thể gửi thành công đến dịch vụ đích.

Việc giám sát thường xuyên giúp phát hiện lỗi sớm và đảm bảo các tác vụ tự động hoạt động theo đúng yêu cầu.

### 5. Những lưu ý quan trọng (Important Considerations)

**5.1. Chi phí và Free Tier**

Theo trang thông tin giá của AWS, EventBridge Scheduler cung cấp tối đa 14 triệu lượt kích hoạt miễn phí mỗi tháng. Sau khi vượt quá mức sử dụng miễn phí, chi phí được tính dựa trên số lượng lượt kích hoạt và AWS Region đang sử dụng.

Đối với các bài thực hành của sinh viên, dự án học thuật và những ứng dụng có số lượng tác vụ lập lịch tương đối nhỏ, mức miễn phí này mang lại nhiều lợi ích trong quá trình thử nghiệm.

Tuy nhiên, nhà phát triển cần lưu ý rằng các dịch vụ đích như Lambda, ECS, SQS và CloudWatch có thể phát sinh chi phí riêng. Vì vậy, không nên mặc định rằng toàn bộ quy trình tự động hóa đều hoàn toàn miễn phí.

**5.2. EventBridge Scheduler và EventBridge Rules**

Trước đây, nhiều nhà phát triển sử dụng EventBridge Rules để tạo các tác vụ chạy theo lịch trình. Tuy nhiên, hai tính năng này phục vụ những mục đích khác nhau:

- **EventBridge Scheduler:** Được thiết kế cho các tác vụ lập lịch độc lập. Dịch vụ hỗ trợ One-time Schedule, Rate-based Schedule và Cron-based Schedule, cùng với Retry Policy, DLQ và Flexible Time Window.
- **EventBridge Rules:** Chủ yếu được thiết kế để lọc các sự kiện trong Event Bus và chuyển những sự kiện phù hợp với Event Pattern đến các dịch vụ đích. Rules cũng hỗ trợ Scheduled Rules.

AWS khuyến nghị sử dụng EventBridge Scheduler cho các yêu cầu lập lịch mới vì dịch vụ cung cấp nhiều tính năng lập lịch chuyên biệt và khả năng mở rộng tốt hơn.

**5.3. Các nguyên tắc bảo mật và vận hành**

- Chỉ cấp những quyền thực sự cần thiết cho IAM Execution Role.
- Không nên tắt Retry Policy và DLQ khi chưa đánh giá mức độ quan trọng của tác vụ.
- Theo dõi CloudWatch Metrics để phát hiện các lần kích hoạt thất bại.
- Xóa hoặc cấu hình tự động xóa những One-time Schedule đã hoàn thành nếu không còn cần thiết.
- Kiểm tra chi phí của cả Scheduler và các dịch vụ đích được kích hoạt.

### 6. Kết luận (Conclusion)

Amazon EventBridge Scheduler là một dịch vụ nhỏ nhưng giải quyết được một vấn đề rất phổ biến trong quá trình phát triển ứng dụng: tự động thực thi các tác vụ theo lịch trình mà không cần duy trì máy chủ riêng.

Nhờ khả năng tích hợp với nhiều dịch vụ AWS, hỗ trợ nhiều phương pháp lập lịch, Retry Policy, Dead-letter Queue và Flexible Time Window, Scheduler giúp đơn giản hóa việc triển khai các quy trình tự động hóa.

Đối với các dự án sinh viên và ứng dụng Serverless, đây là một dịch vụ đáng để tìm hiểu và áp dụng. Thay vì phải tự xây dựng một hệ thống lập lịch từ đầu, nhà phát triển có thể tận dụng dịch vụ do AWS quản lý để giảm thời gian phát triển và tập trung nhiều hơn vào những chức năng cốt lõi của ứng dụng.

Cảm ơn mọi người đã đọc bài viết! Nếu bạn đã từng sử dụng EventBridge Scheduler trong dự án của mình hoặc có kinh nghiệm tối ưu các tác vụ lập lịch trên AWS, hãy cùng chia sẻ những ý kiến và kinh nghiệm thực tế nhé!

### 7. Tài liệu tham khảo (References)

1. **AWS Documentation – What is Amazon EventBridge Scheduler?**
   https://docs.aws.amazon.com/scheduler/latest/UserGuide/what-is-scheduler.html

2. **AWS Documentation – Schedule Types on EventBridge Scheduler**
   https://docs.aws.amazon.com/scheduler/latest/UserGuide/schedule-types.html

3. **AWS Documentation – Getting Started with EventBridge Scheduler**
   https://docs.aws.amazon.com/scheduler/latest/UserGuide/getting-started.html

4. **AWS Documentation – Configuring Flexible Time Windows**
   https://docs.aws.amazon.com/scheduler/latest/UserGuide/managing-schedule-flexible-time-windows.html

5. **AWS Documentation – Managing a Schedule**
   https://docs.aws.amazon.com/scheduler/latest/UserGuide/managing-schedule.html

6. **AWS Pricing – Amazon EventBridge**
   https://aws.amazon.com/eventbridge/pricing/
