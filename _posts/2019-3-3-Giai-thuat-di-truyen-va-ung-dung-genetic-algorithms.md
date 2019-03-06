---
layout: post
title: Giải thuật di truyền và ứng dụng với python
mathjax: true
---

Chào các bạn mình là **Sơn Nguyễn** ở trong bài viết này mình sẽ hướng dẫn các bạn hiểu cũng như xây dựng một chương trình đơn giản với giải thuật di truyền. Để các bạn có thể ứng dụng giải thuật di truyền vào những bài toán cụ thể của các bạn. Trong các lĩnh vực khác của khoa học máy tính.
<br/>






## Mục lục

- Giới thiệu ngắn gọn về thuật toán di truyền
- Mục tiêu các vấn đề cần giải quyết
- Dự án đầu tiên
- Lập trình di truyền với python
- Hello world
- Đoán số của tôi
- Đoán mật khẩu


## Giới thiệu ngắn gọn về thuật toán di truyền
Thuật toán di truyền là một trong những công cụ chúng ta có thể sử dụng để áp dụng cho các thuật toán học máy cho các bài toán tìm kiếm, tối ưu, và để giải quyết các vấn đề có hàng tỷ giải pháp có thể giải. Ý tưởng chính bắt nguồn từ sinh học để trả lời cho các vấn đề có không gian tìm kiếm lớn bằng cách liên tục tạo ra các giải pháp và đánh giá độ **tốt** của các giải pháp phù hợp với kết quả mong muốn, và tinh chỉnh các giải pháp tốt nhất.

Khi giải quyết vấn đề bằng thuật toán di truyền, thay vì yêu cầu một giải pháp cụ thể, bạn cung cấp các đặc điểm mà giải pháp **phải có** để giải pháp đó được chấp nhận. Ví dụ khi bạn muốn đổ đầy một chiếc xe tải đang di chuyển bạn cung cấp một bộ quy tắc như: đặt những thứ lớn lên trước, phân bổ cân bằng trọng lượng của xe. đặt những thứ nhẹ lên trên nhưng không được lỏng lẻo, lồng những thứ có hình dạng kỳ lạ để chúng không di chuyển xung quanh.


## Mục tiêu các vấn đề cần giải quyết
Hãy tưởng tượng bạn có 10 cơ hội để đoán một số trong khoảng từ 1 đến 1000 và khi bạn đoán 1 số bạn sẽ nhận được phản hồi của máy tính hoặc người quản trò là **đúng** hoặc **sai**. Bạn có thể đoán số chính xác ? Khi mà chỉ có phản hồi là **Đúng** hoặc **sai** bạn không có cách nào để cải thiện dự đoán của bạn. Tất nhiên bạn không thể sử dụng giải thuật di truyền để giải quyết những bài toán như vậy. Một khía cạnh cơ bản của giải thuật di truyền là  là chúng ta phải cung cấp thông tin phán đoán đó có tốt hay không. Sự phản hồi ở đây được gọi là **thể lực** (fitness).


Nếu thay vì đúng hoặc sai khi phản hồi bạn nhận được **cao hơn** hoặc **thấp hơn** cho thấy **số bạn cần đoán** và **số bạn đoán** cao hơn hay thấp hơn so với nhau. Bạn sẽ luôn tìm thấy được số đó vì 10 lần đoán là đủ để sử dụng thuật toán **tìm kiếm nhị phân** trong khoảng từ 1 đến 1000.

Bây giờ hãy tưởng tượng nhân kích thước của vấn đề này để thay vì cố gắng tìm 1 số bạn đang cố gắng tìm một bộ 100 số, tất cả trong phạm vi từ 1 đến 1000. Bạn chỉ nhận được giá trị **fitness** (thể lực, độ tốt) cho biết **mức độ** của dãy số so với dãy số mong muốn. Mục tiêu của bạn sẽ là tối đa hoặc tối thiểu **fitness** Bạn sẽ tìm ra nhiều kết quả hoặc bạn có thể dạy cho giải thuật nên bỏ qua những bộ số nào để nó đạt tối thiểu.

Các thuật toán di truyền và lập trình di truyền rất tốt trong việc tìm giải pháp cho các vấn đề rất lớn. Họ làm điều đó bằng cách lấy hàng triệu mẫu từ không gian tìm kiếm, thực hiện các thay đổi nhỏ, có thể kết hợp lại các phần của các giải pháp tốt nhất, so sánh kết quả **fitness** với kết quả tốt nhất hiện tại. Quá trình này lặp lại cho đến khi một điều kiện dừng sảy ra: giải pháp đã biết được tìm thấy, một giải pháp đáp ứng tất cả các yêu cầu được tìm thấy, một số gen quy định đã được sinh ra, thời gian ...

## Dự án đầu tiên

Hãy tưởng tượng bạn nhận được một yêu cầu đoán mật khẩu gồm 3 chữ cái. Bạn mong muốn nhận được sự phản hồi là gì về kết quả mà bạn đã đoán? Ví dụ: Nếu mật khẩu là ***'aaa'*** và bạn đoán là **'abc'** giá trị $$ fitness $$ nên là gì ? Sẽ phải có một phản hồi đơn giản như: có bao nhiêu chữ cái trong dự đoán của bạn đúng. ví dụ: **'bab'** có một chữ cái đúng, **'zap'** cũng đúng nhưng có một giá trị $$ fitness $$ kém hơn so với giá trị $$ fitness $$ của **aaa**  giá trị $$ fitness $$ ở đây có thể là khoảng cách giữa 2 chuỗi khi sắp sếp theo bảng chữ cái, chữ **abc** gần với **aaa** hơn so với **zap** đây là một vấn đề mà các bạn cần quan tâm khi bắt đầu xây dựng giải pháp cho vấn đề của bạn. Giải thuật di truyền rất tốt trong việc tìm giải pháp tốt cho các vấn đề với không gian tìm kiếm lớn vì chúng có thể nhanh chóng tìm thấy các phần dự đoán cải thiện giá trị $$ fitness $$ để có giải pháp tốt hơn.

Trong dự đoán trên giá trị $$ fitness $$ trả về số lượng chữ cái khớp với mật khẩu. Điều này có nghĩa là 'abc', 'bab' và 'zba' đều trả về giá trị là 1 vì mỗi cái đều có một chữ cái đúng. Thuật toán di truyền có thể kết hợp 2 chữ cái đầu tiên của 'abc' với chữ cái cuối cùng của 'zba' để tạo ra dự đoán 'aba'

Chúng ta sẽ xem xét thêm về dự án dò mật khẩu trong phần này và tiếp tục khám phá nhiều dự án khác nhau để tìm hiểu các cách khác nhau để giải quyết vấn đề với giải thuật di truyền.

## Lập trình di truyền với python

Lý do tôi chọn python vì nó đơn giản và dễ học nếu bạn từng học lập trình trước đó hay chưa học thì nó cũng sẽ dễ dàng với bạn vì python là một ngôn ngữ trong sáng. Gần với ngôn ngữ tự nhiên.

## Hello world

### Đoán số của tôi

Hãy bắt đầu bằng cách học một chút về các thuật toán di truyền. Chúng ta có một trò chơi đơn giản dành cho 2 người, trong đó một người chọn một số bí mật từ 1 đến 10 và người còn lại phải đoán:

```

Nó là số  2? Sai
Nó là số 3? Sai
Nó là số 7? Sai
Nó là số 1? Đúng

```