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

Một kế hoạch vận hành xe tối ưu bao gồm tuyến đường, thời gian khởi hành xe tại kho, tính phí kế hoạch, và những con đường ngắn nhất có được để đáp ứng khách hàng nhu cầu, đảm bảo an toàn hoạt động và giảm chi phí. Các tuyến đường và thời gian khởi hành xe tại kho. Cần trả lời Hai câu hỏi sau: khách hàng được truy cập như thế nào và khi nào các phương tiện được sử dụng khởi hành từ kho, tương ứng. Các kế hoạch tính phí là để giải quyết vấn đề như thế nào và khi nào các phương tiện được sử dụng với nhu cầu sạc được sạc lại. Các con đường ngắn nhất là hướng dẫn các phương tiện cách lái xe lớn mạng lưới đường bộ.

Để ngụ ý sơ đồ vận hành xe tối ưu, chúng tôi hiển thị một ví dụ kết quả đơn giản với 10 khách hàng và 8 lần sạc các trạm (tham khảo Hình 1). Kết quả chi tiết là sau: depot-1-9-C2-6-depot (tuyến 1), depot-5-4-7-8-C5-kho (tuyến 2) và kho-2-3-10-kho (tuyến 3)

![Mô tả bài toán tối ưu điều phối xe điện với thời gian khác nhau]({{ site.baseurl }}/images/hinh1_toi-uu.PNG "Mô tả bài toán tối ưu điều phối xe điện với thời gian khác nhau")

Xe trên tuyến 1 rời kho lúc 13:40 để thăm ba khách hàng (1, 9, 6) và cần được sạc lại tại nút C2 trong quá trình vận chuyển. Tương tự, chiếc xe trên tuyến đường 2 rời khỏi kho lúc 15:10 và được sạc lại tại nút C5. Trên tuyến đường 3, chiếc xe có đủ năng lượng pin cho toàn bộ chuyến đi để không có nhu cầu di chuyển đến bất kỳ trạm sạc nào. Bởi vì toàn bộ mạng lưới đường bao gồm thông tin giao lộ lớn không được đưa ra trong Hình 1, các đường dẫn ngắn nhất không được xây dựng. Một trường hợp nghiên cứu thực tế và kết quả hoàn chỉnh tương ứng được trình bày trong Phần 5

Ngoài ra, một thuật toán Dijkstra động được giới thiệu trong Mục 2.3 được đề xuất để giải quyết vấn đề con đường ngắn nhất

2.1. **Charging Demand (Nhu cầu sạc pin)** . Nói chung, Công ty hỗ trợ các xe EV (Xe điện) có  điểm sạc tại kho. Xe EV có thể được sạc trong thời gian nhàn rỗi không phải di chuyển(ví dụ: thời gian ban đêm). Vì vậy xe luôn đầy pin khi rời khỏi kho. Tuy nhiên, đôi khi những chuyến đi quá dài để EV không có đủ pin hoàn thành toàn bộ chuyến đi đó. trạm sạc công cộng cung cấp sự lựa chọn tốt hơn xe EV sẽ đến đó để bổ sung năng lượng pin. Theo Hiệp hội kỹ sư ô tô (SAE), ba cấp độ sạc
tồn tại, như được liệt kê trong Bảng 1. 
![ 3 Cấp độ sạc xe điện]({{ site.baseurl }}/images/distra_bang_lv.png "3 Cấp độ sạc xe điện")

Cấp 1 phù hợp để qua đêm tại nhà và nơi làm việc. Cấp 2 thường được cài đặt
tại các cơ sở tư nhân và công cộng. Cấp 3, cũng được gọi là để sạc nhanh, sạc điện áp cao.     

Hiện nay, phần lớn các trạm sạc công cộng ở Bắc Kinh cung cấp sạc nhanh, có thể nhanh chóng hoàn thành quá trình sạc trong 1 giờ. Năng lượng pin được sạc lại thực sự không được xem xét; đó là, bất kể năng lượng pin Khi xe EV đến trạm sạc, sạc thời gian được coi là một giá trị không đổi (giả sử 30 phút). Khi nào sạc lại được thực hiện, pin được làm đầy với công suất. Ngoài ra, hàng đợi không được xem xét; đó là, EVs là chắc chắn sạc lại bất cứ khi nào có thể.

Môi trường giao thông biến đổi liên tục. Các điều kiện giao thông phức tạp có thể mất nhiều thời gian đi lại hơn do đó gây trở ngại cho việc phục vụ khách hàng. Việc triển khai, chẳng hạn như biến động về thời gian di chuyển, là một phương pháp hiệu quả để phản ánh môi trường giao thông năng động trong mạng lưới đường bộ thực sự. Do đó, thời gian di chuyển thay đổi được giới thiệu để khôi phục môi trường lái xe thực sự của EVs. Tính toán hiệu quả và toàn diện về thời gian đi là rất đáng kể.

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

## Phần 4 Mô hình giải pháp công nghệ

Các VRP và các biến thể là một vấn đề khó NP. các thuật toán có thể đạt được hiệu suất tốt hơn trong tính toán thời gian và chất lượng giải pháp cho VRP và các biến thể. Như một trong số các thuật toán heuristic, thuật toán di truyền (GA) là dễ dàng để lập trình và có thời gian tính toán nhanh hơn. Hơn nữa, GA đã được áp dụng rộng rãi trong các VRP hoặc biến thể phức tạp thực hiện đặc biệt là trong các mạng lưới đường lớn và thực tế và có thể có được giải pháp tốt hơn chấp nhận được. Do đó, xem xét sự phức tạp của mô hình đề xuất và con đường mạng, GA được coi là công nghệ giải pháp mô hình trong bài báo.

Trong GA, một số lượng cá thể có gen được xử lý bởi các toán tử chọn và nhân để sản xuất cá nhân mới. Các cá nhân có thể lực tốt hơn sẽ có được nhiều cơ hội hơn để tồn tại. Để đạt được sự đa dạng Trong số các cá nhân, chéo và đột biến được áp dụng trong thủ tục GA. Quy trình của GA được hiển thị là sau.

Bước 1. Áp dụng chế độ được mã hóa để tạo ra quần thể ban đầu
𝑃 (𝑔𝑒𝑛) (| 𝑃 (𝑔𝑒𝑛) | = 𝑁); thì = 0.

![ Giá trị tham số]({{ site.baseurl }}/images/bang2_bai2.png "Giá trị tham số")

Bước 2. Tính toán thể lực cho từng cá nhân trong P(𝑔𝑒𝑛)

Bước 3. Chọn $$ Ne  $$ cá nhân từ $$ 𝑃(gen) $$ ở thể lực cao giá trị như những cá nhân $$ P1 = N $$ ưu tú. Những cá nhân ưu tú thì không xử lý; sang Bước 7. Các cá nhân còn lại sáng tác một dân số bình thường $$ P1(gen) (| P1 (gen) | = 𝑁 - Ne). $$

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

(2) Sau khi bị rối loạn, chuỗi số được xác định như A.

![ Bảng 4]({{ site.baseurl }}/images/bang4_bai2.png "Giá trị tham số")

(3) Xác định tuần tự các số sê-ri là mm + 1,mm + 2 ,. . . , mm + 𝑘𝑘 tại các kho bắt đầu và kho cuối.

(4) Vị trí đầu tiên và vị trí cuối cùng của được chèn
lần lượt bằng các số $$ mm + 1 $$ và $$ mm  + 2 $$.

(5) Cuối cùng, các số $$ mm + 3, mm + 4 ,. . . , mm + 2𝑘𝑘  $$ là ngẫu nhiên chèn vào bất kỳ vị trí nào khác của.

Việc chèn $$ A $$  tạo thành một cá thể. Cá thể là chia thành nhiều phân đoạn theo các số từ $$ mm + 1 $$ 
đến $$ mm + 2kk $$. Mỗi phân đoạn có thể được chuyển đổi thành một tuyến đường. Tuy nhiên, một số tuyến đường được coi là không hiệu quả vì chúng không ghé thăm bất kỳ khách hàng nào.

Một ví dụ đơn giản được hiển thị trong Hình 4 để giải thích chế độ được mã hóa. Ba phương tiện, một trạm sạc, và chín khách hàng có sẵn. Dựa trên quy trình của chế độ được mã hóa, một cá nhân được hình thành. Một số phát hiện có thể đạt được bằng cách giải mã từng cá nhân: tuyến 1 thăm khách hàng 5, 2 và 1; tuyến đường 2 không hiệu quả; tuyến 3 thăm khách hàng 4, 9, 6, 3, 7 và 8; và tuyến đường 3 được sạc lại trước khi trở về kho.

Ngoài hai biến quyết định ($$ y_{jk} $$ và $$ x_{ijk} $$ ),biến quyết định còn lại $$ T_{Ok} $$  chỉ ra rằng chiếc xe thời gian khởi hành tại kho được giải quyết một mình. Giấy áp dụng phương pháp toàn diện. Tập hợp thời gian khởi hành có sẵn bao gồm thời gian trong khoảng thời gian mười phút giữa thời gian hoạt động sớm nhất và thời gian hoạt động mới nhất (ví dụ: 06:00, 06:10, ..., 20:50, 21:00).

Mỗi tuyến hiệu quả có trật tự khớp với một thời gian khởi hành có sẵn để tính giá trị đối tượng. Đối với giá trị đối tượng tối thiểu, thời gian khởi hành có sẵn được coi là thời gian khởi hành xe tại kho.

## Phần 5 Nghiên cứu trường hợp thực tế lớn

Một nghiên cứu trường hợp lớn và thực tế được thực hiện để phản ánh hiệu suất của mô hình đề xuất và công nghệ giải pháp. Tất cả các thử nghiệm đã được chạy trên máy tính để bàn với CPU Intel Core i5-5200U, RAM 16 GB và hệ điều hành 64 bit. Một số loại dữ liệu thử nghiệm được xác định như sau.

### 5.1. Số liệu thực nghiệm
5.1.1. Mạng lưới đường bộ. Các mô hình được áp dụng cho một rời rạc đại diện của một mạng lưới đường lớn và thực tế trong Khu đô thị Bắc Kinh (trong vòng thứ năm). Toàn bộ con đường Mạng lưới khu đô thị Bắc Kinh quá phức tạp. giản thể. Xem xét nguồn dữ liệu tốc độ du lịch, mô hình độ phức tạp và hiệu quả của giải pháp, bài báo chủ yếu chọn tất cả các đường cao tốc và phần lớn các tuyến đường huyết mạch để xây dựng một mạng lưới đường lớn và thực tế. Sau khi tạo mạng lưới đường bao gồm 222 nút và 943 liên kết. Các nút và liên kết đại diện cho giao lộ đường và đường phân khúc, tương ứng.

5.1.2. Cơ sở dữ liệu. Ba loại cơ sở tồn tại: kho, khách hàng, và trạm sạc. Chỉ có một kho được đặt tại trung tâm của mạng lưới đường bộ. Địa điểm của 50 khách hàng sẽ được phục vụ vào ngày hôm sau và 20 trạm sạc được phân phối ngẫu nhiên tại các nút của mạng lưới đường bộ. Trọng lượng hàng hóa được phân bổ ngẫu nhiên cho mỗi khách hàng từ tám hạng cân (10 kg, 20 kg, 30 kg, 40 kg, 50 kg, 60 kg, 70 kg và 80 kg). Tương tự, cửa sổ thời gian của mỗi khách hàng cũng được sản xuất ngẫu nhiên mỗi giờ trong khoảng từ 8:00 và 19:00. Hình 5 trình bày mạng lưới đường toàn diện tải dữ liệu cơ sở.

5.1.3. Dữ liệu tốc độ du lịch. Để tính thời gian di chuyển trong Mô hình EVRP-CTVTT, tốc độ di chuyển phải được xác định. Cảm biến vi sóng được cài đặt trên một phần của đường cao tốc thu thập dữ liệu tốc độ giao thông cứ sau 2 phút vào một ngày. Bởi vì dữ liệu tốc độ di chuyển là từ thực tế và khoảng thời gian thu thập rất ngắn (2 phút), lưu lượng truy cập thực môi trường có thể được phục hồi hiệu quả. Hình 6 cho thấy dữ liệu tốc độ di chuyển trong khoảng thời gian vận hành xe.

5.1.4. Xác định giá trị biến thiên không đổi. Hiện tại, EVs cho hậu cần tại Bắc Kinh chủ yếu là xe điện do Công ty ô tô Bắc Kinh sản xuất. Theo thông số kỹ thuật công nghệ hậu cần EV, khả năng tải xe và phạm vi lái tối đa lần lượt là 1000 kg và 120 km. Chi phí cố định cho mỗi đơn vị xe 𝑐𝑓 xem xét tiền lương lái xe, bảo trì, chi phí nhàn rỗi và chi phí bảo hiểm xe. Chi phí đi lại trên mỗi đơn vị dựa trên thời gian sử dụng và hiệu quả hoạt động. Theo lời khuyên từ công ty hậu cần, chúng tôi đặt hai thông số tương ứng là 100 nhân dân tệ và 1 nhân dân tệ / phút. Chi phí $$ c_c $$ tính phí trên mỗi đơn vị được xác định bởi giá điện và phí dịch vụ tính phí. Tại Bắc Kinh, giá điện công nghiệp trung bình là 0,8 nhân dân tệ / kWh [32]. Hiện tại, không có cách tiếp cận tiêu chuẩn thống nhất có sẵn cho phí dịch vụ tính phí. Để tính toán thuận tiện, chi phí tính phí trên mỗi đơn vị được định giá là 30 nhân dân tệ: 21,6 nhân dân tệ (chi phí có tính phí 100%) cộng với phí dịch vụ tính phí 8.4 nhân dân tệ). . Thời gian sạc $$ t_c $$ được đặt thành 30 phút theo Mục 2.1. Các biến không đổi được tóm tắt trong Bảng 3.

5.2. Kết quả và phân tích. Dựa trên dữ liệu thử nghiệm đã nói ở trên, mô hình EVRP-CTVTT được giải quyết bằng GA

![ Bảng 5]({{ site.baseurl }}/images/bang5_bai2.png "Giá trị tham số")

![ Bảng 5]({{ site.baseurl }}/images/bang6_bai2.png "Giá trị tham số")

![ Bảng 5]({{ site.baseurl }}/images/table3_bai2.png "Giá trị tham số")


![ Bảng 5]({{ site.baseurl }}/images/table4_bai2.png "Giá trị tham số")

MATLAB R2012a được áp dụng trong triển khai GA. Do
với tính ngẫu nhiên của thuật toán, GA được chạy liên tục mười lần
Thời gian tính toán mà thuật toán thực hiện mỗi thí nghiệm không khác nhau lắm. Thời gian tính toán trung bình là khoảng 3 h. Hãy xem xét rằng mô hình và mạng lưới đường thực tế là quá phức tạp. Ngoài ra, kết quả thu được một ngày trước khi kết quả được thực hiện thực tế. Do đó, thời gian tính toán mà thuật toán thực hiện là chấp nhận được. Đối tượng mô hình (giá trị đối tượng tối ưu) được coi là chỉ số thử nghiệm được so sánh. Thí nghiệm có giá trị đối tượng tối ưu nhất sẽ được phân tích chi tiết. Kết quả được so sánh trong Bảng 4 chỉ ra rằng Thí nghiệm 1 có hiệu suất giải pháp tốt nhất. Quá trình lặp lại thuật toán của Thí nghiệm 1 (Hình 7) cho thấy GA có thể nhanh chóng đảm bảo sự hội tụ và cải thiện nỗ lực tính toán. Ngoài ra, kết quả, bao gồm các tuyến đường, thời gian khởi hành xe tại kho và kế hoạch sạc, được trình bày như sau. Thông tin về phương tiện đang chạy bao gồm thời gian khởi hành xe, quãng đường di chuyển và thứ tự của các nút được truy cập được thể hiện trong Bảng 5. Bảng 6 tóm tắt tất cả các chi phí.

![ Bảng 5]({{ site.baseurl }}/images/bang7_bai2.png "Giá trị tham số")

![ Bảng 5]({{ site.baseurl }}/images/bang8_bai2.png "Giá trị tham số")

Theo yêu cầu, bảy chiếc xe được phái đi. Khoảng cách di chuyển của tuyến đường 1 vượt quá phạm vi lái xe tối đa (120 km). Do phạm vi hạn chế, phương tiện trên tuyến 1 bắt buộc phải được sạc lại tại trạm sạc 2 trong quá cảnh. Hơn nữa, thời gian sạc sẽ trì hoãn thời gian phục vụ khách hàng và tạo ra chi phí phạt lớn hơn cho tuyến 1.
Là yếu tố quan trọng nhất ảnh hưởng đến các tuyến đường và kế hoạch tính phí, phạm vi còn lại của mỗi chiếc xe đến bất kỳ nút nào được truy cập cần phải được phân tích chi tiết (tham khảo Hình 8). Nó chỉ ra rằng giải pháp tối ưu thu được thỏa mãn giới hạn phạm vi rằng phạm vi còn lại của xe tại bất kỳ nút nào được truy cập phải vượt quá 0.
Đối với tuyến đường 1, do xe được sạc đầy tại trạm sạc 2, phạm vi còn lại cho khách hàng 22 là nút được truy cập đầu tiên sau khi xe được sạc lại tăng rõ rệt.

Bên cạnh các tuyến đường, thời gian khởi hành xe tại kho, và kế hoạch tính phí, phải có kết quả về vấn đề đường đi ngắn nhất. Chúng tôi cũng mô tả các con đường ngắn nhất dọc theo các tuyến đường trong mạng lưới đường bộ. Theo Hình 9, đường chạy của từng tuyến có thể được hiển thị rõ ràng. Các phương tiện tương ứng ghé thăm khách hàng hoặc trạm sạc một cách có trật tự.

## Kết luận

Hiện nay, EV ngày càng tăng được sử dụng trong các khác nhau lĩnh vực giao thông như hậu cần. Để giải quyết tốt hơn vấn đề làm thế nào kế hoạch vận hành xe được lên kế hoạch Khi EV được coi là chế độ vận chuyển để thăm khách hàng trong mạng lưới đường bộ thực sự, bài viết này toàn diện xem xét các tính năng phân phối (cửa sổ thời gian và trọng lượng ràng buộc), các đặc tính EV (phạm vi giới hạn và nhu cầu sạc) và môi trường giao thông động để phát triển mô hình EVRP-CTVTT với tổng chi phí tối thiểu.

![ Bảng 5]({{ site.baseurl }}/images/table5_bai2.png "Giá trị tham số")

![ Bảng 5]({{ site.baseurl }}/images/table6_bai2.png "Giá trị tham số")

Một kế hoạch vận hành phương tiện tối ưu, bao gồm đồng thời các tuyến đường, thời gian khởi hành phương tiện tại kho, kế hoạch sạc và các con đường ngắn nhất, đã đạt được.

Do phạm vi hạn chế, EV đôi khi được sạc lại tại các trạm sạc nhiều lần trong khi quá cảnh để đảm bảo chuyến đi được hoàn thành. Phương pháp tốt nhất để gán tối ưu các trạm sạc cho EV với nhu cầu sạc cũng được thảo luận trong bài báo.

Trong thực tế, giao thông liên tục thay đổi. Khác với phần lớn các giấy tờ liên quan, bài viết này tập trung trên môi trường giao thông năng động. Để thực hiện tính năng động của giao thông, sự biến động của thời gian di chuyển là được giới thiệu trong mô hình đang phát triển. Du lịch thay đổi tốc độ cứ sau 2 phút được áp dụng để tính toán thời gian đi lại Dựa trên tốc độ di chuyển thay đổi, một thuật toán Dijkstra năng động thực hiện một số cải tiến trên thuật toán Dijkstra cổ điển được đề xuất để giải quyết con đường ngắn nhất giữa bất kỳ hai nút liền kề dọc theo tuyến đường.

Một nghiên cứu trường hợp lớn và thực tế với mạng lưới đường bộ tại khu vực đô thị Bắc Kinh, với 50 khách hàng và 20 trạm sạc, được trình bày. GA được áp dụng để giải quyết Mô hình EVRP-CTVTT và thu được một số kết quả, bao gồm các tuyến đường, thời gian khởi hành xe tại kho, và phương án thu phí.

Kết quả chỉ ra rằng GA mang lại hiệu suất chấp nhận được về thời gian tính toán, độ hội tụ và chất lượng giải pháp.
Từ kết quả, chúng tôi kết luận rằng EVRP-CTVTT mô hình và thuật toán Dijkstra hoàn toàn thỏa mãn nhu cầu của khách hàng trong khi giảm chi phí, ngăn chặn sự cạn kiệt của tất cả năng lượng pin trong khi vận chuyển và đảm bảo Hoạt động an toàn. Ngoài ra, kết quả cung cấp một sơ đồ phương tiện tối ưu cho công ty hậu cần với EV hoạt động.

Mặc dù bài báo trước tiên xem xét thời gian tính phí và thời gian di chuyển thay đổi để giải quyết EVRP, một số khía cạnh vẫn chưa được giải quyết

(i) Ngay cả khi chúng tôi áp dụng dữ liệu tốc độ giao thông thực tế, đôi khi có sự ngẫu nhiên trong tốc độ di chuyển do một số tai nạn giao thông. Do đó, các biểu thức phức tạp hơn của tốc độ di chuyển sẽ được tập trung vào.

(ii) Các vị trí trạm sạc, có thể ảnh hưởng đến gói sạc, được cố định. Vấn đề tuyến đường liên kết nghiên cứu liên quan và vấn đề vị trí sẽ được điều tra trong tương lai.

(iii) Giải pháp tối ưu bị ảnh hưởng rất nhiều bởi các tham số chi phí trên mỗi đơn vị. Bài viết này trực tiếp cung cấp các giá trị dựa trên kinh nghiệm hoạt động. Công việc trong tương lai của chúng tôi sẽ bao gồm phân tích độ nhạy cho các thông số này.

![ Bảng 5]({{ site.baseurl }}/images/bang9_bai2.png "Giá trị tham số")
![ Bảng 5]({{ site.baseurl }}/images/bang10_bai2.png "Giá trị tham số")
![ Bảng 5]({{ site.baseurl }}/images/bang11_bai2.png "Giá trị tham số")
![ Bảng 5]({{ site.baseurl }}/images/bang12_bai2.png "Giá trị tham số")