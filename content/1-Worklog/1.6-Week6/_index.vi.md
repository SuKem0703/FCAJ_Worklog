---
title: "Worklog Tuần 6"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---
### Mục tiêu tuần 6:

* Tìm hiểu các dịch vụ lưu trữ và sao lưu dữ liệu trên AWS: Amazon S3 và AWS Backup.
* Khảo sát giải pháp sử dụng AWS Lambda để tự động export cơ sở dữ liệu nhằm tối ưu chi phí lưu trữ ngoài AWS.
* Tạm gác các tác vụ Cloud, quay lại môi trường Node.js để giải quyết bài toán cốt lõi của backend game: Thiết kế hệ thống chống gian lận vật phẩm bằng kỹ thuật sinh số ngẫu nhiên dựa trên `master seed`.

### Các công việc cần triển khai trong tuần này:

| Thứ      | Công việc                                                                                                                                                                                                                                                                                                                                                       | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu / Ghi chú                                                                                                  |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| 2         | - Tìm hiểu dịch vụ Amazon S3:<br />+ Các phân khúc lưu trữ.<br />+ Versioning và bảo mật Bucket Policies.<br />+ Tìm hiểu tổng quan về AWS Backup.                                                                                                                                                                                            | 08/06/2026       | 08/06/2026         |                                                                                                                               |
| 3         | - Khảo sát giải pháp backup tự chế:<br />+ Lên ý tưởng dùng Lambda trigger theo lịch để export CSDL ra file và đẩy lên S3.<br />+ Đánh giá chi phí và tính khả thi của giải pháp.                                                                                                                                                  | 09/06/2026       | 09/06/2026         | Giải giáp không cần thiết do dịch vụ Backup tiêu chuẩn đã khá rẻ và dữ liệu thuần văn bản nên rất nhẹ. |
| 4 - 5 - 6 | - Tìm hiểu kỹ thuật Deterministic Random.<br />- Xây dựng thuật toán sinh số giả ngẫu nhiên dựa trên `master seed` được cấp phát từ server.<br />- Tích hợp và kiểm thử:<br />+ Server tạo và lưu trữ seed cho session.<br />+ Validate kết quả vật phẩm client gửi lên bằng cách chạy lại chuỗi seed trên server | 10/06/2026       | 12/06/2026         |                                                                                                                               |

### Kết quả đạt được tuần 6:

* Nắm vững cách quản lý đối tượng tĩnh trên Amazon S3 và cách thiết lập các chính sách vòng đời để tối ưu chi phí lưu trữ dài hạn.
* Hoàn thành đánh giá giải pháp dùng AWS Lambda để tự động export database lưu trữ riêng.
* Củng cố kỹ năng lập trình backend với Node.js thông qua việc giải quyết bài toán thực tế trong phát triển game đa người chơi.
* Thiết kế và triển khai thành công cơ chế  Deterministic Random:
  * Hiểu được nguyên lý chống gian lận: Client không tự quyết định kết quả rơi vật phẩm, mọi con số ngẫu nhiên đều được sinh ra từ một `master seed`.
  * Xây dựng luồng đồng bộ: Server tạo `master seed` khi bắt đầu màn chơi và gửi cho Client. Khi Client báo cáo kết quả rớt đồ, Server chỉ việc dùng chính seed đó để mô phỏng lại thao tác. Nếu kết quả trùng khớp, vật phẩm mới được ghi nhận.
  * Phương pháp này giúp hệ thống chống hack hiệu quả mà vẫn đảm bảo Server không bị quá tải do không phải liên tục tính toán tỷ lệ cho từng quái vật bị tiêu diệt.
