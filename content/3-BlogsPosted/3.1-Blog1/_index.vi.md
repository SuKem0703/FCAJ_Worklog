---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
### **Sử dụng Amazon CloudFront để tăng tốc và tối ưu quá trình xử lý yêu cầu của người dùng**

![Có thể là đồ họa về sơ đồ tầng, bản thiết kế và văn bản cho biết 'Amazon CloudFront Viewers Origin server 白白白官 Edge locations Regional edge caches'](https://scontent.fsgn2-6.fna.fbcdn.net/v/t39.30808-6/739508936_1519848743226069_530702931998462867_n.jpg?stp=dst-jpg_tt6&cstp=mx907x550&ctp=s907x550&_nc_cat=111&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeFSBVyckJD3jWyYfZhaV-tLR0emncwW07NHR6adzBbTsz7np6e_WGnm_e4YURaHkMwDXupoxzTOPCAU_8NhWNV1&_nc_ohc=Y9slTg22QTsQ7kNvwEZQtp-&_nc_oc=Ado5B4-ADRLb7Ag9QUEEtpc-OwgABzZgeCG8kPUgbrL_yB_xuH3nC8uKWKKE72aySScd3en9Os7kkILZI1iOs7Q5&_nc_zt=23&_nc_ht=scontent.fsgn2-6.fna&_nc_gid=AXqlakUu8H6izJwOgiRN3w&_nc_ss=7b2a8&oh=00_AQDQP2cDs_7eBdP8dle4TSbCgkSNfnFIiNT8eWuQCYpDTg&oe=6A5ADE88)

#### 3.1.1 Amazon CloudFront là gì?

CloudFront hoạt động bằng cách đặt các bản sao nội dung tại nhiều Edge Location trên toàn thế giới. Khi người dùng gửi request, CloudFront sẽ kiểm tra xem nội dung đã được lưu trong bộ nhớ đệm (cache) tại Edge Location gần nhất hay chưa.

* Nếu  đã có trong cache (Cache Hit) , CloudFront sẽ trả dữ liệu ngay từ Edge Location mà không cần truy cập đến máy chủ gốc (Origin).
* Nếu  chưa có trong cache (Cache Miss) , CloudFront sẽ chuyển request đến Origin (ví dụ như Amazon S3, API Gateway hoặc Application Load Balancer), lấy dữ liệu, trả về cho người dùng và đồng thời lưu vào cache để phục vụ các request tiếp theo.

Nhờ cơ chế này, CloudFront giúp rút ngắn thời gian phản hồi và cải thiện đáng kể trải nghiệm của người dùng trên phạm vi toàn cầu.

#### 3.1.2 Điểm nổi bật & lợi ích cốt lõi

Điểm mình thấy ấn tượng nhất ở Amazon CloudFront là khả năng  tăng hiệu năng đồng thời giảm tải cho hệ thống phía sau .

Một số lợi ích nổi bật gồm:

* Giảm độ trễ (Low Latency): Người dùng nhận dữ liệu từ Edge Location gần nhất thay vì phải kết nối trực tiếp đến Origin ở khoảng cách địa lý xa.
* Tăng tốc độ tải nội dung: Các nội dung được truy cập thường xuyên sẽ được cache tại Edge Location, giúp phản hồi nhanh hơn nhiều so với việc luôn truy vấn về Origin.
* Giảm tải cho Origin: Khi nhiều người dùng cùng truy cập một nội dung, phần lớn request sẽ được phục vụ từ cache, giúp giảm số lượng request gửi đến Amazon S3, API Gateway hoặc máy chủ ứng dụng.
* Tiết kiệm chi phí: Việc giảm số lần truy cập Origin cũng giúp giảm chi phí tính theo request hoặc băng thông của các dịch vụ phía sau.
* Tăng cường bảo mật: CloudFront có thể tích hợp với AWS WAF để lọc các request độc hại trước khi chúng đến ứng dụng, góp phần bảo vệ hệ thống khỏi nhiều hình thức tấn công phổ biến.

#### 3.1.3 Các trường hợp sử dụng lý tưởng

Amazon CloudFront phù hợp với nhiều loại ứng dụng khác nhau, đặc biệt là những hệ thống cần phục vụ lượng lớn người dùng hoặc có phạm vi truy cập toàn cầu.

Một số trường hợp sử dụng phổ biến:

* Phân phối website tĩnh được lưu trữ trên Amazon S3.
* Tăng tốc API khi kết hợp với Amazon API Gateway.
* Phân phối hình ảnh, video và các nội dung đa phương tiện.
* Cung cấp file tải xuống như phần mềm, tài liệu hoặc bản cập nhật.
* Hỗ trợ các ứng dụng web có lượng truy cập lớn cần giảm tải cho máy chủ gốc.

#### 3.1.4 Ví dụ thực tế

Giả sử một website bán hàng lưu toàn bộ hình ảnh sản phẩm trên Amazon S3 và sử dụng CloudFront để phân phối nội dung.

Khi khách hàng đầu tiên truy cập hình ảnh của một sản phẩm:

1. Request được gửi đến CloudFront.
2. CloudFront chưa tìm thấy hình ảnh trong cache (Cache Miss).
3. CloudFront lấy hình ảnh từ Amazon S3.
4. Hình ảnh được trả về cho người dùng và đồng thời được lưu vào Edge Location.

Những khách hàng tiếp theo trong cùng khu vực khi truy cập hình ảnh đó sẽ nhận dữ liệu trực tiếp từ Edge Location (Cache Hit) mà không cần truy cập lại Amazon S3.

Nhờ vậy:

* Hình ảnh tải nhanh hơn.
* Amazon S3 nhận ít request hơn.
* Website vẫn hoạt động ổn định ngay cả khi có nhiều người dùng truy cập cùng lúc.

#### 3.1.5 Kết luận

Sau khi tìm hiểu về Amazon CloudFront, mình hiểu rõ hơn cách một dịch vụ CDN giúp cải thiện hiệu năng của hệ thống thông qua cơ chế cache tại các Edge Location trên toàn cầu.

Điều mình thấy giá trị nhất là CloudFront không chỉ giúp tăng tốc độ truy cập cho người dùng mà còn giảm tải cho Origin, tối ưu chi phí vận hành và có thể kết hợp với AWS WAF để tăng cường bảo mật. Đây là một dịch vụ rất hữu ích khi xây dựng các ứng dụng web hoặc kiến trúc serverless trên AWS, đặc biệt với những hệ thống cần khả năng mở rộng và phục vụ người dùng ở nhiều khu vực khác nhau.

Hy vọng bài chia sẻ này sẽ hữu ích với mọi người. Nếu anh chị và các bạn đã từng triển khai Amazon CloudFront trong thực tế, rất mong được cùng trao đổi và học hỏi thêm.

**Nguồn tham khảo:** [https://aws.amazon.com/vi/blogs/networking-and-content-delivery/charting-the-life-of-an-amazon-cloudfront-request/](https://aws.amazon.com/vi/blogs/networking-and-content-delivery/charting-the-life-of-an-amazon-cloudfront-request/)
