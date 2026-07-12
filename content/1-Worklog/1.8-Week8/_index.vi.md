---
title: "Worklog Tuần 8"
date: 2026-06-22
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
### Mục tiêu tuần 8:

* Tìm hiểu sâu về các tác vụ bảo trì cơ sở dữ liệu quan hệ (PostgreSQL/Aurora) với lệnh `VACUUM` và `ANALYZE`.
* Nắm vững kỹ thuật can thiệp vào tầng API Gateway để đóng/mở cổng giao tiếp linh hoạt bằng Stage Variables.
* Xác định và thiết kế luồng Bảo trì hệ thống tự động làm tính năng đặc biệt cho dự án.
* Hoàn thiện và đối chiếu toàn bộ sơ đồ hệ thống cuối cùng.
* Tổng duyệt lại kiến trúc và lập kế hoạch triển khai cụ thể, phân công công việc từng nhóm chức năng cho các thành viên.

### Các công việc cần triển khai trong tuần này:

| Thứ               | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                           | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------ | ----------------- |
| 2                  | - Tìm hiểu DB Maintenance:<br />+ Lệnh `VACUUM`: dọn dẹp dead tuples.<br />+ Lệnh `ANALYZE`: cập nhật statistics cho query planner.<br />- Tìm hiểu API Gateway: Cách dùng SDK để update `stageVariables`, điều hướng traffic sang trang bảo trì hoặc trả về mã lỗi 503 khi cần thiết.                                                                                                          | 22/06/2026       | 22/06/2026         |                   |
| 3                  | - Hoàn thiện, thống nhất và review sơ đồ kiến trúc.<br />- Lập kế hoạch: Phân tách hệ thống thành các module nhỏ, chia nhóm triển khai và phân công nhiệm vụ cụ thể cho từng thành viên.                                                                                                                                                                                                           | 23/06/2026       | 23/06/2026         |                   |
| 4 - 5 - 6 - 7 - CN | - Triển khai và viết báo cáo step by step cho:<br />+ Hạ tầng cơ sở: IAM Role, chính sách, tính toán chi phí thực tế với trường hợp tiêu cực nhất, thiết lập hạn mức quản lý chi phí bằng AWS Budget.<br />+ Lớp biên mạng: triển khai nhanh CloudFront, WAF bằng CloudFormation (tại Mỹ).<br />+ Cơ sở dữ liệu: AuroraSQL, triển khai nhanh AWS Backup với AWS S3 bằng CloudFormation. | 24/06/2026       | 28/06/2026         |                   |

### Kết quả đạt được tuần 8:

* Nắm vững cơ chế bảo trì cơ sở dữ liệu (Aurora/PostgreSQL) thông qua lệnh `VACUUM` để dọn dẹp dữ liệu thừa và `ANALYZE` để tối ưu hóa trình lên kế hoạch truy vấn.
* Tìm hiểu cách sử dụng SDK để can thiệp vào API Gateway, linh hoạt cập nhật `stageVariables` nhằm tự động điều hướng traffic sang luồng bảo trì hoặc ngắt kết nối để bảo vệ hệ thống.
* Hoàn thiện, review và thống nhất được sơ đồ kiến trúc hệ thống tổng thể cuối cùng, đảm bảo tính liên kết chặt chẽ giữa các thành phần.
* Lập thành công kế hoạch triển khai chi tiết: phân rã hệ thống thành các module nhỏ, chia nhóm và phân công nhiệm vụ rõ ràng cho từng thành viên trong dự án.
* Hoàn thành triển khai thực tế và viết báo cáo hướng dẫn cho các hạng mục nền tảng:
  * Hạ tầng cơ sở: Khởi tạo thành công IAM Role, các chính sách bảo mật, tính toán rủi ro chi phí thực tế cho kịch bản tiêu cực nhất và cấu hình cảnh báo an toàn qua AWS Budget.
  * Lớp biên mạng: Ứng dụng CloudFormation để triển khai nhanh chóng hệ thống phân phối CloudFront và tường lửa WAF tại khu vực Mỹ.
  * Cơ sở dữ liệu & Lưu trữ: Khởi tạo AuroraSQL và thiết lập thành công tự động hóa sao lưu dữ liệu sang Amazon S3 thông qua AWS Backup bằng script CloudFormation.
