---
title: "Worklog Tuần 5"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---
### Mục tiêu tuần 5:

* Tìm hiểu các kỹ thuật tối ưu hóa tài nguyên và quản lý tải hệ thống trên AWS.
* Thực hành tư duy thiết kế hệ thống phân tán: chia nhỏ dự án thành các AWS Lambda functions độc lập.
* Nắm bắt cơ chế hoạt động của các dịch vụ hỗ trợ tối ưu: Amazon RDS Proxy, Amazon ElastiCache, Amazon SQS và Elastic Load Balancing.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                         | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu / Ghi chú                                                                                                                                |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2    | - Phân tích cấu trúc dự án và thiết kế Microservices:<br />+ Chia nhỏ logic ứng dụng thành các hàm AWS Lambda độc lập.<br />+ Xác định ranh giới và cách các hàm giao tiếp với nhau. | 01/06/2026       | 01/06/2026         |                                                                                                                                                             |
| 3    | - Tìm hiểu tối ưu hóa Database connections:<br />+ Vấn đề cạn kiệt kết nối khi dùng Lambda với RDS.<br />+ Giải pháp Connection Pooling sử dụng Amazon RDS Proxy.                              | 02/06/2026       | 02/06/2026         |                                                                                                                                                             |
| 4    | - Tìm hiểu tối ưu tốc độ đọc:<br />+ Cơ chế hoạt động của Amazon ElastiCache.<br />+ Sự khác biệt cơ bản giữa Redis và Memcached.<br />+ Áp dụng cache để giảm tải Database.        | 03/06/2026       | 03/06/2026         | Lý thuyết khác xa thực hành, việc áp dụng Cache cho xử lý bất đồng bộ gần như bất khả thi và không thực dụng cho nhu cầu hiện tại. |
| 5    | - Tìm hiểu xử lý bất đồng bộ và Decoupling:<br />+ Amazon SQS.<br />+ Cách dùng SQS làm buffer giữa các dịch vụ để tránh quá tải hệ thống.                                                | 04/06/2026       | 04/06/2026         |                                                                                                                                                             |
| 6    | - Tìm hiểu phân phối tải (Load Balancing cho EC2):<br />+ Elastic Load Balancing cơ bản.<br />+ Phân biệt Application Load Balancer và Network Load Balancer.                                        | 05/06/2026       | 05/06/2026         |                                                                                                                                                             |

### Kết quả đạt được tuần 5:

* Đã hình thành tư duy chuyển đổi từ kiến trúc Monolithic sang Serverless Microservices thông qua việc phân rã dự án thành nhiều hàm AWS Lambda thực hiện các tác vụ chuyên biệt.
* Nắm rõ được nguyên nhân gây nghẽn kết nối cơ sở dữ liệu khi Lambda scale up đột ngột và cách RDS Proxy duy trì, tái sử dụng các kết nối để bảo vệ database.
* Hiểu cách tăng tốc độ phản hồi của ứng dụng và giảm tải cho CSDL chính bằng cách lưu trữ dữ liệu thường xuyên truy xuất vào bộ nhớ đệm  Amazon ElastiCache.
* Nắm được khái niệm tách rời các thành phần hệ thống bằng Amazon SQS. Biết cách thiết kế hệ thống chịu được lượng truy cập tăng vọt đột biến bằng cách đưa các luồng xử lý nặng vào hàng đợi để xử lý bất đồng bộ.
* Phân biệt được các lớp mạng hoạt động của ALB và NLB, từ đó biết cách chọn Load Balancer phù hợp để phân phối đều traffic đến các target.
