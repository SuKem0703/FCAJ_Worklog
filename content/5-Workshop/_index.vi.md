---
title: "Workshop"
date: 2026-06-18
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
# Nghiên cứu và Triển khai Hệ thống Máy chủ cho Trò chơi Trực tuyến

#### Tổng quan

Hệ thống máy chủ xử lý dữ liệu đóng vai trò cốt lõi trong việc quản lý trạng thái, đồng bộ dữ liệu thời gian thực và bảo mật thông tin người chơi. Đối với các dòng game có tần suất tương tác liên tục, việc tối ưu hóa hạ tầng để đạt độ trễ tối thiểu và khả năng chịu tải linh hoạt là yếu tố quyết định trải nghiệm người dùng.

Trong đề tài này, chúng ta sẽ nghiên cứu cách thiết kế, cấu hình và triển khai một kiến trúc máy chủ toàn diện trên nền tảng điện toán đám mây AWS, kết hợp các giải pháp lưu trữ tối ưu nhằm đảm bảo an toàn dữ liệu và tối ưu hóa chi phí vận hành.

Hệ thống phân tách luồng dữ liệu và xử lý thành hai mô hình chiến lược tùy thuộc vào đặc thù luồng traffic:

+ **Cơ chế xử lý đồng bộ (Compute Layer)** - Sử dụng máy chủ trung gian phối hợp với hệ thống cân bằng tải để điều phối các truy vấn API dạng văn bản, hoặc chuyển dịch sang kiến trúc phi máy chủ để tự động co giãn theo lượng người chơi trong thời gian thực.
+ **Cơ chế lưu trữ đa tầng (Database Layer)** - Phân cấp dữ liệu thông qua hệ quản trị cơ sở dữ liệu quan hệ bảo mật cao đặt trong phân vùng mạng riêng tư, kết hợp lớp bộ nhớ đệm để giảm tải và tăng tốc độ phản hồi cho các tác vụ đọc/ghi lặp đi lặp lại.

#### Nội dung

1. [Tổng quan về kiến trúc hệ thống](5.1-architecture-overview/)
2. [Khởi tạo Hạ tầng Cơ sở và Quản lý](5.2-management/)
3. [Xây dựng Cơ sở dữ liệu và Sao lưu](5.3-database/)
4. [Kiến trúc dự án](5.4-architecture-overview/)
5. [Khởi tạo Amazon API Gateway](5.5-API-Gateway/)
6. [Amazon SQS FIFO](5.6-sqs-fifo/)
7. [AWS DLQ &amp; AWS CloudWatch](5.7-sqs-dlq/)
8. [AWS EventBridge](5.8-eventbridge/)
9. [AWS Backup](5.9-aws-backup/)
10. [Kiểm tra kết quả và thực nghiệm](5.10-verification-and-testing/)
11. [Dọn dẹp tài nguyên](5.11-clean-up/)
12. [Khó khăn và hướng phát triển](5.12-challenges-and-future/)
