---
layout: post
title: Bài toán điều phối xe điện với thời gian sạc và di chuyển khác nhau
---

Chào các bạn mình là **Sơn** hôm trước mình được một bạn nữ nhờ nghiên cứu bài toán điều phối xe điện cho đồ án tốt nghiệp của bạn ấy. Do bạn ấy cười xinh và tính dại gái của mình nổi lên và mình đã nhận lời nghiên cứu bài toán này. Đó là lý do bài viêt này ra đời.

Vấn đề định tuyến, điều phối xe điện với thời gian sạc và thời gian di chuyển thay đổi được phát triển để giải quyết một số vấn đề vận hành
xe điện chẳng hạn như giới hạn phạm vi và nhu cầu sạc của xe điện.

Cách giải quyết bài toán là sử dụng giải thuật di chuyền để tìm được các tuyến đường tối ưu, thời gian rời khỏi xe, kế hoạch tính phí.
Trong khi đó một giải thuật Dynamic  Dijkstra tìm đường ngắn nhất giữa hai Node liền kề dọc theo các tuyến đường. Để hạn chế  và ngăn chặn cạn kiệt toàn bộ pin cũng như đảm bảo hoạt động giao thông. Của các xe điện với việc không đủ năng lượng cần sạc lại ở các điểm sạc. Các biến động về thời gian sạc và di chuyển khác nhau thể hiện cho việc sự năng động của các phương tiện giao thông.
 
 ## introduction.
 
 Với khủng hoảng năng lượng và ô nhiễm môi trường, sử dụng năng lượng ví dụ như săng dầu hoặc những chất đốt tương tự đang gây ô nhiễm môi trường và được nhiều quốc gia quan tâm chú ý. 30% khí thải từ hoạt động giao thông gây hiệu ứng nhà kính ở USA. Vì thế việc sử lý hiệu quả, chuyên sâu, và giảm lượng cacbon của hoạt động giao thông là một chủ đề rất được quan tâm. Có hai cách tiếp cận bền vững cho vấn đề này.
Chúng ta sẽ bắt đầu xem sét. Vấn đề công nghệ tái tạo năng lượng và việc sử dụng hiệu quả các phương thức trong vận tải. Một hướng khác phát triển và tái cấu trúc công nghệ năng lượng ví dự như các loại xe AFVs, PHEVs, EVs (các loại xe điện, hoặc các loại xe kết hợp nhiều dạng nguyên liệu) 
