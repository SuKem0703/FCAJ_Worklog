---
title: "Worklog Tuần 7"
date: 2026-06-15
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---
### Mục tiêu tuần 7:

* Xây dựng sơ đồ kiến trúc hệ thống tổng thể cho dự án thực tiễn.
* Tham khảo, theo dõi và đánh giá chéo các bài tập/dự án của bạn học để chắt lọc những giải pháp tối ưu áp dụng vào dự án nhóm.
* Khảo sát, vẽ thử và phân tích ưu/nhược điểm của nhiều biến thể kiến trúc khác nhau: Server truyền thống, Serverless, và kiến trúc lai.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                     | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------ | ----------------- |
| 2    | - Theo dõi các đánh giá dự án của bạn học:<br />+ Phân tích các mô hình kiến trúc nhóm khác sử dụng.<br />+ Thảo luận nhóm để chọn lọc ý tưởng phù hợp cho dự án chung. | 15/06/2026       | 15/06/2026         |                   |
| 3    | - Thiết kế kiến trúc Server truyền thống:<br />+ Vẽ sơ đồ: EC2 + RDS + Load Balancer.<br />+ Đánh giá khả năng scale và chi phí vận hành.                                                 | 16/06/2026       | 16/06/2026         |                   |
| 4    | - Thiết kế kiến trúc lai:<br />+ Mô hình 1: EC2 + Supabase + Supabase Pooling.<br />+ Mô hình 2: EC2 + RDS + RDS Proxy + Load Balancer.                                                              | 17/06/2026       | 17/06/2026         |                   |
| 5    | - Thiết kế kiến trúc Serverless thuần:<br />+ Mô hình 1: Lambda + AuroraDB + RDS Proxy.<br />+ Lambda + AuroraDB + ElastiCache + RDS Proxy.                                                           | 18/06/2026       | 18/06/2026         |                   |
| 6    | - Tổng hợp và chốt sơ đồ dự án thực tiễn:<br />+ So sánh: độ trễ, chi phí, khả năng bảo trì giữa các biến thể.<br />+ Chốt sơ đồ kiến trúc cuối cùng cho dự án nhóm.      | 19/06/2026       | 19/06/2026         |                   |

### Kết quả đạt được tuần 7:

* Đã hoàn thành quá trình review và đánh giá chéo bài tập của các bạn học, qua đó rút ra được nhiều góc nhìn mới mẻ về cách phân bổ tài nguyên và xử lý luồng dữ liệu để cân nhắc áp dụng vào dự án thực tiễn của nhóm.
* Hoàn thành việc vẽ nháp và trực quan hóa 5 biến thể sơ đồ kiến trúc hạ tầng:
  * Kiến trúc truyền thống: `EC2 + RDS + Load Balancer` - Dễ tiếp cận, dễ hình dung nhưng tốn chi phí duy trì cố định và cần setup Auto Scaling cẩn thận.
  * Kiến trúc lai 1: `EC2 + Supabase + Supabase Pooling` - Kết hợp khả năng tính toán truyền thống của EC2 với Backend-as-a-Service (Supabase), tận dụng tính năng pooling có sẵn của Supabase để giảm tải số lượng kết nối trực tiếp vào Postgres.
  * Kiến trúc lai 2: `EC2 + RDS + RDS Proxy + Load Balancer` - Giải quyết bài toán nghẽn kết nối Database của mô hình truyền thống khi EC2 scale-out thông qua lớp đệm RDS Proxy.
  * Kiến trúc Serverless 1: `Lambda + AuroraDB + RDS Proxy` - Tối ưu chi phí theo lượt dùng. RDS Proxy đóng vai trò sống còn ở đây để giữ connection pool, ngăn Lambda tạo ra quá nhiều kết nối mới đánh sập AuroraDB khi có lượng truy cập đột biến.
  * Kiến trúc Serverless 2: `Lambda + AuroraDB + ElastiCache + RDS Proxy` - Mô hình toàn diện nhất. Thêm ElastiCache vào để làm bộ nhớ đệm, giúp giảm thiểu đáng kể số vòng truy vấn xuống DB, tăng tốc độ phản hồi xuống mức thấp nhất. Tuy nhiên, chi phí lại vượt quá mức cần thiết và không phù hợp với quy mô dự án hiện tại.
* Việc vẽ ra nhiều biến thể giúp team có cái nhìn trực quan nhất về sự đánh đổi giữa Khả năng bảo trì, Hiệu năng và Chi phí. Dựa vào các bản phác thảo này, nhóm đã có đủ cơ sở để chốt kiến trúc hệ thống tổng thể cho dự án.
