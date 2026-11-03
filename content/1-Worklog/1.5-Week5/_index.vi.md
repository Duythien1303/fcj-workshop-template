---
title: "Worklog Tuần 5"
date: 2026-11-02
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---



### Mục tiêu tuần 5

- Tìm hiểu tổng quan về Generative Artificial Intelligence (Generative AI) và vai trò của công nghệ này trong các ứng dụng hiện đại.
- Nắm được những khái niệm cơ bản về Large Language Models (LLMs), Foundation Models và các phương pháp ứng dụng mô hình ngôn ngữ.
- Nghiên cứu Amazon Bedrock và khả năng hỗ trợ xây dựng ứng dụng Generative AI trên nền tảng AWS.
- Tìm hiểu kỹ thuật Prompt Engineering và những phương pháp cải thiện chất lượng phản hồi của mô hình AI.
- Nghiên cứu Retrieval-Augmented Generation (RAG), Embeddings, Vector Database và Knowledge Bases.
- Tìm hiểu kiến trúc AI Agents và cách tích hợp các mô hình AI với API, công cụ và nguồn dữ liệu bên ngoài.
- Tổng hợp kiến thức AWS đã nghiên cứu trong 5 tuần đầu tiên.
- Xác định định hướng, mục tiêu và những công nghệ có thể sử dụng cho Project cuối kỳ thực tập.
- Xây dựng kế hoạch nghiên cứu và triển khai Project trong 5 tuần tiếp theo.

### Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|---|---|---|---|---|
| 2 | - Tìm hiểu tổng quan về Generative AI và các ứng dụng trong thực tế. <br> - Nghiên cứu Large Language Models (LLMs) và Foundation Models. <br> - Tìm hiểu sự khác biệt giữa Traditional AI, Generative AI và Agentic AI. <br> - Nghiên cứu các trường hợp ứng dụng AI trong phát triển phần mềm, xử lý ngôn ngữ và tự động hóa. | 02/11/2026 | 02/11/2026 | [AWS Generative AI](https://aws.amazon.com/generative-ai/) |
| 3 | - Tìm hiểu tổng quan về Amazon Bedrock và các khả năng chính của dịch vụ. <br> - Nghiên cứu cách Amazon Bedrock hỗ trợ truy cập Foundation Models. <br> - Tìm hiểu các khái niệm Model Inference, Tokens, Context Window và Model Parameters. <br> - Nghiên cứu Prompt Engineering và các phương pháp thiết kế Prompt. <br> - Tìm hiểu quy trình thử nghiệm và đánh giá phản hồi của mô hình AI. | 03/11/2026 | 03/11/2026 | [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html) <br> [Prompt Engineering](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-prompt-engineering.html) |
| 4 | - Tìm hiểu Retrieval-Augmented Generation (RAG) và vai trò của RAG trong ứng dụng Generative AI. <br> - Nghiên cứu Embeddings và Vector Database. <br> - Tìm hiểu Amazon Bedrock Knowledge Bases. <br> - Nghiên cứu quy trình thu thập dữ liệu, chia nhỏ tài liệu (Chunking), tìm kiếm thông tin và sinh phản hồi. <br> - Phân tích những ưu điểm và hạn chế của RAG trong các hệ thống AI. | 04/11/2026 | 04/11/2026 | [Amazon Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html) |
| 5 | - Tìm hiểu khái niệm AI Agents và Agentic AI. <br> - Nghiên cứu kiến trúc hệ thống AI Agent, bao gồm LLM, Tools, Memory và API. <br> - Tìm hiểu Amazon Bedrock Agents và cơ chế phối hợp giữa các thành phần. <br> - Nghiên cứu cách tích hợp AI Agents với AWS Lambda và các dịch vụ Backend. <br> - Khảo sát những ứng dụng AI có thể phát triển thành Project cuối kỳ thực tập. | 05/11/2026 | 05/11/2026 | [Amazon Bedrock Agents](https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html) |
| 6 | - Tổng hợp kiến thức Generative AI, Amazon Bedrock, RAG và AI Agents. <br> - Ôn tập các dịch vụ AWS đã nghiên cứu trong 5 tuần đầu. <br> - Phân tích các ý tưởng Project dựa trên kiến thức và kỹ năng hiện có. <br> - Xác định mục tiêu, phạm vi nghiên cứu và những yêu cầu cơ bản của Project cuối kỳ. <br> - Lập kế hoạch nghiên cứu, thiết kế, phát triển và kiểm thử Project trong 5 tuần tiếp theo. | 06/11/2026 | 06/11/2026 | [AWS Documentation](https://docs.aws.amazon.com/) <br> [AWS Workshops](https://catalog.workshops.aws/) |

### Kết quả dự kiến đạt được tuần 5

#### 1. Kiến thức tổng quan về Generative AI

- Hiểu được khái niệm Generative AI và vai trò của công nghệ này trong việc tạo nội dung, hỗ trợ xử lý thông tin và tự động hóa các tác vụ.
- Phân biệt được những khái niệm quan trọng:

  - **Traditional AI:** Các hệ thống AI được xây dựng nhằm thực hiện những nhiệm vụ như phân loại, dự đoán và nhận dạng.

  - **Generative AI:** Công nghệ AI có khả năng tạo ra nội dung mới như văn bản, hình ảnh, mã nguồn và các loại dữ liệu khác.

  - **Agentic AI:** Hướng tiếp cận xây dựng các hệ thống AI có khả năng sử dụng công cụ và phối hợp nhiều bước xử lý để thực hiện nhiệm vụ.

- Tìm hiểu những ứng dụng phổ biến của Generative AI:

  - Chatbots và Virtual Assistants.
  - Tóm tắt tài liệu và phân tích văn bản.
  - Hỗ trợ lập trình và phát triển phần mềm.
  - Truy xuất và xử lý thông tin.
  - Tự động hóa các quy trình công việc.

#### 2. Kiến thức về Large Language Models và Foundation Models

- Tìm hiểu khái niệm Large Language Models (LLMs) và khả năng xử lý, phân tích, sinh ngôn ngữ tự nhiên.
- Nắm được những khái niệm cơ bản:

  - **Foundation Model:** Mô hình được huấn luyện trên lượng dữ liệu lớn, có thể thích ứng với nhiều nhiệm vụ khác nhau.

  - **Large Language Model (LLM):** Mô hình ngôn ngữ quy mô lớn có khả năng xử lý và sinh văn bản.

  - **Token:** Đơn vị dữ liệu được mô hình sử dụng trong quá trình xử lý đầu vào và tạo đầu ra.

  - **Context Window:** Giới hạn lượng ngữ cảnh mà mô hình có thể xử lý trong một lần tương tác.

  - **Inference:** Quá trình sử dụng mô hình đã được huấn luyện để tạo dự đoán hoặc phản hồi.

- Hiểu được vai trò của LLM trong các ứng dụng Generative AI và AI Agents.

#### 3. Kiến thức về Amazon Bedrock

- Tìm hiểu Amazon Bedrock là dịch vụ được AWS quản lý, hỗ trợ xây dựng và mở rộng các ứng dụng Generative AI.
- Nghiên cứu khả năng truy cập nhiều Foundation Models thông qua các giao diện và API được hỗ trợ.
- Tìm hiểu những thành phần và chức năng liên quan:

  - **Foundation Models:** Các mô hình AI phục vụ những nhiệm vụ như sinh văn bản, phân tích dữ liệu và xử lý nội dung.

  - **Model Inference:** Gửi dữ liệu đầu vào đến mô hình và nhận kết quả xử lý.

  - **Knowledge Bases:** Hỗ trợ kết nối mô hình với dữ liệu và nguồn tri thức bên ngoài.

  - **Agents:** Hỗ trợ xây dựng các hệ thống AI có khả năng xử lý nhiệm vụ và tương tác với công cụ.

- Nhận thức được tầm quan trọng của việc lựa chọn mô hình phù hợp dựa trên chất lượng đầu ra, tốc độ phản hồi, khả năng hỗ trợ nhiệm vụ và chi phí.

#### 4. Kiến thức về Prompt Engineering

- Hiểu được vai trò của Prompt Engineering trong việc cải thiện chất lượng phản hồi của các mô hình ngôn ngữ.
- Tìm hiểu một số kỹ thuật phổ biến:

  - **Zero-shot Prompting:** Yêu cầu mô hình thực hiện nhiệm vụ mà không cung cấp ví dụ mẫu.

  - **Few-shot Prompting:** Cung cấp một số ví dụ để hướng dẫn mô hình thực hiện nhiệm vụ.

  - **Role-based Prompting:** Xác định vai trò hoặc bối cảnh hoạt động của mô hình.

  - **Structured Prompting:** Thiết kế Prompt có cấu trúc rõ ràng về nhiệm vụ, dữ liệu đầu vào và định dạng kết quả mong muốn.

- Nhận thức được tầm quan trọng của việc kiểm thử và đánh giá phản hồi thay vì chỉ dựa vào một kết quả do mô hình tạo ra.

#### 5. Kiến thức về Retrieval-Augmented Generation (RAG)

- Tìm hiểu RAG là phương pháp kết hợp truy xuất thông tin từ nguồn dữ liệu bên ngoài với khả năng tạo phản hồi của mô hình ngôn ngữ.
- Nắm được những thành phần cơ bản:

  - **Document Processing:** Chuẩn bị và xử lý dữ liệu tài liệu.

  - **Chunking:** Chia tài liệu thành các đoạn nhỏ phù hợp cho việc truy xuất.

  - **Embeddings:** Biểu diễn nội dung dữ liệu dưới dạng Vector số.

  - **Vector Database:** Hệ thống lưu trữ và tìm kiếm các Vector dựa trên độ tương đồng.

  - **Retriever:** Thành phần tìm kiếm thông tin có liên quan đến truy vấn.

  - **LLM:** Sử dụng thông tin truy xuất được để xây dựng phản hồi.

- Nghiên cứu quy trình hoạt động cơ bản của RAG:

  1. Thu thập và chuẩn bị nguồn dữ liệu.
  2. Chia nhỏ và xử lý tài liệu.
  3. Chuyển đổi nội dung thành Embeddings.
  4. Lưu trữ dữ liệu phục vụ truy xuất.
  5. Tiếp nhận câu hỏi từ người dùng.
  6. Truy xuất những nội dung liên quan.
  7. Cung cấp ngữ cảnh cho mô hình ngôn ngữ.
  8. Tạo phản hồi dựa trên câu hỏi và thông tin được truy xuất.

- Hiểu được những lợi ích và hạn chế của RAG, đặc biệt là sự phụ thuộc vào chất lượng dữ liệu và kết quả truy xuất.

#### 6. Kiến thức về AI Agents và Agentic AI

- Nắm được khái niệm AI Agent và vai trò của hệ thống AI trong việc thực hiện các nhiệm vụ thông qua việc sử dụng công cụ.
- Tìm hiểu các thành phần phổ biến của một kiến trúc AI Agent:

  - **LLM:** Hỗ trợ diễn giải yêu cầu, suy luận và tạo phản hồi.

  - **Tools:** Các công cụ được hệ thống cho phép sử dụng để thực hiện tác vụ.

  - **Memory:** Cơ chế duy trì thông tin hoặc ngữ cảnh khi ứng dụng yêu cầu.

  - **API Integration:** Kết nối hệ thống AI với các dịch vụ và nguồn dữ liệu bên ngoài.

  - **Workflow:** Quy trình phối hợp giữa các thành phần để hoàn thành nhiệm vụ.

- Nghiên cứu Amazon Bedrock Agents và các thành phần như Foundation Model, Instructions, Action Groups và Knowledge Bases.
- Tìm hiểu khả năng tích hợp AI Agents với các dịch vụ AWS và ứng dụng Backend.
- Nhận thức được vai trò của kiểm soát quyền truy cập, đánh giá kết quả và giám sát hoạt động trong việc phát triển các hệ thống AI Agent.

#### 7. Tổng hợp kiến thức AWS trong 5 tuần đầu

| Tuần | Chủ đề | Kiến thức trọng tâm |
|---|---|---|
| **Tuần 1** | AWS Fundamentals | Cloud Computing, AWS Services, Regions, Availability Zones |
| **Tuần 2** | AWS Networking & Security | VPC, Subnet, Route Table, Security Group, IAM |
| **Tuần 3** | AWS Storage & Database | Amazon S3, EBS, EFS, RDS, DynamoDB |
| **Tuần 4** | AWS Serverless & Application Deployment | AWS Lambda, API Gateway, CloudWatch |
| **Tuần 5** | Generative AI on AWS | Amazon Bedrock, LLMs, Prompt Engineering, RAG, AI Agents |

Năm tuần đầu tiên được xây dựng nhằm tạo nền tảng kiến thức về điện toán đám mây, bảo mật, lưu trữ dữ liệu, phát triển ứng dụng Serverless và những công nghệ AI hiện đại.

Các nội dung này có thể được sử dụng làm cơ sở để lựa chọn kiến trúc, công nghệ và phương pháp triển khai Project cuối kỳ thực tập.

#### 8. Chuẩn bị cho Project cuối kỳ thực tập

- Khảo sát những ý tưởng Project phù hợp với kiến thức và kỹ năng đã tích lũy.
- Xác định các yếu tố cần phân tích trước khi triển khai:

  - **Problem Definition:** Xác định vấn đề thực tế mà Project hướng đến giải quyết.

  - **Project Objectives:** Xây dựng các mục tiêu cụ thể và có thể đánh giá được.

  - **Project Scope:** Xác định phạm vi chức năng và những giới hạn của Project.

  - **Technology Stack:** Lựa chọn các công nghệ, thư viện, Framework và dịch vụ cần thiết.

  - **System Architecture:** Xây dựng kiến trúc tổng quan của hệ thống.

  - **Evaluation Methods:** Lựa chọn các phương pháp kiểm thử và đánh giá kết quả.

  - **Development Timeline:** Phân chia tiến độ nghiên cứu và phát triển cho từng tuần.

- Xây dựng kế hoạch Project dự kiến:

| Tuần | Giai đoạn | Nội dung |
|---|---|---|
| **Tuần 6** | Research & Problem Definition | Nghiên cứu đề tài, xác định bài toán và yêu cầu |
| **Tuần 7** | System Design | Thiết kế kiến trúc và các thành phần chính |
| **Tuần 8** | Implementation | Phát triển các chức năng cốt lõi |
| **Tuần 9** | Testing & Optimization | Kiểm thử, đánh giá và cải thiện hệ thống |
| **Tuần 10** | Final Demo & Documentation | Hoàn thiện sản phẩm, báo cáo và demo |

#### 9. Tổng kết tuần 5

Tuần thứ năm tập trung vào việc nghiên cứu các công nghệ Generative AI và khả năng ứng dụng trên nền tảng Amazon Web Services.

Thông qua những nội dung về Large Language Models, Amazon Bedrock, Prompt Engineering, RAG và AI Agents, mục tiêu của tuần là xây dựng nền tảng kiến thức cần thiết để hiểu và lựa chọn những phương pháp phát triển ứng dụng AI hiện đại.

Bên cạnh việc nghiên cứu các công nghệ mới, tuần 5 còn có vai trò tổng kết kiến thức AWS đã học trong bốn tuần trước, bao gồm Cloud Computing, Networking, Security, Storage, Database và Serverless Computing.

Đây cũng là giai đoạn chuyển tiếp từ việc tìm hiểu công nghệ sang nghiên cứu và xây dựng Project cuối kỳ thực tập.

Kết quả mong đợi sau tuần này là xác định được hướng nghiên cứu, phạm vi, mục tiêu và kế hoạch thực hiện Project trong năm tuần tiếp theo, tạo tiền đề cho quá trình thiết kế, phát triển, kiểm thử và hoàn thiện sản phẩm.
