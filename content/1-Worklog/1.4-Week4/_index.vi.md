---
title: "Worklog Tuần 4"
date: 2026-06-25
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

* Hiểu và nắm bắt các khái niệm về kiến trúc Serverless trên nền tảng AWS.
* Làm quen và thực hành với AWS Lambda cùng các dịch vụ cơ sở dữ liệu Serverless (DynamoDB, Aurora).
* Khám phá các dịch vụ thuộc lớp biên mạng và bảo mật: API Gateway, CloudFront, AWS WAF.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------- | ------------------ | ----------------- |
| 2    | - Tìm hiểu kiến trúc Serverless trên AWS:<br />+ Khái niệm Serverless.<br />+ Ưu/nhược điểm so với máy chủ truyền thống.<br />+ Khám phá AWS Lambda.                | 25/06/2026       | 25/06/2026         |                   |
| 3    | - Tìm hiểu các Database hỗ trợ Serverless:<br />+ Amazon DynamoDB.<br />+ Amazon Aurora Serverless.<br />+ Use cases cho từng loại DB.                                          | 26/06/2026       | 26/06/2026         |                   |
| 4    | - Khởi tạo Amazon Aurora.<br />- Thử đóng gói toàn bộ dự án thành một lambda.                                                                                                  | 27/06/2026       | 27/06/2026         |                   |
| 5    | - Tìm hiểu lớp biên mạng:<br />+ Amazon API Gateway.<br />+ Amazon CloudFront.<br />+ AWS WAF.<br />- Sử dụng CloudFormation để khởi tạo lớp biên mạng cho lambda đã làm. | 28/06/2026       | 28/06/2026         |                   |

### Kết quả đạt được tuần 4:

* Hiểu rõ khái niệm Serverless, cách tối ưu hóa chi phí và giảm bớt gánh nặng vận hành máy chủ.
* Nắm được cơ chế hoạt động của AWS Lambda, cấu hình trigger, quyền thực thi.
* Phân biệt được sự khác nhau giữa DynamoDB và Aurora Serverless, cũng như khi nào nên áp dụng loại nào cho dự án.
* Triển khai thành công mô hình Serverless tất cả trong một.
* Hiểu vai trò của các dịch vụ lớp biên:
  * API Gateway:Đóng vai trò là cửa ngõ quản lý và định tuyến các API calls vào Lambda.
  * CloudFront: Hỗ trợ phân phối nội dung đến người dùng cuối với độ trễ thấp nhất.
  * AWS WAF: Cách hoạt động của tường lửa ứng dụng web để chặn các luồng traffic độc hại trước khi chúng chạm đến backend.
* Có khả năng xâu chuỗi các dịch vụ: `End-user -> CloudFront -> API Gateway -> Lambda -> DynamoDB`.
