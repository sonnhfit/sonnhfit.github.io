---
layout: post
title: Giải thuật di truyền và ứng dụng với python
mathjax: true
---

Chào các bạn mình là **Sơn Nguyễn** ở trong bài viết này mình sẽ hướng dẫn các bạn hiểu cũng như xây dựng một chương trình đơn giản với giải thuật di truyền. Để các bạn có thể ứng dụng giải thuật di truyền vào những bài toán cụ thể của các bạn. Trong các lĩnh vực khác của khoa học máy tính.

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

Nếu câu trả lời là đúng hoặc sai thì nó vẫn thực hiện khả thi trong khoảng từ 1 đến 10 nhưng nhanh chóng trở chán nản hơn khi chúng ta tăng phạm vi lên 1 - 100 hoặc 1 - 1000. Bởi vì chúng ta không thể cải thiện dự đoán. Điều này không khác gì việc chúng ta đoán một cách lần lượt từ 1 đến hết khá là mất thời gian và công sức.

```
Nó là số  1? Sai
Nó là số 2? Sai
Nó là số 3? Sai
Nó là số 4? Sai
Nó là số 5? Sai
Nó là số 6? Sai
...

```

Để trò chơi chở nên thú vị hơn chúng ta sẽ nói **cao hơn** hoặc **thấp hơn**.

```
1? Cao hơn
7? thấp hơn
6? thấp hơn
5? thấp hơn
4? Đúng

```

Điều này có thể khá thú vị trong một khoảng thời gian và với phạm vi từ 1 - 10 nhưng ngay sau đó chúng ta tăng phạm từ 1 - 100. Bởi vì đây là một trò chơi thi xem ai đoán giỏi hơn. Tại thời điểm này người nào có chiến lược đoán hiệu quả nhất sẽ chiến thắng.

Tuy nhiên, một điều mà mọi người thường làm là sử dụng phương pháp loại trừ. Ví dự như sau:

```
1? Cao hơn
7? Thấp hơn
```

Tại sao chúng ta sẽ không đoán 8, 9 hoặc 10 nữa ? Tất nhiên lý do là chúng ta đã biết nó là những con số lớn hơn 7.

> chú ý
>> Khi các bạn chơi bài, những người chơi giỏi thường ghi nhớ những lá bài  đã được đánh. Và quan sát đối thủ cũng như biết được các tình huống có thể xảy ra với những lá bài chưa được đánh để có thể dành chiến thắng.

Một thuật toán di truyền không biết cái nào là xấu hơn cái nào tốt hơn thì nó được coi là không có trí thông minh. Nó sẽ không học, và tiếp tục mắc sai lầm mỗi lần. Nếu không thể học được thì nó chỉ có thể giải quyết các vấn đề như được lập trình một cách tuần tự. Tuy nhiên mục đích của chúng ta là sử dụng nó để giải quyết các vấn đề mà con người sẽ đấu tranh để giải quyết hoặc không thể giải quyết được, làm thế nào các thuật toán di truyền có thể làm được điều đó ?

Các thuật toán di truyền thăm dò ngẫu nhiên không gian bài toán kết hợp với các quá trình tiến hóa như đột biệt, lai chéo, để cải thiện dự đoán. Nhưng bởi vì thuật toán không sử dụng kinh nghiệm, phương pháp loại trừ, ... nên thuật toán sẽ thử những thứ con người sẽ không bao giờ nghĩ để thử. Do đó chúng ta có thể cải tiến thuật toán và giới hạn không gian bài toán để có những kết quả tiềm năng.

### Đoán mật khẩu

Bây giờ chúng ta sẽ áp dụng những thứ ở trên như thế nào cho việc đoán mật khẩu. Bắt đầu với một chuỗi chữ cái được tạo ngẫu nhiên sau đó thay đổi một chữ cái ngẫu nhiên tại một thời điểm cho đến khi tìm được chuỗi chữ cái là ```hello world!``` về mặt lý thuyết và thủ công không có tý gì gọi là thông minh ai cũng có thể nghĩ ra cái giải thuật này thì sẽ như sau:

```

_letters = [a..zA..Z !]
target = "Hello World!"
guess = lấy ngẫu nhiên 12 ký tự từ _letters
while guess != target:
  index = lấy ngẫu nhiên giá trị từ [0..độ dài của target]
  guess[index] = lấy một ký tự ngẫu nhiên từ _letters

```

Nếu bạn thử viết điều này với ngôn ngữ lập trình yêu thích của bạn, bạn sẽ thấy rằng nó hoạt động kém hiệu quả hơn so với việc chơi trò đoán số và thuật toán không thể biết nó đoán tốt hơn hay xấu hơn.

Một giải pháp là giúp nó đoán đúng bằng cách cho nó biết có bao nhiêu chữ cái trong số đoán là đúng vị trí. Ví dụ **"World!Hello?"** sẽ nhận được kết quả là 2 vì chỉ có 2 chữ cái đúng vị trí so với từ **"Hello World!"** (chữ l) 2 ở đây được gọi là giá trị $$ fitness $$.

### Chương trình đầu tiên

#### Gen

Để bắt đầu thuật toán di truyền cần một bộ gen sử dụng để xây dựng dự đoán. Đối với dự án này sẽ là một bộ chung chữ cái. Nó cũng cần một mật khẩu đích để đoán.

```python
geneSet = " abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!."
target = "Hello World!"
```

#### Tạo một dự đoán

Tiếp theo thuật toán cần tạo ra một chuỗi ngẫu nhiên từ bộ gen
```python
import random
def generate_parent(length):
    genes = []
    while len(genes) < length:
        sampleSize = min(length - len(genes), len(geneSet))
        genes.extend(random.sample(geneSet, sampleSize))
    return ''.join(genes)

```

#### Fitness

giá trị $$ fitness $$ mà thuật toán di truyền cung cấp là phản hồi duy nhất. Trong phần này giá trị $$ fitness $$ là tổng số chữ cái trùng khớp với mật khẩu.

Mình định nghĩa hàm này như sau:

```python
def get_fitness(guess):
    return sum(1 for expected, actual in zip(target, guess)
        if expected == actual)
```

hàm trên sẽ trả về số ký tự ở đúng vị trí của dự đoán.

#### Đột biến

Chúng ta có hàm đột biến gen này để giải quyết vấn đề nếu một Gen mới (newGen) được chọn ngẫu nhiên trùng với gen mà chúng ta đã xem xét.
Điều này sẽ giúp chúng ta giảm thiểu việc tính toán không cần thiết. 
Và đây cũng là cách mà chúng ta có thể tạo ra một dự đoán mới bằng cách thay đổi dự đoán hiện tại.

```python
def mutate(parent):
    index = random.randrange(0, len(parent))
    childGenes = list(parent)
    newGene, alternate = random.sample(geneSet, 2)
    childGenes[index] = alternate if newGene == childGenes[index] else newGene
    return ''.join(childGenes)

```

Việc triển khai này chuyển đổi mỗi chuỗi parent thành một mảng với hàm **list(parent)**, sau đó thay thế 1 chữ cái trong mảng bằng cách chọn ngẫu nhiên từ geneSet.

#### Hiển thị

Tiếp theo, điều quan trọng là phải theo dõi những gì đang xả ra.

```python
import datetime
def display(guess):
    timeDiff = datetime.datetime.now() - startTime
    fitness = get_fitness(guess)
    print("{}\t{}\t{}".format(guess, fitness, timeDiff))

```

#### Hàm main

Hàm main bắt đầu bằng việc khởi tạo **bestParent** một cách ngẫu nhiên là hiển thị nó.

```python

random.seed()
startTime = datetime.datetime.now()
bestParent = generate_parent(len(target))
bestFitness = get_fitness(bestParent)
display(bestParent)

```
Cuối cùng là một vòng lặp

- Tạo ra một dự đoán
- Tính toán giá trị $$ fitness $$ cho dự đoán đó
- So sánh $$ fitness $$ với giá trị $$ fitness $$ tốt nhất của các dự đoán trước đó
- Giữ dự đoán với giá trị $$ fitness $$ tốt hơn

Chu kỳ này lặp lại cho đến khi xảy ra điều kiện dừng, trong trường hợp này điều kiện dừng là khi chúng ta tìm được chữ **Hello World!**.

```python


while True:
    child = mutate(bestParent)
    childFitness = get_fitness(child)
    if bestFitness >= childFitness:
        continue
    display(child)
    if childFitness >= len(bestParent):
        break
    bestFitness = childFitness
    bestParent = child

```

Toàn bộ đoạn code trên như sau:

```python

import random
import datetime

geneSet = " abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!."
target = "Hello World!"


def generate_parent(length):
    genes = []
    while len(genes) < length:
        sampleSize = min(length - len(genes), len(geneSet))
        genes.extend(random.sample(geneSet, sampleSize))
    return ''.join(genes)

def get_fitness(guess):
    return sum(1 for expected, actual in zip(target, guess) if expected == actual)

def mutate(parent):
    index = random.randrange(0, len(parent))
    childGenes = list(parent)
    newGene, alternate = random.sample(geneSet, 2)
    childGenes[index] = alternate if newGene == childGenes[index] else newGene
    return ''.join(childGenes)


def display(guess):
    timeDiff = datetime.datetime.now() - startTime
    fitness = get_fitness(guess)
    print("{}\t{}\t{}".format(guess, fitness, timeDiff))

random.seed()
startTime = datetime.datetime.now()
bestParent = generate_parent(len(target))
bestFitness = get_fitness(bestParent)
display(bestParent)


while True:
    child = mutate(bestParent)
    childFitness = get_fitness(child)
    if bestFitness >= childFitness:
        continue
    display(child)
    if childFitness >= len(bestParent):
        break
    bestFitness = childFitness
    bestParent = child

```
