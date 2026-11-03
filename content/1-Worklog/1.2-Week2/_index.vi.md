---
title: "Worklog Tuần 2"
date: 2026-09-28
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2

- Tìm hiểu các khái niệm cơ bản về mạng máy tính và vai trò của Networking trong môi trường Cloud Computing.
- Nắm được kiến thức nền tảng về Amazon Virtual Private Cloud (Amazon VPC) và cách tổ chức mạng trên AWS.
- Tìm hiểu các thành phần quan trọng trong VPC như Subnet, Route Table, Internet Gateway và Security Group.
- Phân biệt Public Subnet và Private Subnet trong kiến trúc mạng AWS.
- Nghiên cứu các nguyên tắc bảo mật mạng và quản lý quyền truy cập bằng AWS Identity and Access Management (IAM).
- Làm quen với quy trình thiết kế và cấu hình mạng VPC cơ bản.
- Xây dựng nền tảng kiến thức về Networking và Security để phục vụ việc triển khai các ứng dụng trên AWS trong những tuần tiếp theo.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| 2 | - Tìm hiểu tổng quan về Networking trong Cloud Computing. <br> - Nghiên cứu Amazon Virtual Private Cloud (VPC) và vai trò của VPC trong AWS. <br> - Tìm hiểu địa chỉ IP, CIDR Block và các khái niệm cơ bản về phân chia mạng. <br> - Phân biệt mạng truyền thống và mạng trên nền tảng Cloud. | 28/09/2026 | 28/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| 3 | - Nghiên cứu kiến trúc mạng Amazon VPC. <br> - Tìm hiểu Public Subnet và Private Subnet. <br> - Nghiên cứu Route Table và cách định tuyến lưu lượng trong VPC. <br> - Tìm hiểu Internet Gateway và vai trò của nó trong việc kết nối VPC với Internet. | 29/09/2026 | 29/09/2026 | [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) |
| 4 | - Tìm hiểu các cơ chế bảo mật mạng trên AWS. <br> - Nghiên cứu Security Group và Network Access Control List (NACL). <br> - Phân biệt Security Group và NACL. <br> - Tìm hiểu các quy tắc Inbound Rules và Outbound Rules. <br> - Nghiên cứu nguyên tắc Least Privilege trong bảo mật hệ thống. | 30/09/2026 | 30/09/2026 | [VPC Security](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security.html) |
| 5 | - Tìm hiểu AWS Identity and Access Management (IAM). <br> - Nghiên cứu IAM Users, Groups, Roles và Policies. <br> - Tìm hiểu cách quản lý quyền truy cập vào tài nguyên AWS. <br> - Làm quen với nguyên tắc xác thực và phân quyền trong môi trường Cloud. | 01/10/2026 | 01/10/2026 | [AWS IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| 6 | - Tổng hợp kiến thức về Amazon VPC, Subnet, Route Table và Internet Gateway. <br> - Thực hành thiết kế sơ đồ kiến trúc mạng VPC cơ bản. <br> - Tìm hiểu các bước cấu hình VPC và Security Group thông qua AWS Management Console. <br> - Kiểm tra và đánh giá các thành phần trong kiến trúc mạng. <br> - Tổng kết kiến thức tuần 2 và chuẩn bị nội dung nghiên cứu AWS Storage & Database cho tuần 3. | 02/10/2026 | 02/10/2026 | [AWS VPC Workshop](https://catalog.workshops.aws/) |

### Kết quả đạt được tuần 2

#### 1. Kiến thức về AWS Networking

- Hiểu được vai trò của Networking trong việc kết nối và quản lý các tài nguyên trên nền tảng điện toán đám mây.
- Nắm được khái niệm Amazon Virtual Private Cloud (VPC) và vai trò của VPC trong việc xây dựng môi trường mạng ảo trên AWS.
- Tìm hiểu những thành phần cơ bản của hệ thống mạng:
  - **IP Address:** Địa chỉ được sử dụng để định danh các thiết bị và tài nguyên trong mạng.
  - **CIDR (Classless Inter-Domain Routing):** Phương pháp biểu diễn và phân chia dải địa chỉ IP.
  - **VPC:** Mạng ảo được cô lập về mặt logic trong môi trường AWS.
  - **Subnet:** Phân vùng địa chỉ IP bên trong VPC.

#### 2. Kiến thức về kiến trúc Amazon VPC

- Tìm hiểu cách Amazon VPC được tổ chức và cách các thành phần mạng phối hợp với nhau.
- Phân biệt được các loại Subnet:
  - **Public Subnet:** Subnet có tuyến đường đến Internet Gateway, cho phép tài nguyên được cấu hình phù hợp có thể giao tiếp trực tiếp với Internet.
  - **Private Subnet:** Subnet không có tuyến đường trực tiếp đến Internet Gateway.
- Nắm được chức năng của các thành phần:
  - **Route Table:** Chứa các quy tắc định tuyến, xác định đường đi của lưu lượng mạng.
  - **Internet Gateway:** Cho phép kết nối giữa VPC và Internet khi các điều kiện định tuyến và bảo mật được đáp ứng.
  - **Network Interface:** Thành phần mạng ảo hỗ trợ kết nối tài nguyên với hệ thống mạng.

#### 3. Kiến thức về bảo mật mạng AWS

- Hiểu được vai trò của Security Group trong việc kiểm soát lưu lượng mạng đến và đi từ tài nguyên AWS.
- Nắm được sự khác biệt giữa Security Group và Network ACL:
  - **Security Group:** Hoạt động ở cấp tài nguyên hoặc giao diện mạng, có tính stateful.
  - **Network ACL:** Hoạt động ở cấp Subnet và có tính stateless.
- Phân biệt hai loại quy tắc:
  - **Inbound Rules:** Kiểm soát lưu lượng đi vào.
  - **Outbound Rules:** Kiểm soát lưu lượng đi ra.
- Nhận thức được tầm quan trọng của việc giới hạn quyền truy cập mạng và chỉ cho phép những kết nối cần thiết.

#### 4. Kiến thức về AWS Identity and Access Management

- Nắm được vai trò của AWS IAM trong việc quản lý danh tính và quyền truy cập đối với các tài nguyên AWS.
- Phân biệt được các thành phần:
  - **IAM User:** Danh tính được tạo trong tài khoản AWS.
  - **IAM Group:** Nhóm các IAM User để quản lý quyền truy cập.
  - **IAM Role:** Danh tính có tập quyền truy cập, được các đối tượng được phép đảm nhận tạm thời.
  - **IAM Policy:** Tài liệu xác định các quyền truy cập đối với tài nguyên AWS.
- Hiểu nguyên tắc **Least Privilege**, trong đó mỗi người dùng hoặc dịch vụ chỉ được cấp những quyền cần thiết để thực hiện nhiệm vụ.
- Nhận thức được vai trò của xác thực đa yếu tố (MFA) trong việc tăng cường bảo mật tài khoản.

#### 5. Thực hành thiết kế kiến trúc mạng cơ bản

- Tìm hiểu quy trình xây dựng một kiến trúc Amazon VPC đơn giản.
- Thiết kế sơ đồ mạng tham khảo bao gồm:
  - Một VPC với dải địa chỉ CIDR.
  - Một Public Subnet.
  - Một Private Subnet.
  - Một Internet Gateway.
  - Route Table cho từng loại Subnet.
  - Security Group bảo vệ các tài nguyên trong VPC.
- Hiểu được mối liên hệ giữa các thành phần mạng trong quá trình triển khai ứng dụng trên AWS.
- Làm quen với những bước cấu hình và kiểm tra tài nguyên mạng thông qua AWS Management Console.

#### 6. Tổng kết tuần 2

Trong tuần thứ hai, nội dung nghiên cứu tập trung vào hai lĩnh vực quan trọng của Amazon Web Services là Networking và Security.

Thông qua việc tìm hiểu Amazon VPC, Subnet, Route Table, Internet Gateway, Security Group và IAM, em có thêm kiến thức về cách tổ chức mạng ảo, quản lý kết nối và kiểm soát quyền truy cập trong môi trường điện toán đám mây.

Bên cạnh kiến thức lý thuyết, việc nghiên cứu quy trình thiết kế kiến trúc mạng giúp em hiểu rõ hơn mối quan hệ giữa các thành phần và những yếu tố cần quan tâm khi xây dựng hệ thống trên AWS.

Những kiến thức này là nền tảng quan trọng để tiếp tục nghiên cứu các dịch vụ lưu trữ và cơ sở dữ liệu như Amazon S3, Amazon EBS và Amazon RDS trong tuần thực tập tiếp theo.
