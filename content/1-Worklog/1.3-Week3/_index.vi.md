---
title: "Worklog Tuần 3"
date: 2026-10-05
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---


### Mục tiêu tuần 3

- Tìm hiểu tổng quan về các phương pháp lưu trữ và quản lý dữ liệu trên nền tảng Amazon Web Services (AWS).
- Nắm được sự khác biệt giữa ba mô hình lưu trữ phổ biến: Object Storage, Block Storage và File Storage.
- Nghiên cứu các dịch vụ lưu trữ của AWS, bao gồm Amazon Simple Storage Service (Amazon S3), Amazon Elastic Block Store (Amazon EBS) và Amazon Elastic File System (Amazon EFS).
- Tìm hiểu những kiến thức cơ bản về cơ sở dữ liệu quan hệ (Relational Database) và cơ sở dữ liệu phi quan hệ (NoSQL Database).
- Nghiên cứu Amazon Relational Database Service (Amazon RDS) và Amazon DynamoDB.
- Tìm hiểu các phương pháp bảo vệ dữ liệu, kiểm soát quyền truy cập và sao lưu dữ liệu trên AWS.
- Làm quen với quy trình quản lý dữ liệu thông qua AWS Management Console.
- Xây dựng nền tảng kiến thức về Storage và Database để phục vụ việc triển khai các ứng dụng Cloud và AI trong những tuần tiếp theo.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| 2 | - Tìm hiểu tổng quan về Storage trong Cloud Computing. <br> - Phân biệt Object Storage, Block Storage và File Storage. <br> - Nghiên cứu Amazon S3 và các khái niệm Bucket, Object, Key và Storage Class. <br> - Tìm hiểu những trường hợp sử dụng Amazon S3 trong thực tế. | 05/10/2026 | 05/10/2026 | [Amazon S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html) |
| 3 | - Nghiên cứu các tính năng của Amazon S3. <br> - Tìm hiểu S3 Versioning, Lifecycle Rules và Bucket Policies. <br> - Nghiên cứu các phương pháp quản lý quyền truy cập và bảo vệ dữ liệu trên S3. <br> - Tìm hiểu quy trình tạo S3 Bucket, upload, download và quản lý Object. <br> - Thực hành các thao tác S3 cơ bản nếu có môi trường được cấp quyền. | 06/10/2026 | 06/10/2026 | [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) |
| 4 | - Tìm hiểu Amazon Elastic Block Store (EBS) và vai trò của EBS đối với Amazon EC2. <br> - Nghiên cứu EBS Volume, Snapshot và các loại EBS Volume phổ biến. <br> - Tìm hiểu Amazon Elastic File System (EFS). <br> - So sánh Amazon S3, EBS và EFS về phương pháp lưu trữ, khả năng sử dụng và các tình huống triển khai. | 07/10/2026 | 07/10/2026 | [Amazon EBS](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html) <br> [Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html) |
| 5 | - Tìm hiểu tổng quan về Database trong Cloud Computing. <br> - Phân biệt Relational Database và NoSQL Database. <br> - Nghiên cứu Amazon RDS, các hệ quản trị cơ sở dữ liệu được hỗ trợ và những tính năng quản lý cơ bản. <br> - Tìm hiểu Amazon DynamoDB và mô hình lưu trữ dữ liệu NoSQL. <br> - So sánh Amazon RDS và DynamoDB về cấu trúc dữ liệu, khả năng mở rộng và trường hợp sử dụng. | 08/10/2026 | 08/10/2026 | [Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) <br> [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| 6 | - Tổng hợp kiến thức về các dịch vụ AWS Storage và Database đã nghiên cứu. <br> - Tìm hiểu quy trình sao lưu và phục hồi dữ liệu, bao gồm S3 Versioning, EBS Snapshot và RDS Backup. <br> - Nghiên cứu những nguyên tắc bảo mật dữ liệu và quản lý quyền truy cập. <br> - Xây dựng bảng so sánh Amazon S3, EBS, EFS, RDS và DynamoDB. <br> - Tổng kết kiến thức tuần 3 và chuẩn bị nghiên cứu AWS Serverless cho tuần 4. | 09/10/2026 | 09/10/2026 | [AWS Documentation](https://docs.aws.amazon.com/) |

### Kết quả đạt được tuần 3

#### 1. Kiến thức tổng quan về Cloud Storage

- Tìm hiểu được vai trò của các dịch vụ lưu trữ trong việc quản lý và xử lý dữ liệu trên nền tảng điện toán đám mây.
- Phân biệt được ba phương pháp lưu trữ cơ bản:

  - **Object Storage:** Lưu trữ dữ liệu dưới dạng Object, phù hợp với hình ảnh, video, tài liệu, dữ liệu phi cấu trúc và các ứng dụng cần khả năng mở rộng.

  - **Block Storage:** Lưu trữ dữ liệu dưới dạng các khối dữ liệu, thường được sử dụng làm ổ đĩa cho máy chủ và hệ thống cần truy cập dữ liệu ở cấp Block.

  - **File Storage:** Lưu trữ dữ liệu theo cấu trúc thư mục và tệp, hỗ trợ việc truy cập và chia sẻ dữ liệu giữa nhiều hệ thống.

- Hiểu được những đặc điểm cơ bản của từng phương pháp và các tình huống sử dụng phù hợp.

#### 2. Kiến thức về Amazon Simple Storage Service (Amazon S3)

- Nắm được khái niệm Amazon S3 và vai trò của dịch vụ này trong việc lưu trữ dữ liệu dưới dạng Object.
- Tìm hiểu các thành phần cơ bản của Amazon S3:

  - **Bucket:** Vùng chứa dùng để lưu trữ các Object.

  - **Object:** Đơn vị dữ liệu được lưu trữ trong Amazon S3.

  - **Object Key:** Tên định danh của một Object trong Bucket.

  - **Storage Class:** Các lớp lưu trữ được thiết kế phù hợp với những nhu cầu truy cập và chi phí khác nhau.

- Tìm hiểu các tính năng quan trọng:

  - **S3 Versioning:** Quản lý các phiên bản khác nhau của Object.

  - **S3 Lifecycle Rules:** Tự động chuyển đổi lớp lưu trữ hoặc hết hạn Object dựa trên những quy tắc đã được thiết lập.

  - **Bucket Policies:** Quản lý quyền truy cập vào các tài nguyên trong S3 Bucket.

  - **S3 Encryption:** Hỗ trợ bảo vệ dữ liệu được lưu trữ thông qua các phương pháp mã hóa.

- Hiểu được quy trình cơ bản để tạo Bucket, upload, download và quản lý Object thông qua AWS Management Console.
- Nhận thức được tầm quan trọng của việc cấu hình quyền truy cập phù hợp và hạn chế công khai dữ liệu không cần thiết.

#### 3. Kiến thức về Amazon EBS và Amazon EFS

**Amazon Elastic Block Store (EBS)**

- Tìm hiểu Amazon EBS là dịch vụ Block Storage được sử dụng phổ biến với Amazon EC2.
- Nắm được các khái niệm:

  - **EBS Volume:** Thiết bị lưu trữ dạng Block có thể gắn vào EC2 Instance tương thích.

  - **EBS Snapshot:** Bản sao lưu dữ liệu của EBS Volume, phục vụ mục đích bảo vệ và phục hồi dữ liệu.

  - **Volume Types:** Các loại Volume được tối ưu cho những yêu cầu về hiệu năng và chi phí khác nhau.

- Hiểu được vai trò của EBS trong việc cung cấp khả năng lưu trữ dữ liệu bền vững cho các ứng dụng chạy trên EC2.

**Amazon Elastic File System (EFS)**

- Nắm được khái niệm Amazon EFS và vai trò của dịch vụ này trong việc cung cấp hệ thống File Storage được quản lý trên AWS.
- Tìm hiểu khả năng chia sẻ dữ liệu giữa nhiều tài nguyên tính toán tương thích.
- Hiểu được một số trường hợp sử dụng EFS trong các ứng dụng cần hệ thống tệp dùng chung.

#### 4. Kiến thức về Amazon RDS

- Hiểu được khái niệm cơ sở dữ liệu quan hệ và phương pháp tổ chức dữ liệu dưới dạng bảng.
- Nắm được vai trò của Amazon Relational Database Service (RDS) trong việc hỗ trợ triển khai và quản lý cơ sở dữ liệu quan hệ trên AWS.
- Tìm hiểu một số hệ quản trị cơ sở dữ liệu được Amazon RDS hỗ trợ:

  - MySQL.
  - PostgreSQL.
  - MariaDB.
  - Microsoft SQL Server.
  - Oracle Database.

- Nghiên cứu các tính năng cơ bản của Amazon RDS:

  - **Automated Backups:** Tự động sao lưu dữ liệu theo cấu hình.

  - **Multi-AZ Deployment:** Hỗ trợ tăng tính sẵn sàng và khả năng phục hồi của cơ sở dữ liệu.

  - **Read Replicas:** Hỗ trợ mở rộng khả năng xử lý các truy vấn đọc đối với những engine và cấu hình được hỗ trợ.

  - **Monitoring:** Theo dõi các chỉ số hoạt động và hiệu suất của cơ sở dữ liệu.

- Nhận thức được vai trò của cơ sở dữ liệu quan hệ trong các ứng dụng cần quản lý dữ liệu có cấu trúc và đảm bảo tính nhất quán.

#### 5. Kiến thức về Amazon DynamoDB

- Tìm hiểu Amazon DynamoDB là dịch vụ cơ sở dữ liệu NoSQL được quản lý hoàn toàn bởi AWS.
- Nắm được những đặc điểm cơ bản của DynamoDB:

  - **Table:** Cấu trúc lưu trữ các mục dữ liệu.

  - **Item:** Một bản ghi dữ liệu trong bảng.

  - **Attribute:** Thành phần dữ liệu mô tả đặc điểm của Item.

  - **Primary Key:** Khóa dùng để xác định duy nhất từng Item.

- Hiểu được vai trò của DynamoDB trong những ứng dụng yêu cầu độ trễ thấp và khả năng mở rộng cao.
- Tìm hiểu sự khác biệt giữa Amazon RDS và DynamoDB:

  - **Amazon RDS:** Phù hợp với các ứng dụng sử dụng mô hình dữ liệu quan hệ và truy vấn SQL.

  - **Amazon DynamoDB:** Phù hợp với các ứng dụng NoSQL cần khả năng mở rộng và truy cập dữ liệu nhanh theo những mẫu truy vấn được thiết kế trước.

#### 6. Kiến thức về bảo mật và sao lưu dữ liệu

- Tìm hiểu vai trò của bảo mật dữ liệu trong môi trường Cloud Computing.
- Nắm được các phương pháp bảo vệ dữ liệu cơ bản:

  - **Encryption:** Mã hóa dữ liệu trong quá trình lưu trữ hoặc truyền tải.

  - **Access Control:** Kiểm soát quyền truy cập của người dùng và dịch vụ.

  - **Backup:** Sao lưu dữ liệu để hỗ trợ việc khôi phục khi xảy ra sự cố.

  - **Versioning:** Quản lý các phiên bản dữ liệu nhằm hỗ trợ khôi phục khi cần thiết.

- Tìm hiểu vai trò của AWS IAM trong việc kiểm soát quyền truy cập đối với các dịch vụ Storage và Database.
- Nhận thức được tầm quan trọng của việc lựa chọn phương pháp lưu trữ và sao lưu phù hợp với nhu cầu của ứng dụng.

#### 7. So sánh các dịch vụ AWS Storage và Database

| Dịch vụ | Loại dịch vụ | Mục đích sử dụng |
|---|---|---|
| **Amazon S3** | Object Storage | Lưu trữ hình ảnh, video, tài liệu, backup và dữ liệu phi cấu trúc |
| **Amazon EBS** | Block Storage | Cung cấp ổ đĩa lưu trữ cho Amazon EC2 |
| **Amazon EFS** | File Storage | Cung cấp hệ thống tệp dùng chung cho các tài nguyên tính toán tương thích |
| **Amazon RDS** | Relational Database | Quản lý dữ liệu quan hệ và các ứng dụng sử dụng SQL |
| **Amazon DynamoDB** | NoSQL Database | Lưu trữ và truy xuất dữ liệu NoSQL với khả năng mở rộng cao |

Thông qua việc so sánh các dịch vụ, em hiểu rõ hơn rằng mỗi giải pháp lưu trữ và cơ sở dữ liệu được thiết kế để đáp ứng những yêu cầu khác nhau.

Việc lựa chọn dịch vụ phù hợp cần dựa trên cấu trúc dữ liệu, phương thức truy cập, hiệu năng, khả năng mở rộng, bảo mật và chi phí vận hành.

#### 8. Tổng kết tuần 3

Trong tuần thứ ba, nội dung nghiên cứu tập trung vào hai nhóm dịch vụ quan trọng trên nền tảng Amazon Web Services là **Storage và Database**.

Thông qua việc tìm hiểu Amazon S3, Amazon EBS và Amazon EFS, em có thêm kiến thức về các mô hình lưu trữ dữ liệu phổ biến trên nền tảng Cloud Computing, cũng như cách lựa chọn giải pháp lưu trữ phù hợp với từng trường hợp sử dụng.

Bên cạnh đó, việc nghiên cứu Amazon RDS và Amazon DynamoDB giúp em hiểu rõ hơn sự khác biệt giữa cơ sở dữ liệu quan hệ và phi quan hệ, những đặc điểm cơ bản của từng loại và vai trò của chúng trong việc xây dựng ứng dụng hiện đại.

Ngoài kiến thức về lưu trữ và cơ sở dữ liệu, tuần học cũng tập trung vào các nguyên tắc bảo mật, kiểm soát quyền truy cập và sao lưu dữ liệu nhằm đảm bảo tính an toàn và khả năng phục hồi của hệ thống.

Những kiến thức đạt được trong tuần 3 là nền tảng quan trọng để tiếp tục tìm hiểu cách xây dựng, triển khai và quản lý ứng dụng trên AWS, đặc biệt là các dịch vụ Serverless như AWS Lambda, Amazon API Gateway và Amazon CloudWatch trong tuần thực tập tiếp theo.
