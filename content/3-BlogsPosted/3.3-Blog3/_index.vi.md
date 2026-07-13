---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
### Xây dựng hệ thống AI đa người dùng an toàn hơn với Amazon Bedrock

Chào mọi người, hôm nay mình muốn chia sẻ một bài viết khá hay của AWS về cách PAR Technology xây dựng hệ thống AI sử dụng Amazon Bedrock nhưng vẫn đảm bảo mỗi người dùng chỉ được xem đúng dữ liệu mà mình có quyền truy cập.

PAR là công ty cung cấp các giải pháp công nghệ cho nhiều chuỗi nhà hàng. Họ phát triển một hệ thống cho phép người dùng đặt câu hỏi bằng ngôn ngữ tự nhiên, sau đó AI sẽ tự tạo câu lệnh SQL để lấy dữ liệu và trả lời. Ý tưởng nghe khá đơn giản, nhưng khi triển khai thực tế lại phát sinh một bài toán rất quan trọng là bảo mật dữ liệu.

![](https://scontent.fsgn2-8.fna.fbcdn.net/v/t39.30808-6/739699246_1520665259811084_3979309470280326443_n.jpg?stp=dst-jpg_tt6&cstp=mx853x497&ctp=s853x497&_nc_cat=102&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeGN4VpncdwfE0TYbKBi_HNoU0D3pXbypQRTQPeldvKlBBizMZPvCbF7IAWQw1XtrqEIXNncD3mSiJcTmmWhoAbR&_nc_ohc=zX7azuzigUoQ7kNvwEuuE9m&_nc_oc=Adowc2XcccTmhpEkOLjW_qMnTrdTBAZTtNr4hkMUv37wo7xelVUzan6F4CbdzRjH_dg5sgHKWKf-JkQj2GUhTh6r&_nc_zt=23&_nc_ht=scontent.fsgn2-8.fna&_nc_gid=a6DHMTKRpeUham_BJUritA&_nc_ss=7b2a8&oh=00_AQDtaOshej61mUQGDMSSUm9fvsou8L3jHxnbkEFnU6hnjQ&oe=6A5AC9DB)

![img](https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/739620942_1520665423144401_5066396045548758978_n.jpg?stp=dst-jpg_tt6&cstp=mx857x430&ctp=s857x430&_nc_cat=101&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeEluZTeMDzHbgzfhVKc-dQU-VE6hT63A935UTqFPrcD3eXcLd2NsSV6Z7hMj-71X7cj_5lSLMPVmG1Q-CX0B6VJ&_nc_ohc=8auVoYRlI0wQ7kNvwHkKmsp&_nc_oc=AdpgLJJoxLplOtNLxST0lkp4eUExr8z-Spt3XRtuRCak5qals8lF00pP9cKyaZ9DEWcGP63B6Ju3U3YC8Of32Jhr&_nc_zt=23&_nc_ht=scontent.fsgn2-4.fna&_nc_gid=a6DHMTKRpeUham_BJUritA&_nc_ss=7b2a8&oh=00_AQDCNDWhlp5cSXe5kyXqqAP5TBg45K-Ht7l2BpYGKOELsg&oe=6A5AE51A)

#### 3.3.1 Bài toán gặp phải

Trong hệ thống của PAR, có rất nhiều khách hàng cùng sử dụng chung một nền tảng. Ví dụ, chủ một cửa hàng chỉ được xem doanh thu của cửa hàng mình, trong khi quản lý cấp cao có thể xem doanh thu của toàn bộ chuỗi.

Nếu AI tạo truy vấn không đúng hoặc lấy nhầm dữ liệu thì người dùng có thể nhìn thấy thông tin mà họ không được phép truy cập. Đây là vấn đề rất nghiêm trọng đối với các hệ thống doanh nghiệp.

#### 3.3.2 Giải pháp của PAR

Thay vì để AI tự quyết định tất cả, PAR xây dựng hệ thống với nhiều lớp bảo vệ.

Đầu tiên, mọi yêu cầu đều được xác thực danh tính để đảm bảo người gửi là hợp lệ. Sau đó, hệ thống sẽ kiểm tra câu hỏi của người dùng có rõ ràng và phù hợp hay không trước khi chuyển cho AI xử lý.

Quan trọng nhất là dữ liệu sẽ được lọc theo quyền truy cập của từng người dùng trước khi AI tạo câu lệnh SQL. Điều này giúp AI chỉ làm việc trên phần dữ liệu đã được cấp quyền, thay vì toàn bộ cơ sở dữ liệu.

#### 3.3.3 Vì sao cách làm này hiệu quả?

Điểm mình thấy hay là AWS và PAR không đặt toàn bộ niềm tin vào LLM. AI chỉ chịu trách nhiệm hiểu câu hỏi và hỗ trợ tạo SQL, còn việc kiểm soát quyền truy cập vẫn do hệ thống xử lý.

Nhờ vậy, ngay cả khi AI tạo truy vấn chưa chính xác hoặc bị tác động bởi các prompt không mong muốn thì dữ liệu ngoài phạm vi cho phép vẫn không thể bị truy cập.

#### 3.3.4 Kết quả đạt được

Theo bài viết, kiến trúc này đã được sử dụng trong môi trường thực tế và xử lý hơn 50.000 truy vấn mà không xảy ra tình trạng rò rỉ dữ liệu giữa các người dùng.

Ngoài việc tăng tính bảo mật, cách thiết kế này cũng giúp doanh nghiệp yên tâm hơn khi triển khai các ứng dụng AI trên dữ liệu quan trọng.

#### 3.3.5 Cảm nhận của mình

Theo mình, đây là một bài học khá thú vị khi xây dựng ứng dụng AI. Trước đây mình thường nghĩ chỉ cần chọn một mô hình LLM tốt là đủ, nhưng thực tế việc thiết kế kiến trúc và kiểm soát quyền truy cập còn quan trọng hơn.

Amazon Bedrock giúp việc xây dựng ứng dụng AI trở nên thuận tiện, nhưng để hệ thống hoạt động an toàn thì vẫn cần kết hợp với các cơ chế xác thực, phân quyền và lọc dữ liệu ngay từ đầu.

#### 3.3.6 Kết luận

Qua bài viết này mình thấy AI không nên là thành phần duy nhất quyết định việc truy cập dữ liệu. Khi kết hợp Amazon Bedrock với các lớp bảo mật phù hợp, doanh nghiệp có thể xây dựng những hệ thống AI vừa thông minh, vừa an toàn và đáng tin cậy hơn.

Link tham khảo: https://aws.amazon.com/vi/blogs/machine-learning/multi-tenant-llm-analytics-with-row-level-security-how-we-built-a-secure-agent-on-aws/
