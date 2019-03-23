---
layout: post
title: Opentracing Theo dõi phân tán là gì ? 
---

Theo dõi phân tán là gì ?
Theo dõi phân tán, còn được gọi là theo dõi request phân tán là một phương pháp được sử dụng để lập hồ sơ và giám sát các ứng dụng 
và đặc biệt là các ứng dụng được xây dựng bằng kiến trúc microservice truy tìm phân tán giúp xác định chính xác nơi xảy ra lỗi và điêuf 
gì gây ra hiệu suất kém.

## Ai sử dụng truy tìm phân tán ?

Các nhóm IT và DevOps có thể sử dụng theo dõi phân tán để giám sát các ứng dụng. Truy tìm phân tán đặc biệt phù hợp để gỡ lỗi và giám sát các
kiến trúc phần mềm phân tán hiện đại, chẳng hạn như microservice. 
Các nhà phát triển có thể sử dụng theo dõi phân tán để giúp gỡ lỗi và tối ưu hóa mã của họ. 

## OpenTracing là gì ?

OpenTracing dễ dàng để bắt đầu ? Câu trả lời là KHÔNG 

- OpenTracing không phải là một chương trình. Nó yêu cầu bạn thêm vào trong code hoặc framework của bạn 
- OpenTracing không phải là một chuẩn, opentracing đang làm việc hướng tới việc tạo ra các API và công cụ
chuẩn hóa hơn cho việc theo dõi phân tán 
OpenTracing bao gồm một loạt đặc tả API, Opentracing cho phép bạn theo dõi các request bằng cách nhúng vào trong code của bạn 

## Concepts and Terminology

Tất cả các API OpenTracing dành riêng cho ngôn ngữ đều có chung một số thuật ngữ cốt lõi 
Các khái niệm này rất quan trọng và quan trọng đối với dự án đến mức chúng có kho lưu trữ riêng 
github.com/opentracing/specification 

