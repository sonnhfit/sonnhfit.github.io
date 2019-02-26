---
layout: post
title: Bài toán điều phối xe điện với thời gian sạc và di chuyển khác nhau
mathjax: true
---

Chào các bạn mình là **Sơn** hôm trước mình được một bạn nữ nhờ nghiên cứu bài toán điều phối xe điện cho đồ án tốt nghiệp của bạn ấy. Do bạn ấy cười cũng xinh và tính dại gái của mình nổi lên và mình đã nhận lời nghiên cứu bài toán này. Đó là lý do bài viêt này ra đời.

Vấn đề định tuyến, điều phối xe điện với thời gian sạc và thời gian di chuyển thay đổi được phát triển để giải quyết một số vấn đề vận hành
xe điện chẳng hạn như giới hạn phạm vi và nhu cầu sạc của xe điện.

Cách giải quyết bài toán là sử dụng giải thuật di chuyền để tìm được các tuyến đường tối ưu, thời gian rời khỏi xe, kế hoạch tính phí.
Trong khi đó một giải thuật Dynamic  Dijkstra tìm đường ngắn nhất giữa hai Node liền kề dọc theo các tuyến đường. Để hạn chế  và ngăn chặn cạn kiệt toàn bộ pin cũng như đảm bảo hoạt động giao thông. Của các xe điện với việc không đủ năng lượng cần sạc lại ở các điểm sạc. Các biến động về thời gian sạc và di chuyển khác nhau thể hiện cho việc sự năng động của các phương tiện giao thông

## Phần 1 mở đầu

 Với khủng hoảng năng lượng và ô nhiễm môi trường, sử dụng năng lượng ví dụ như săng dầu hoặc những chất đốt tương tự đang gây ô nhiễm môi trường và được nhiều quốc gia quan tâm chú ý. 30% khí thải từ hoạt động giao thông gây hiệu ứng nhà kính ở USA. Vì thế việc xử lý hiệu quả, chuyên sâu, và giảm lượng cacbon của hoạt động giao thông là một chủ đề rất được quan tâm. Có hai cách tiếp cận bền vững cho vấn đề này.
Chúng ta sẽ bắt đầu xem sét. Vấn đề công nghệ tái tạo năng lượng và việc sử dụng hiệu quả các phương thức trong vận tải. Một hướng khác phát triển và tái cấu trúc công nghệ năng lượng ví dự như các loại xe AFVs, PHEVs, EVs (các loại xe điện, hoặc các loại xe kết hợp nhiều dạng nguyên liệu) 


## Phần 2 mô tả bài toán 

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

Môi trường giao thông năng động. Các điều kiện giao thông phức tạp có thể mất nhiều thời gian đi lại hơn do đó gây trở ngại cho khách hàng phục vụ kịp thời và khả năng tiếp cận phương tiện. Việc triển khai, chẳng hạn như biến động về thời gian di chuyển, là một phương pháp hiệu quả để phản ánh môi trường giao thông năng động trong mạng lưới đường bộ thực sự. Do đó, thời gian di chuyển thay đổi được giới thiệu để khôi phục môi trường lái xe thực sự của EVs. Tính toán hiệu quả và toàn diện về thời gian đi du lịch là rất đáng kể.

![ tốc độ di chuyển thay đổi]({{ site.baseurl }}/images/hinh2.png "3 tốc độ di chuyển thay đổi")

Tính toán thời gian di chuyển được đề xuất bởi Ichoua 2003 [25], trong đó việc điều chỉnh tốc độ di chuyển được xem xét và thuộc tính FIFO được chứng nhận được áp dụng trong bài viết này. Một ngày được chia thành nhiều khoảng thời gian. Tốc độ di chuyển không được giả định là không đổi và thay đổi khi một chiếc xe vượt qua ranh giới giữa hai khoảng thời gian liên tiếp. Thời gian tăng tốc hoặc thời gian giảm tốc được xác định bởi hai tốc độ di chuyển khác nhau trong đường biên là ngắn và nên
bị coi thường. Nói cách khác, tốc độ di chuyển thay đổi được coi là một chức năng bước (tham khảo Hình 2). Thời gian di chuyển là tổng thời gian di chuyển và tốc độ giao thông khác nhau.


ví dụ: có nhiều khoảng thời gian $$ T_i  $$  trong đó  $$ i = 1, 2, 3..n $$ 
Một chiếc xe rời khỏi nút bắt đầu của liên kết $$ a $$ tại thời điểm $$ T_k $$ và di chuyển với tốc độ $$ V_a^{T_k} $$ Cho đến khi xe đến tại nút nằm ở ranh giới $$ T_k $$ và $$ T_{k + 1}$$. Xe đi với tốc độ $$ V_a^{ T_{ k+1 } } $$ cho đến khi xe đến node nằm ở danh giới $$ T_{ k+1 } $$ và $$ T_{k+2} $$. Cuối cùng, chiếc xe đến nút cuối của liên kết $$ a $$ tại khoảng thời gian $$ T_m $$.
Hình 3 cho thấy khoảng cách di chuyển và thời gian di chuyển của
xe đi qua link a. Dựa trên quy trình, thời gian di chuyển từ nút $$ i $$ đến nút $$ j $$ là:

$$ t_ij = \sum_{ a\in{L_ij} } \sum_{i=k}^n \frac{l_a^{T_i}}{v_a^{T_i}} $$ (1)

$$ \sum_{i=k}^n l^{T_i}_a = l_a $$ (2)

Trong đó $$ l_a^{T_i} $$ là độ dài của quãng đường di chuyển của xe đi qua liên kết a trong khoảng thời gian $$ T_i $$ và $$ l_a $$ là độ dài của liên kết $$ a $$.

![ Thời gian di chuyể của xe đi qua liên kết a]({{ site.baseurl }}/images/p1_linka.png "Thời gian di chuyể của xe đi qua liên kết a")

###  Thuật toán Dijkstra động (Dynamic Dijkstra Algorithm)

Có những giao lộ lớn trong một mạng lưới đường thực sự. Một điều không thực tế là các phương tiện lái xe theo đường thẳng giữa hai nút. Do đó, làm thế nào để tìm ra các đường dẫn ngắn nhất giữa hai nút liền kề dọc theo các tuyến là một vấn đề trong mô hình EVRP-CTVTT.
Các tuyến đường, thời gian khởi hành xe tại kho, và gói sạc được lấy từ mô hình EVRP-CTVTT hiện diện trong phần 3. Vấn đề đường dẫn ngắn nhất (SP) trong phần này được đề cập để mô tả giải pháp sẽ sử dụng trong mô hình  EVRP-CTVTT.
Chúng ta cần có được đường đi ngắn nhất với chi phí tối thiểu trong một đồ thị đầy đủ. Phương pháp phổ biến nhất là thuật toán Dijkstra cổ điển đó là một phương pháp giả sử một nút đơn lẻ giống như nút nguồn, và tìm các đường dẫn ngắn nhất từ nguồn tới tất cả các nút khác trong biểu đồ và tạo ra một cây đường đi ngắn nhất. Trong thuật toán Dijkstra cổ điển trọng số liên kết giữa các đỉnh luôn được coi là khoảng cách (Hằng số)

Tuy nhiên, hệ thống giao thông trong thực tế lại có nhiều biến số thay đổi liên tục, các phương tiện mất nhiều thời gian hơn. Phần lớn lái xe quan tâm nhiều hơn đến thời gian thay vì khoảng cách. Do đó, thời gian di chuyển thay vì khoảng cách được coi là liên kết trọng số.

Thời gian di chuyển của mỗi liên kết không phải lúc nào cũng không đổi và thay đổi theo thời gian thực. Sau đó, trọng lượng liên kết được gây ra là động. Để giải quyết SP với thời gian di chuyển thay đổi, chúng tôi tham khảo cách xây dựng và lý thuyết của thuật toán Dijkstra cổ điển và thực hiện một số cải tiến so với thuật toán Dijkstra cổ điển để đề xuất thuật toán Dijkstra động, trong đó thời gian di chuyển giữa hai bất kỳ
các nút trong biểu đồ cần được tính toán lại để trọng lượng liên kết được cập nhật theo thời gian thực khi một nút chọn nút được kết nối tiếp theo.
Theo tính toán thời gian di chuyển trong Mục 2.2, phải biết khoảng thời gian của xe đến nút bắt đầu của liên kết hiện tại. Tuy nhiên,có thể có một số liên kết ngược dòng cho liên kết hiện tại. Khi liên kết hiện tại được chuyển từ các liên kết ngược dòng khác nhau, có thời gian đến khác nhau tại nút bắt đầu của liên kết hiện tại. Vì vậy, khoảng thời gian xe đến nút bắt đầu của liên kết hiện tại phải được ghi trực tuyến kết hợp với các khoảng thời gian của liên kết hiện tại để tính thời gian di chuyển của liên kết hiện tại.
Dựa trên những ý tưởng của thuật toán Dijkstra động được mô tả ở dưới. Graph là mạng lưới đường bộ, source là điểm gốc xuất phát, target là đích đến. Thời gian di chuyển của con đường ngắn nhất từ nguồn đến đích: $$ cost(u, V) $$ đại diện cho trọng số của liên kết giữa (u, V). Xe đến node thứ $$ i $$ tại thời điểm $$ time[i] $$,S Là dãy đường đi ngắn nhất từ 𝑠𝑜𝑢𝑟𝑐𝑒 đến 𝑡𝑎𝑟𝑔𝑒𝑡;

Mã giả của thuật toán Dijkstra động ( tìm đường ngắn nhất động) như sau:
```
Duyệt từng Node v trong Graph
{
    dist[v] = vô cực
    prev[v] = Undefined
    Thêm v vào hàng đợi Q
}

dist[source] = 0
u0 = source

Trong khi Q chưa rỗng
{
    u = node in Q với điều kiện min dist[u]
    xóa u khỏi Q
    Nếu prev[u] is defined
    {
        u0 = prev[u]
        cost(u0, u) = kết quả của biểu thức (1) với T0
        time[u] = time[u0] + cost(u0, u)

    }
    Duyệt từng hàng xóm v của u
    {
        cost(u, v) = kết quả của biểu thức (1) với time[u]
        alt = dist[u] + cost(u, v)
        Nếu (alt < dist[v]>)
        {
            dist[v] = alt
            prev[v] = u
            time[v] = time[v] + cost(u, v)
        }
    }
}
return dist[], prev[]
S = ""
u = đích
while prev[u] is defined:
{
    Chèn u vào đầu của S
    u = prev[u]
}

Chèn u vào đầu của S

```


## Phần 3 xây dựng mô hình

Dựa trên mô tả vấn đề ở phần 2 mô hình EVRP-CTVTT được xây dựng như chương trình tuyến tính bên dưới. Và các biến liên quan trong mô hình được định nghĩa như sau:

$$ C_0 $$: Tổng chi phí

$$ Cf_k $$: Chi phí cố định của xe k

$$ Ct_k $$: Chi phí thời gian đi lại của xe k

$$ Cr_k $$: Chi phí sạc xe k

$$ Cp_k $$: Chi phí thưởng phạt của xe k

$$ C_f $$: Chi phí xe cố định trên mỗi đơn vị

$$ c_t $$: Chi phí thời gian cho mỗi đơn vị

$$ c_c $$: chi phí sạc trên mỗi đơn vị

$$ c_e $$: chi phí phạt đến sớm mỗi đơn vị

$$ c_d $$: chi phí phạt chậm trễ mỗi đơn vị

$$ F $$: một bộ trạm sạc

$$ O $$: bắt đầu kho

$$ O' $$: kết thúc kho

$$ V: O \cup C \cup F \cup O' $$.

$$ K $$: một bộ các phương tiện có sẵn

$$ D_{ik} $$: phạm vi còn lại của xe k tại nút 𝑖 (km)

$$ d_{ij} $$: Khoảng cách di chuyển của con đường ngắn nhất từ node i tới node j (km)

$$ D_{max} $$: Phạm vi lái xe tối đa (km)

$$ W_{Ok} $$: tải trọng của xe k khởi hành từ đầu kho (kg)


$$ w_i $$: trọng lượng hàng hóa của nút 𝑖 (kg)

$$ W_{max} $$: tải trọng xe (kg)

$$ t_{ijk} $$: Thời gian di chuyển của phương tiện k đi từ nút i đến nút j (phút)

$$ T_{ik} $$: Thời gian khởi hành của xe k tại nút i

$$ T_o^{early} $$: thời gian hoạt động xe sớm nhất

$$ T_{o'}^{delay} $$: thời gian vận hành xe mới nhất

$$ T_i^{early} $$ thời gian đến sớm nhất tại nút i

$$ T_i^{delay} $$ thời gian đến muộn nhất tại nút i

$$ t_c $$: thời gian sạc (phút)

$$ z_j $$: có trạm sạc tại nút $$ 𝑗, {1, 𝑗 \in 𝐹;0, khác} $$

$$ T_{Ok} $$: Giờ khởi hành của xe k tại kho

$$ x_{ijk} $$: {1, xe k thăm từ node i đến node j; 0, Trường hợp khác} 

$$ y_{jk} $$: {1, xe k được sạc lại tại nút j; 0, Trường hợp khác}


Trong đó hàm mục tiêu của model như sau:
Minimize $$ C_0 =  \sum_{k \in K } Cf_k + Ct_k + Cr_k + Cp_k $$ (3)

$$ Cf_k = c_f(1 - \sum_{i \in O} \sum_{j \in {O'}} x_{ijk})$$ (4)


$$ Ct_k = c_t (\sum_{i \in {O'}}T_{ik} - \sum_{i \in {O}}T_{ik} - t_c \sum_{i \in F}y_{ik}) $$ (5)

$$ Cr_k = c_c \sum_{i \in F}y_{ik} $$ (6)


$$ Cp_k = \sum_{i \in C}[c_e max {0, T_i^{early}} + c_d max {0, T_[ik] - T_i^{delay}}] $$ (7)

subject to $$ \sum_{i \in C \cup F \cup O} x_{ijk} = 1 \forall j \in C, \forall k \in K $$ (8)

$$ \sum_{j \in C\cup F\cup{O'}} x_{ijk} = 1 \forall i \in C, \forall k \in K $$ (9)

$$ \sum_{ \forall i \in C \cup F\cup O} x_{ijk} = \sum_{\forall m \in C \cup F \cup {O'}} x_{jmk} \forall j \in C \cup F, \forall k \in K $$ (10)

$$ \sum_{ \forall j \in C \cup F \cup {O'}} x_{Ojk} = 1 \forall k \in K $$ (11)


$$ \sum_{ \forall j \in C \cup F \cup {O}} x_{jO'k} = 1 \forall k \in K $$ (12)

$$ D_{jk} = [D_{jk}(1-y_{jk}) + y_{ik}D_{max} - d_{ij}]x_{ijk} \forall i \in C \cup F \cup O , \forall j \in C \cup F \cup O' , \forall k \in K  $$ (13)

$$ D_{ik} >= 0 \forall j \in C \cup F \cup O' , \forall k \in K $$ (14)

$$ D_{Ok} = D_{max} \forall k \in K  $$ (15)


$$ W_{Ok} <= W_{max} \forall j \in V \forall k \in K $$ (16)

$$ W_{Ok} <= W_{max} \forall j \in V, \forall k \in K $$ (17)

$$ T_{jk} = (T_{ik} + t_{ijk} + y_{ik}t_c)x_{ijk} \forall i \in C \cup F \cup O, \forall j \in C \cup F \cup O' , \forall k \in K $$ (18)

$$ T_O^{early} <= T_{Ok}  \forall k \in K $$ (19)

$$ T_{O'}^{delay} >= T_{O'k} \forall k \in K $$ (20)

$$ y_{jk} <= z_j \forall j \in V , \forall k \in K $$ (21)

$$ y_{jk} = {0, 1} \forall j \in V , \forall k \in K $$ (22)

$$ x_{ijk} = {0, 1} \forall j \in C \cup F \cup O' , \forall i \in C \cup F \cup O, \forall k \in K $$ (23)


Phương trình (3) giảm thiểu tổng chi phí, bao gồm chi phí cố định phương tiện, chi phí đi lại, chi phí phạt và chi phí sạc. Trong (4), các phương tiện được sử dụng chi phí cố định phương tiện. Chi phí đi lại trong (5) tỷ lệ thuận với thời gian di chuyển. Phương trình (6) mô tả chi phí để sử dụng các trạm sạc. Bởi vì khách hàng có thể được phục vụ sớm hoặc muộn, nên chi phí phạt được tính theo (7).

Phương trình (8) và (9) đảm bảo rằng mỗi khách hàng chỉ được truy cập bằng một phương tiện. Phương trình (10) trình bày dòng chảy bảo tồn, trong đó số lượng khách đến phải bằng số lần khởi hành tại bất kỳ khách hàng hoặc trạm thu phí nào. Phương trình (11) và (12) yêu cầu tất cả các phương tiện rời khỏi kho bắt đầu và trở về kho cuối. Bởi vì chỉ có một kho tồn tại, kho bắt đầu và kho cuối được đặt tại cùng một nút (𝑂 = 𝑂'). Không có phương tiện đang chạy vượt qua bất kỳ nút, ngoại trừ kho bắt đầu và kho cuối.

Phương trình (13) là biểu thức của phạm vi dư. Các ổ đĩa dựa trên con đường ngắn nhất được giải quyết trong Phần 2.3. Giới hạn phạm vi mà phạm vi còn lại của bất kỳ phương tiện nào tại bất kỳ nút nào phải lớn hơn 0 được đề xuất trong (14). Công thức (15) nói rằng mỗi chiếc xe có phí 100% khi rời kho bắt đầu.

Công thức (16) nói rằng các phương tiện giao tải nhiều tải đến khách hàng. Phương trình (17) đảm bảo rằng trọng lượng tải của mỗi chiếc xe không vượt quá khả năng tải của xe. Trong (18), thời gian khởi hành xe tại nút hiện tại bằng với tổng thời gian khởi hành xe tại nút cuối cùng, hành trình thời gian giữa nút cuối cùng và nút hiện tại và thời gian sạc. Thời gian di chuyển có được bằng thời gian di chuyển tính toán ((1) - (2)). Phương trình (19) - (20) đảm bảo rằng tất cả xe thực hiện giao hàng trong thời gian vận hành xe giai đoạn.

Phương trình (21) yêu cầu tất cả các phương tiện chỉ đến thăm trạm sạc để được sạc lại. Phương trình (22) và (23) đảm bảo rằng $$ y_{jk} $$ và x_{ijk} là các biến quyết định 0-1.

Phần 4 Mô hình giải pháp công nghệ

Các VRP và các biến thể là một vấn đề khó NP. các thuật toán có thể đạt được hiệu suất tốt hơn trong tính toán thời gian và chất lượng giải pháp cho VRP và các biến thể. Như một trong số các thuật toán heuristic, thuật toán di truyền (GA) là dễ dàng để lập trình và có thời gian tính toán nhanh hơn. Hơn nữa, GA đã được áp dụng rộng rãi trong các VRP hoặc biến thể phức tạp thực hiện đặc biệt là trong các mạng lưới đường lớn và thực tế và có thể có được giải pháp tốt hơn chấp nhận được. Do đó, xem xét sự phức tạp của mô hình đề xuất và con đường mạng, GA được coi là công nghệ giải pháp mô hình trong bài báo.

Trong GA, một số lượng cá thể có gen được xử lý bởi các toán tử chọn và nhân để sản xuất cá nhân mới. Các cá nhân có thể lực tốt hơn sẽ có được nhiều cơ hội hơn để tồn tại. Để đạt được sự đa dạng Trong số các cá nhân, chéo và đột biến được áp dụng trong thủ tục GA. Quy trình của GA được hiển thị là sau.

Bước 1. Áp dụng chế độ được mã hóa để tạo ra quần thể ban đầu
𝑃 (𝑔𝑒𝑛) (| 𝑃 (𝑔𝑒𝑛) | = 𝑁); thì = 0.

![ Giá trị tham số]({{ site.baseurl }}/images/bang2_bai2.png "Giá trị tham số")

Bước 2. Tính toán thể lực cho từng cá nhân trong P(𝑔𝑒𝑛)

Bước 3. Chọn $$ Ne  $$ cá nhân từ $$ 𝑃(gen) $$ ở thể lực cao giá trị như những cá nhân ưu tú. Những cá nhân ưu tú thì không xử lý; sang Bước 7. Các cá nhân còn lại sáng tác một dân số bình thường $$ P1(gen) (| P1 (gen) | = 𝑁 - Ne). $$

Bước 4. Cứ hai cá thể trong P1(gen) tạo thành một cặp áp dụng trong một chéo. Mỗi cá nhân được yêu cầu phải thỏa mãn tất cả các ràng buộc. Nếu không, cặp đôi là vô ích; chạy chéo lần nữa. 𝑃1 (gen) được cập nhật.

Bước 5. Mỗi cá nhân trong P1(gen) được áp dụng trong một đột biến. Mỗi cá nhân được yêu cầu phải đáp ứng tất cả các ràng buộc. Nếu không, cá nhân là vô ích; chạy lại đột biến. 𝑃1 (gen) là cập nhật.

Bước 6. 1 P1(pen) và các cá nhân ưu tú được kết hợp để tạo thành một quần thể mới P(gen), trong đó gen = gen + 1.

Bước 7. Nếu gen < T, quay lại Bước 3. Nếu không, hãy ngừng chạy
và đầu ra cá nhân có giá trị thể dục cao nhất trong
𝑃 (gen).

Bước 8. Giải mã cá nhân để đạt được giải pháp tối ưu

Các tham số GA (số lượng cá nhân, số lượng thế hệ, số lượng cá nhân ưu tú, tỷ lệ chéo, và tỷ lệ đột biến) có thể có tác động đến các giá trị giải pháp. Ba tham số (số lượng cá thể, số lượng thế hệ và số lượng cá nhân ưu tú) được xác định bằng nhiều thí nghiệm với các thông số khác nhau. Và hai các tham số (tỷ lệ chéo và tỷ lệ đột biến) được chọn trong phạm vi giá trị hợp lý của họ. Tất cả các tham số trong GA là được liệt kê trong Bảng 2.

Hai biến quyết định $$ y_{ik} $$ (tuyến đường) và $$ 𝑥_{ijk} $$ (tính phí kế hoạch) có thể được lấy từ cá nhân. Mã hóa chế độ trong đó các biến quyết định được thể hiện bởi cá nhân là tiền đề của GA. Chúng tôi áp dụng chế độ trong đó cá nhân bao gồm tất cả các nút truy cập. Ví dụ, có là một kho, nn khách hàng,mm trạm sạc và phương tiện. Quy trình của chế độ được mã hóa như sau:

(1) Số sê-ri của nn khách hàng và mm các trạm tính phí được sắp xếp liên tiếp là 1 ,. . . , nn, nn + 1 ,. . . , mm.