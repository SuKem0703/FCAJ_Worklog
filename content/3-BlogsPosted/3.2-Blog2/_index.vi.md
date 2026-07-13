---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
### Amazon EKS Hỗ Trợ Truyền Dữ Liệu Từ Mặt Phẳng Điều Khiển Thông Qua VPC Của Bạn

Trong quá trình tìm hiểu về Amazon EKS, mình thấy AWS vừa giới thiệu tính năng Customer-Routed Control Plane Egress. Tính năng này cho phép lưu lượng từ Control Plane của Kubernetes được định tuyến thông qua Amazon VPC của khách hàng, giúp tăng khả năng kiểm soát và bảo mật hệ thống.

![Có thể là đồ họa về bản thiết kế, sơ đồ tầng và văn bản cho biết 'AWS Cloud AWS Region Amazon EKS Control Plane (managed) Your VPC kube-apiserver Your egress controls (choose any combination) 四 (EKS-managed) ENI your FC) EKS managed control plane trafic ออศรัทนอย ovor EKS managed network path governed your ogress contrals Customer destinations Admission wubhcok OIDC provider Legend Apgregate PI server Amazon EKS ENI VPC endpeint Transi Gatoway NAT Gateway PrivateLin'](https://scontent.fsgn2-7.fna.fbcdn.net/v/t39.30808-6/740769954_1520636753147268_6569374290610978119_n.jpg?stp=dst-jpg_tt6&cstp=mx921x535&ctp=s921x535&_nc_cat=100&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeEOWx61b8hA-5lYmEZhNsUWtNIwVyoUDzO00jBXKhQPM4hEyspulfaaBTEAx91gOQMo0e7_7o8Dz4UHRcFbWZDv&_nc_ohc=ML7L_ZDcrM4Q7kNvwEnLSLA&_nc_oc=Adq3MoZ5E_hTO2UC1-p_vnFKYBkjtRQyLc3odd_yb5sHE9fc004NAD-WzRypuvg4qXNTgwLfjqQLWC5vSjj1ubO9&_nc_zt=23&_nc_ht=scontent.fsgn2-7.fna&_nc_gid=dFpWsQnnBiVpmAoj6RTC4g&_nc_ss=7b2a8&oh=00_AQCEW_p70XQFIbV6a_QUzd8jNbkye_D0uos5c9mvKIuTjQ&oe=6A5ADFC7)

#### 3.2.1 Amazon EKS là gì?

Amazon Elastic Kubernetes Service (Amazon EKS) là dịch vụ Kubernetes được AWS quản lý. Dịch vụ này giúp người dùng triển khai và vận hành Kubernetes dễ dàng hơn mà không cần tự quản lý Control Plane. Ngoài ra, EKS còn tích hợp với nhiều dịch vụ AWS như IAM, VPC và CloudWatch để hỗ trợ quản lý và giám sát hệ thống.

#### 3.2.2 Điểm mới của tính năng

Trước đây, lưu lượng từ Kubernetes Control Plane được xử lý theo hạ tầng mạng do AWS quản lý. Với tính năng mới, lưu lượng này có thể đi qua chính Amazon VPC của khách hàng thông qua Elastic Network Interface (ENI). Nhờ đó, người quản trị có thể áp dụng các công cụ như Security Group, Route Table, VPC Endpoint hoặc AWS Network Firewall để kiểm soát lưu lượng mạng tốt hơn.

#### 3.2.3 Lợi ích

Theo mình, tính năng này mang lại nhiều lợi ích như:

* Tăng khả năng kiểm soát lưu lượng mạng.
* Nâng cao tính bảo mật cho hệ thống.
* Hỗ trợ đáp ứng các yêu cầu về kiểm toán và tuân thủ.
* Thuận tiện khi sử dụng các dịch vụ xác thực hoặc hệ thống nội bộ.

#### 3.2.4 Một số lưu ý

Khi sử dụng chế độ CUSTOMER_ROUTED, người quản trị cần cấu hình mạng chính xác vì việc định tuyến sẽ do doanh nghiệp tự quản lý. Do đó, nên kiểm tra kỹ trước khi triển khai trên môi trường thực tế.

#### 3.2.5 Đánh giá cá nhân

Theo mình, đây là một cập nhật khá hữu ích của Amazon EKS. Tính năng này giúp doanh nghiệp chủ động hơn trong việc quản lý lưu lượng và tăng cường bảo mật khi triển khai Kubernetes trên AWS. Đối với sinh viên đang tìm hiểu về Cloud như mình, đây cũng là cơ hội để hiểu rõ hơn cách AWS liên tục cải tiến các dịch vụ nhằm đáp ứng nhu cầu thực tế của người dùng.

#### 3.2.6 Kết luận

Customer-Routed Control Plane Egress là một cải tiến đáng chú ý của Amazon EKS. Việc cho phép định tuyến lưu lượng Control Plane thông qua Amazon VPC giúp hệ thống linh hoạt, an toàn và dễ quản lý hơn. Mình tin rằng tính năng này sẽ được nhiều doanh nghiệp áp dụng khi triển khai Kubernetes trên AWS trong thời gian tới.

Nguồn tham khảo: https://aws.amazon.com/vi/blogs/containers/amazon-eks-now-supports-control-plane-egress-through-your-vpc/
