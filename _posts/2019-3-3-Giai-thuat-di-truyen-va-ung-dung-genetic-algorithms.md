---
layout: post
title: Giải thuật di truyền và ứng dụng với python
mathjax: true
---

Chào các bạn mình là **Sơn Nguyễn** ở trong bài viết này mình sẽ hướng dẫn các bạn hiểu cũng như xây dựng một chương trình đơn giản với giải thuật di truyền. Để các bạn có thể ứng dụng giải thuật di truyền vào những bài toán cụ thể của các bạn. Trong các lĩnh vực khác của khoa học máy tính.

#Mục lục
+ **Giới thiệu ngắn gọn về thuật toán di truyền**
+ **Mục tiêu các vấn đề cần giải quyết**
+ **Dự án đầu tiên**
+ **Lập trình di truyền với python**
+ **Hello world**
- **Đoán số của tôi**
- **Đoán mật khẩu**


## Giới thiệu ngắn gọn về thuật toán di truyền
Thuật toán di truyền là một trong những công cụ chúng ta có thể sử dụng để áp dụng cho các thuật toán học máy cho các bài toán tìm kiếm, tối ưu, và để giải quyết các vấn đề có hàng tỷ giải pháp có thể giải. Ý tưởng chính bắt nguồn từ sinh học để trả lời cho các vấn đề có không gian tìm kiếm lớn bằng cách liên tục tạo ra các giải pháp và đánh giá độ **tốt** của các giải pháp phù hợp với kết quả mong muốn, và tinh chỉnh các giải pháp tốt nhất.

Khi giải quyết vấn đề bằng thuật toán di truyền, thay vì yêu cầu một giải pháp cụ thể, bạn cung cấp các đặc điểm mà giải pháp **phải có** để giải pháp đó được chấp nhận. Ví dụ khi bạn muốn đổ đầy một chiếc xe tải đang di chuyển bạn cung cấp một bộ quy tắc như: đặt những thứ lớn lên trước, phân bổ cân bằng trọng lượng của xe. đặt những thứ nhẹ lên trên nhưng không được lỏng lẻo, lồng những thứ có hình dạng kỳ lạ để chúng không di chuyển xung quanh.


## Mục tiêu các vấn đề cần giải quyết
