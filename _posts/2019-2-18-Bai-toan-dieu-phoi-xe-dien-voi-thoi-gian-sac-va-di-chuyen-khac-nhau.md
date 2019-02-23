---
layout: post
title: Bài toán điều phối xe điện với thời gian sạc và di chuyển khác nhau
---

Chào các bạn mình là **Sơn** hôm trước mình được một bạn nữ nhờ nghiên cứu bài toán điều phối xe điện cho đồ án tốt nghiệp của bạn ấy. Do bạn ấy cười cũng xinh và tính dại gái của mình nổi lên và mình đã nhận lời nghiên cứu bài toán này. Đó là lý do bài viêt này ra đời.

Vấn đề định tuyến, điều phối xe điện với thời gian sạc và thời gian di chuyển thay đổi được phát triển để giải quyết một số vấn đề vận hành
xe điện chẳng hạn như giới hạn phạm vi và nhu cầu sạc của xe điện.

Cách giải quyết bài toán là sử dụng giải thuật di chuyền để tìm được các tuyến đường tối ưu, thời gian rời khỏi xe, kế hoạch tính phí.
Trong khi đó một giải thuật Dynamic  Dijkstra tìm đường ngắn nhất giữa hai Node liền kề dọc theo các tuyến đường. Để hạn chế  và ngăn chặn cạn kiệt toàn bộ pin cũng như đảm bảo hoạt động giao thông. Của các xe điện với việc không đủ năng lượng cần sạc lại ở các điểm sạc. Các biến động về thời gian sạc và di chuyển khác nhau thể hiện cho việc sự năng động của các phương tiện giao thông.
 
 ## introduction.
 
 Với khủng hoảng năng lượng và ô nhiễm môi trường, sử dụng năng lượng ví dụ như săng dầu hoặc những chất đốt tương tự đang gây ô nhiễm môi trường và được nhiều quốc gia quan tâm chú ý. 30% khí thải từ hoạt động giao thông gây hiệu ứng nhà kính ở USA. Vì thế việc sử lý hiệu quả, chuyên sâu, và giảm lượng cacbon của hoạt động giao thông là một chủ đề rất được quan tâm. Có hai cách tiếp cận bền vững cho vấn đề này.
Chúng ta sẽ bắt đầu xem sét. Vấn đề công nghệ tái tạo năng lượng và việc sử dụng hiệu quả các phương thức trong vận tải. Một hướng khác phát triển và tái cấu trúc công nghệ năng lượng ví dự như các loại xe AFVs, PHEVs, EVs (các loại xe điện, hoặc các loại xe kết hợp nhiều dạng nguyên liệu) 


## Mô tả bài toán 

Giả sử rằng có 20 EV(xe điện) hậu cần có sẵn để giao nhiều hàng hóa từ kho duy nhất cho khách hàng. Yêu cầu tất cả các phương tiện đã sử dụng phải khởi hành từ kho để thực hiện giao hàng và quay trở lại kho được áp dụng. Trong chuyến lưu diễn giữa chừng, những chiếc xe này không được phép quay trở lại kho. Để ngăn chặn sự cạn kiệt của toàn bộ pin, EVs với nguồn pin không đủ có thể được sạc lại tại các trạm sạc nhiều lần trong quá trình vận chuyển.

Một kế hoạch vận hành xe tối ưu bao gồm tuyến đường, thời gian khởi hành xe tại kho, tính phí kế hoạch, và những con đường ngắn nhất có được để đáp ứng khách hàng nhu cầu, đảm bảo an toàn hoạt động và giảm chi phí. Các tuyến đường và thời gian khởi hành xe tại kho. Cần trả lời Hai câu hỏi sau: khách hàng được truy cập như thế nào và khi nào các phương tiện được sử dụng khởi hành từ kho, tương ứng. Các
kế hoạch tính phí là để giải quyết vấn đề như thế nào và khi nào các phương tiện được sử dụng với nhu cầu sạc được sạc lại. Các con đường ngắn nhất là hướng dẫn các phương tiện cách lái xe lớn mạng lưới đường bộ.

Để ngụ ý sơ đồ vận hành xe tối ưu, chúng tôi hiển thị một ví dụ kết quả đơn giản với 10 khách hàng và 8 lần sạc các trạm (tham khảo Hình 1). Kết quả chi tiết là sau: depot-1-9-C2-6-depot (tuyến 1), depot-5-4-7-8-C5-kho (tuyến 2) và kho-2-3-10-kho (tuyến 3)

![Mô tả bài toán tối ưu điều phối xe điện với thời gian khác nhau]({{ site.baseurl }}/images/hinh1_toi-uu.PNG "Mô tả bài toán tối ưu điều phối xe điện với thời gian khác nhau")

Xe trên tuyến 1 rời kho lúc 13:40 để thăm ba khách hàng (1, 9, 6) và cần được sạc lại tại nút C2 trong quá trình vận chuyển. Tương tự, chiếc xe trên tuyến đường 2 rời khỏi kho lúc 15:10 và được sạc lại tại nút C5. Trên tuyến đường 3, chiếc xe có đủ năng lượng pin cho toàn bộ chuyến đi để không có nhu cầu di chuyển đến bất kỳ trạm sạc nào. Bởi vì toàn bộ mạng lưới đường bao gồm thông tin giao lộ lớn không được đưa ra trong Hình 1, các đường dẫn ngắn nhất không được xây dựng. Một trường hợp nghiên cứu thực tế và kết quả hoàn chỉnh tương ứng được trình bày trong Phần 5

Ngoài ra, một thuật toán Dijkstra động được giới thiệu trong Mục 2.3 được đề xuất để giải quyết vấn đề con đường ngắn nhất

2.1. Charging Demand (Nhu cầu sạc pin). Nói chung, Công ty hỗ trợ các xe EV có  điểm sạc tại kho. EV có thể được tính phí trong thời gian nhàn rỗi (ví dụ: thời gian ban đêm). Vì vậy, khi rời kho,
EVs có nguồn pin đầy đủ. Tuy nhiên, đôi khi những chuyến đi quá dài để EV không có đủ pin hoàn thành toàn bộ chuyến đi đó. trạm sạc công cộng cung cấp sự lựa chọn tốt hơn chạy EV để bổ sung năng lượng pin. Theo Hiệp hội kỹ sư ô tô (SAE), ba cấp độ sạc
tồn tại, như được liệt kê trong Bảng 1. 
![ 3 Cấp độ sạc xe điện]({{ site.baseurl }}/images/distra_bang_lv.png "3 Cấp độ sạc xe điện")

Cấp 1 phù hợp để qua đêm tại nhà và nơi làm việc. Cấp 2 thường được cài đặt
tại các cơ sở tư nhân và công cộng. Cấp 3, cũng được gọi là để sạc nhanh, sạc điện áp cao.     

Hiện nay, phần lớn các trạm sạc công cộng ở Bắc Kinh cung cấp sạc nhanh, có thể nhanh chóng hoàn thành quá trình sạc trong 1 h. Năng lượng pin được sạc lại thực sự không được xem xét; đó là, bất kể năng lượng pin Khi EV đến trạm sạc, sạc thời gian được coi là một giá trị không đổi (giả sử 30 phút). Khi nào sạc lại được thực hiện, pin được làm đầy với công suất. Ngoài ra, hàng đợi không được xem xét; đó là, EVs là chắc chắn sạc lại bất cứ khi nào có thể.
