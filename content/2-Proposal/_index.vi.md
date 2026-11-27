---
title: "Đề xuất dự án"
date: 2026-11-27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Driver Drowsiness & Distraction Detection
## Giải pháp Edge AI kết hợp AWS Serverless để giám sát trạng thái tài xế

### 1. Tóm tắt dự án (Executive Summary)

**Driver Drowsiness & Distraction Detection** là dự án nghiên cứu và phát triển nguyên mẫu kết hợp Computer Vision, Edge AI và AWS Cloud nhằm nhận diện các biểu hiện có thể liên quan đến tình trạng buồn ngủ hoặc mất tập trung của tài xế. Mục tiêu là hỗ trợ nhận biết sớm những dấu hiệu bất thường, không thay thế các hệ thống an toàn giao thông đã được kiểm định và không đưa ra chẩn đoán tình trạng sức khỏe của tài xế.

Hệ thống thu nhận hình ảnh khuôn mặt từ webcam và xử lý video **trực tiếp trên thiết bị Edge**. Python, OpenCV và MediaPipe Face Mesh (478 facial landmarks theo proposal gốc) hỗ trợ trích xuất **Eye Aspect Ratio (EAR)**, **Mouth Aspect Ratio (MAR)**, **Head Pose** và đặc trưng **Gaze Direction** đang ở mức thử nghiệm. Temporal Analysis kết hợp phân tích CSV và các rule-based candidates giúp nghiên cứu sự thay đổi trạng thái theo thời gian, thay vì chỉ dựa vào một khung hình đơn lẻ.

Kiến trúc Cloud được đề xuất chỉ nhận **metadata của sự kiện**, không nhận video webcam gốc, thông qua Amazon API Gateway (HTTP API). AWS Lambda kiểm tra dữ liệu và ghi sự kiện có điều kiện vào Amazon DynamoDB. Amazon Cognito hỗ trợ xác thực người dùng của Dashboard; Frontend được định hướng lưu trong Amazon S3 private và phân phối qua Amazon CloudFront. CloudWatch, IAM, CloudTrail và AWS Budgets hỗ trợ giám sát, bảo mật và quản lý chi phí; AWS WAF là thành phần tùy chọn.

**Tiến độ được xác nhận trong proposal:** Pipeline xử lý hình ảnh tại Edge đã được xây dựng, kiến trúc AWS đã được thiết kế. Local Event Buffer/Retry, việc hoàn thiện Temporal Analysis, đánh giá Gaze, tích hợp Cloud và kiểm thử khả năng phục hồi vẫn cần tiếp tục thực hiện hoặc xác minh. Đây là **kiến trúc mục tiêu**, không phải mô tả một hệ thống Production đã triển khai hoàn chỉnh.

### 2. Vấn đề đặt ra (Problem Statement)

#### Vấn đề cần giải quyết

Tài xế có thể xuất hiện những biểu hiện như nhắm mắt kéo dài, ngáp, thay đổi tư thế đầu hoặc hướng nhìn. Việc phát hiện và diễn giải những biểu hiện này một cách ổn định gặp khó khăn do sự khác biệt giữa từng người, điều kiện ánh sáng, góc quay, tình trạng che khuất khuôn mặt và chuyển động khi ghi hình.

Nếu xử lý bằng cách liên tục truyền video lên Cloud, hệ thống có thể phát sinh lưu lượng mạng lớn, độ trễ, chi phí và rủi ro quyền riêng tư. Do đó, một nguyên mẫu giám sát cần tách biệt việc phân tích hình ảnh tại thiết bị với nhiệm vụ lưu trữ sự kiện trên Cloud, hỗ trợ tình huống mất kết nối và tránh đưa ra kết luận chắc chắn khi thông tin chưa đủ tin cậy.

#### Giải pháp đề xuất

Dự án lựa chọn kiến trúc **Edge AI + AWS Serverless** với các bước:

1. **Thu nhận và phân tích tại Edge:** Webcam cung cấp hình ảnh cho OpenCV và MediaPipe. Pipeline trích xuất EAR, MAR, Head Pose và đặc trưng Gaze đang thử nghiệm.
2. **Phân tích theo thời gian:** Phân tích CSV và rule-based candidates giúp nghiên cứu các đặc trưng qua nhiều khung hình để xác định những sự kiện cần ghi nhận; các quy tắc và ngưỡng vẫn cần kiểm thử.
3. **Lưu đệm cục bộ:** Mỗi sự kiện được gắn `event_id`. Local Event Buffer dự kiến giữ metadata khi mất mạng; cơ chế Retry gửi lại khi có kết nối.
4. **Tiếp nhận sự kiện trên Cloud:** Edge gửi metadata bằng HTTPS POST đến API Gateway. Lambda Event Writer kiểm tra dữ liệu và sử dụng DynamoDB `Conditional PutItem` để hạn chế ghi trùng theo `event_id`.
5. **Truy cập lịch sử có xác thực:** Dashboard sử dụng Amazon Cognito và JWT cho các API được bảo vệ. Lambda Event Reader truy vấn DynamoDB để cung cấp lịch sử sự kiện phù hợp.
6. **Phân phối và giám sát:** CloudFront phân phối Frontend từ S3 private thông qua Origin Access Control (OAC). CloudWatch phục vụ thu thập log và metrics.

Thiết kế giữ toàn bộ quá trình xử lý video tại Edge. Phần Cloud tập trung vào **metadata, lưu trữ, phân quyền truy cập và giám sát**, không thực hiện suy luận trực tiếp trên luồng video gốc.

#### Lợi ích và giá trị ứng dụng

- **Ưu tiên quyền riêng tư:** Không gửi video webcam gốc lên AWS trong luồng xử lý đề xuất.
- **Giảm phụ thuộc vào mạng:** Quá trình phân tích khuôn mặt vẫn có thể tiếp tục tại Edge; đồng bộ sự kiện được thiết kế để khôi phục sau sự cố mạng.
- **Giảm công việc quản trị:** API Gateway, Lambda và DynamoDB giúp hạn chế nhu cầu vận hành máy chủ ứng dụng.
- **Truy xuất sự kiện:** Dashboard dự kiến cho phép người dùng có quyền xem lịch sử sự kiện đã ghi nhận.
- **Giá trị học tập:** Dự án kết nối Computer Vision/AI với bảo mật AWS, Serverless, triển khai Frontend và giám sát hệ thống.

Hiện chưa có dữ liệu thực nghiệm để khẳng định mức giảm tai nạn, lợi ích tài chính hoặc tỷ lệ tiết kiệm chi phí cụ thể.

### 3. Kiến trúc giải pháp (Solution Architecture)

Hệ thống gồm ba lớp chính: **Edge Processing**, **AWS Event Backend** và **Web Dashboard**. Chỉ metadata sự kiện được gửi từ thiết bị Edge sang Cloud.

```text
XỬ LÝ TẠI EDGE (thiết bị cục bộ)
Webcam -> OpenCV -> MediaPipe Face Mesh (478 landmarks)
       -> EAR / MAR / Head Pose / Gaze thử nghiệm
       -> CSV Analysis + Temporal / Rule-based Candidates
       -> Event Metadata (event_id)
       -> Local Event Buffer + Retry (dự kiến)
                      |
                 HTTPS POST
             (chỉ metadata)
                      v
BACKEND TRÊN AWS CLOUD
Amazon API Gateway (HTTP API)
       -> AWS Lambda Event Writer (kiểm tra dữ liệu)
       -> Amazon DynamoDB (Conditional PutItem theo event_id)

DASHBOARD / TRUY VẤN LỊCH SỬ
Trình duyệt -> Amazon Cognito (đăng nhập / JWT)
            -> API Gateway (JWT Authorizer cho route bảo vệ)
            -> AWS Lambda Event Reader
            -> Amazon DynamoDB -> Lịch sử sự kiện -> Trình duyệt

Frontend: Amazon S3 private -> CloudFront (OAC) -> Trình duyệt
Giám sát: CloudWatch | Phân quyền: IAM | Audit: CloudTrail
Quản lý chi phí: AWS Budgets | Bảo vệ bổ sung: AWS WAF (tùy chọn)
```

*Hình 1 – Sơ đồ kiến trúc đề xuất Edge AI và AWS Cloud (dạng văn bản). Sơ đồ thể hiện thiết kế, không phải bằng chứng tất cả dịch vụ Cloud đã triển khai.*

#### Các dịch vụ AWS sử dụng

| Dịch vụ AWS | Vai trò dự kiến | Trạng thái theo proposal |
|---|---|---|
| Amazon API Gateway (HTTP API) | Tiếp nhận sự kiện từ Edge và request của Dashboard | Đã thiết kế kiến trúc |
| AWS Lambda – Event Writer | Kiểm tra metadata và ghi sự kiện | Đã thiết kế kiến trúc |
| Amazon DynamoDB | Lưu lịch sử sự kiện, hỗ trợ ghi có điều kiện | Đã thiết kế kiến trúc |
| AWS Lambda – Event Reader | Truy xuất lịch sử sự kiện cho Dashboard | Đã thiết kế kiến trúc |
| Amazon Cognito | Đăng ký, đăng nhập và cấp JWT | Đã thiết kế kiến trúc |
| Amazon S3 | Lưu Frontend ở chế độ private | Đã thiết kế kiến trúc |
| Amazon CloudFront + OAC | Phân phối giao diện, hạn chế truy cập trực tiếp S3 | Đã thiết kế kiến trúc |
| Amazon CloudWatch | API access logs, Lambda logs/errors/duration, DynamoDB metrics | Đã đưa vào phương án giám sát |
| AWS IAM | Quản lý quyền truy cập theo nguyên tắc tối thiểu | Thành phần hỗ trợ đề xuất |
| AWS CloudTrail | Theo dõi hoạt động tài khoản AWS | Thành phần hỗ trợ đề xuất |
| AWS Budgets | Theo dõi và cảnh báo chi phí | Thành phần hỗ trợ đề xuất |
| AWS WAF | Bảo vệ bổ sung ở tầng ứng dụng | **Tùy chọn** |

#### Thiết kế các thành phần (Component Design)

**Xử lý AI tại Edge**
- **Dữ liệu đầu vào:** Video từ webcam, xử lý cục bộ bằng OpenCV.
- **Nhận diện khuôn mặt:** MediaPipe Face Mesh với 478 landmarks theo tài liệu dự án.
- **Trích xuất đặc trưng:** EAR, MAR, Head Pose và Gaze Direction thử nghiệm.
- **Phân tích trạng thái:** Phân tích CSV và rule-based candidates; thuật toán cuối cùng vẫn cần hoàn thiện, đánh giá.
- **Đồng bộ sự kiện:** `event_id`, Local Event Buffer và Retry theo thiết kế; chưa xác nhận hoàn tất.

**Xử lý sự kiện trên Cloud**
- **Tiếp nhận:** API Gateway nhận HTTPS POST chứa metadata, không chứa video gốc.
- **Kiểm tra và lưu trữ:** Lambda Event Writer kiểm tra dữ liệu trước khi ghi có điều kiện vào DynamoDB nhằm hỗ trợ tránh trùng lặp.
- **Truy vấn lịch sử:** Các yêu cầu Dashboard được bảo vệ đi qua API Gateway đến Lambda Event Reader để truy xuất dữ liệu từ DynamoDB.

**Frontend, xác thực và vận hành**
- **Xác thực:** Cognito cấp JWT để đăng nhập Dashboard; API Gateway JWT Authorizer bảo vệ những route được cấu hình.
- **Phân phối:** CloudFront cung cấp Frontend từ S3 private thông qua OAC.
- **Giám sát:** CloudWatch theo dõi hoạt động; IAM, CloudTrail và Budgets hỗ trợ phân quyền, audit và kiểm soát chi phí.

*Lưu ý thiết kế bảo mật:* Proposal mô tả JWT cho Dashboard nhưng chưa xác định phương án xác thực cuối cùng đối với API nhận sự kiện từ Edge. Cơ chế này cần được làm rõ và kiểm thử trước khi triển khai công khai. Việc JWT hợp lệ cũng chưa tự bảo đảm người dùng được quyền xem mọi bản ghi DynamoDB; cần kiểm tra phân quyền trên dữ liệu.

### 4. Triển khai kỹ thuật (Technical Implementation)

#### Các giai đoạn triển khai

Dự án được chia thành các nhóm công việc sau. Thứ tự này nhằm lập kế hoạch, không đồng nghĩa mọi giai đoạn đã hoàn thành.

1. **Nghiên cứu và xây dựng pipeline Edge:** Tìm hiểu biểu hiện buồn ngủ/mất tập trung, xây dựng xử lý webcam với OpenCV và MediaPipe, trích xuất EAR, MAR, Head Pose và Gaze. **Trạng thái:** Đã có pipeline Edge; Gaze vẫn thử nghiệm.
2. **Phân tích theo thời gian và đánh giá:** Sử dụng CSV analysis, rule-based candidates để nghiên cứu thay đổi qua khung hình, hoàn thiện tiêu chí sự kiện và kiểm tra cảnh báo sai. **Trạng thái:** Đã có hướng tiếp cận ban đầu; cần hoàn thiện.
3. **Xử lý sự kiện cục bộ tin cậy:** Xác định metadata và `event_id`, hoàn thiện Local Event Buffer, kiểm thử Retry và đồng bộ khi kết nối phục hồi. **Trạng thái:** Đã định hướng; cần hoàn thiện và kiểm thử sự cố mạng.
4. **Tích hợp AWS Backend và Dashboard:** Cấu hình API Gateway, Lambda Writer/Reader, DynamoDB, Cognito, S3 private/CloudFront OAC và giám sát. Kiểm tra phân quyền và truy xuất lịch sử xuyên suốt. **Trạng thái:** Đã thiết kế kiến trúc Cloud; chưa có xác nhận toàn bộ đã triển khai thành công.
5. **Kiểm thử và hoàn thiện tài liệu:** Thử nghiệm các mức ánh sáng, góc quay, mất mạng, ghi trùng sự kiện, lỗi Backend, kiểm soát truy cập, giám sát và cảnh báo chi phí. Ghi lại kết quả và giới hạn thực tế. **Trạng thái:** Cần chứng cứ kiểm thử.

#### Yêu cầu kỹ thuật

- **Thiết bị Edge:** Webcam và máy tính có khả năng chạy pipeline Computer Vision cục bộ. Proposal chưa quy định cấu hình CPU/GPU tối thiểu.
- **Phần mềm Edge:** Python, OpenCV, MediaPipe Face Mesh, các thành phần phân tích theo thời gian/CSV, cùng Local Buffer và Retry dự kiến.
- **Dịch vụ Cloud:** API Gateway, Lambda, DynamoDB, Cognito, S3, CloudFront, CloudWatch; các dịch vụ hỗ trợ IAM, CloudTrail, AWS Budgets, WAF tùy chọn.
- **Dữ liệu sự kiện:** Chỉ gửi metadata với `event_id` duy nhất; schema cuối cùng, thời gian lưu trữ và nguyên tắc phân quyền cần được chốt.
- **Quyền riêng tư và bảo mật:** Không tải video gốc lên AWS; giới hạn quyền IAM; xác thực Dashboard và phân quyền truy cập lịch sử sự kiện.
- **Tiêu chí đánh giá:** Chất lượng phát hiện, cảnh báo sai, độ trễ, khả năng hoạt động khi mất mạng và xử lý các điều kiện hình ảnh khó. Chưa có ngưỡng số liệu được xác nhận.

### 5. Tiến độ và các mốc (Timeline & Milestones)

Tài liệu proposal gốc **không cung cấp ngày cụ thể đã được xác nhận cho từng mốc**. Bảng sau là **đề xuất phân bổ** theo cấu trúc Worklog tuần 6–12 của FCAJ; cần đối chiếu lại lịch làm việc thực tế.

| Giai đoạn dự kiến | Trọng tâm | Sản phẩm / Bằng chứng |
|---|---|---|
| Tuần 6 | Nghiên cứu bài toán và yêu cầu | Mô tả bài toán, đặc trưng ban đầu, yêu cầu chức năng và quyền riêng tư |
| Tuần 7 | Thiết kế kiến trúc và luồng dữ liệu | Sơ đồ Edge–Cloud, luồng sự kiện, vai trò dịch vụ AWS |
| Tuần 8 | Phát triển chức năng Edge cốt lõi | Pipeline webcam, trích xuất đặc trưng, rule candidates ban đầu |
| Tuần 9 | Tích hợp và kiểm thử | Luồng metadata cục bộ, kiểm tra tích hợp AWS, biên bản thử nghiệm |
| Tuần 10 | Đánh giá và tối ưu | Kiểm thử ánh sáng/góc quay, phân tích cảnh báo sai, quan sát hiệu năng |
| Tuần 11 | Hoàn thiện và tài liệu kỹ thuật | Cải thiện độ ổn định, hướng dẫn cài đặt, sơ đồ và báo cáo kiểm thử |
| Tuần 12 | Báo cáo và trình diễn | Kết quả đã kiểm chứng, giới hạn, demo và báo cáo thực tập |

**Nguyên tắc nghiệm thu:** Chỉ đánh dấu một mốc hoàn thành khi có code, log, hình ảnh, kết quả kiểm thử hoặc bằng chứng phù hợp. Theo tài liệu nguồn, pipeline Edge và kiến trúc Cloud đã được xây dựng/thiết kế, nhưng chưa xác nhận hoàn thiện hệ thống end-to-end.

### 6. Dự toán ngân sách (Budget Estimation)

Dự án lựa chọn kiến trúc Serverless nhằm giảm nhu cầu quản trị máy chủ cố định trong giai đoạn ít người dùng. **Proposal gốc chưa cung cấp bảng tính AWS Pricing Calculator hoặc hóa đơn chi phí AWS thực tế.** Vì vậy, không sao chép chi phí của dự án IoT Weather trong file mẫu và không tự tạo số tiền giả định.

#### Các thành phần chi phí hạ tầng

| Thành phần | Yếu tố cần tính chi phí |
|---|---|
| Amazon API Gateway | Số lượng API requests |
| AWS Lambda | Số lần gọi, bộ nhớ, thời gian thực thi |
| Amazon DynamoDB | Lượt đọc/ghi và dữ liệu sự kiện lưu trữ |
| Amazon Cognito | Mô hình tính phí theo người dùng/xác thực áp dụng |
| Amazon S3 | Dung lượng Frontend và các request |
| Amazon CloudFront | Lưu lượng truyền tải và request |
| Amazon CloudWatch | Dung lượng log, thời gian giữ log, metrics và alarms |
| AWS CloudTrail | Cấu hình ghi nhận/audit và chi phí lưu trữ liên quan |
| AWS WAF (nếu bật) | Chi phí bảo vệ bổ sung theo mức sử dụng |
| Thiết bị Edge / mạng | Thiết bị sẵn có, điện và kết nối Internet |

**Cần thực hiện trước khi triển khai:** Xác định số thiết bị, số sự kiện/thiết bị/ngày, số lượt API, dung lượng metadata, thời gian lưu lịch sử, nhu cầu Dashboard, AWS Region và thời gian lưu log; sau đó lập dự toán tại [AWS Pricing Calculator](https://calculator.aws/).

**Biện pháp kiểm soát:** Thiết lập AWS Budgets và cảnh báo, kiểm tra thời gian lưu CloudWatch Logs, hạn chế request không cần thiết và chỉ gửi metadata cần thiết. Chưa khẳng định ROI hay thời gian hoàn vốn khi chưa có dữ liệu đo lường.

### 7. Đánh giá rủi ro (Risk Assessment)

#### Ma trận rủi ro sơ bộ

Các nội dung dưới đây là *nhận định phục vụ lập kế hoạch*, chưa phải xác suất đã được đo lường từ thực nghiệm.

| Rủi ro | Tác động tiềm ẩn | Phương án ứng phó |
|---|---|---|
| Kết nối Internet gián đoạn | Metadata không được đồng bộ ngay | Local Event Buffer, Retry và kiểm thử phục hồi |
| Ánh sáng kém, góc quay lệch, khuôn mặt bị che | Sai lệch đặc trưng hoặc không nhận diện được | Kiểm thử nhiều điều kiện; cho phép trạng thái chưa xác định |
| Quy tắc Temporal Analysis chưa phù hợp | Cảnh báo sai hoặc bỏ sót sự kiện | Tinh chỉnh bằng dữ liệu thử nghiệm và phân tích cảnh báo sai |
| Gaze Direction đang thử nghiệm | Nhận định mất tập trung chưa tin cậy | Chưa dùng Gaze làm tiêu chí chính khi chưa được đánh giá |
| Gửi trùng sự kiện | Bản ghi lịch sử bị lặp | `event_id` duy nhất và DynamoDB Conditional PutItem |
| Truy cập trái phép lịch sử | Lộ dữ liệu và rủi ro quyền riêng tư | Cognito/JWT, phân quyền dữ liệu và rà soát IAM |
| Lỗi dịch vụ Cloud/cấu hình sai | Gián đoạn tiếp nhận sự kiện hoặc Dashboard | Lưu sự kiện chờ tại Edge, theo dõi và kiểm thử khôi phục |
| Chi phí AWS phát sinh ngoài dự kiến | Vượt ngân sách | AWS Budgets, theo dõi sử dụng và dự toán theo tải |

#### Biện pháp giảm thiểu

- **Độ tin cậy nhận diện:** Kiểm thử trong nhiều điều kiện ánh sáng, góc quay; ghi lại trường hợp thất bại hoặc chưa xác định.
- **Khả năng chịu lỗi mạng:** Lưu metadata chưa đồng bộ tại Edge và kiểm tra gửi lại sau khi có kết nối.
- **Toàn vẹn dữ liệu:** Sử dụng event_id nhất quán và ghi có điều kiện để hạn chế trùng lặp.
- **Quyền riêng tư:** Giữ video gốc tại Edge; kiểm soát và ghi nhận quyền truy cập metadata.
- **Giám sát AWS:** Theo dõi CloudWatch Logs, số lỗi, thời gian xử lý và hoạt động DynamoDB.
- **Chi phí:** Sử dụng AWS Budgets và đánh giá lại dự toán khi lưu lượng tăng.

#### Phương án dự phòng

- Khi mất Internet, tiếp tục xử lý tại Edge và giữ sự kiện chưa đồng bộ cho đến khi có thể gửi lại, sau khi cơ chế Buffer được kiểm thử đạt yêu cầu.
- Khi dữ liệu khuôn mặt không đủ tin cậy, tránh đưa ra kết luận chắc chắn và ghi nhận giới hạn để đánh giá.
- Khi dịch vụ Cloud gặp lỗi, kiểm tra log/quyền truy cập, sửa cấu hình và kiểm thử lại trước khi xác nhận tích hợp thành công.
- Khi chi phí tăng bất thường, giảm mức sử dụng không cần thiết và xem lại chính sách lưu trữ, logging hoặc dịch vụ tùy chọn.

### 8. Kết quả dự kiến (Expected Outcomes)

#### Cải thiện về kỹ thuật

Khi được hoàn thiện và kiểm chứng, hệ thống hướng đến khả năng:

- Xử lý video webcam trực tiếp tại Edge để trích xuất đặc trưng khuôn mặt và phân tích trạng thái theo thời gian.
- Nhận diện những sự kiện có thể liên quan đến buồn ngủ hoặc mất tập trung mà không tải video gốc lên AWS.
- Tạo metadata và đồng bộ tin cậy thông qua cơ chế Local Event Buffer/Retry.
- Lưu trữ và truy vấn lịch sử qua API Gateway, Lambda và DynamoDB.
- Cung cấp Dashboard được bảo vệ bằng Cognito, S3 private và CloudFront.
- Theo dõi hoạt động và chi phí thông qua CloudWatch và AWS Budgets.

#### Giá trị lâu dài

- Minh họa cách kết hợp Edge AI và AWS Serverless trong một ứng dụng hoàn chỉnh.
- Tạo nền tảng mô-đun để cải thiện Temporal Analysis và nghiên cứu thêm các đặc trưng khuôn mặt.
- Hỗ trợ nghiên cứu khả năng ổn định, bảo vệ quyền riêng tư, chi phí và trải nghiệm người dùng.
- Là kết quả học tập và thực hành kỹ thuật trong chương trình First Cloud AI Journey (FCAJ).

**Giới hạn phạm vi:** Đây là kết quả kỳ vọng. Độ chính xác nhận diện, mức độ sẵn sàng triển khai Production và hiệu quả trong điều kiện lái xe thực tế cần được xác nhận bằng kiểm thử có tài liệu, không thể suy ra chỉ từ kiến trúc đề xuất.
