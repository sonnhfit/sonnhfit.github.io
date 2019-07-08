---
layout: post
title: Statistics the average nodes
mathjax: true
---
Bài viết này mình sẽ tổng hợp các cách biểu diễn central tendency trong numpy, Central tendency là giá trị mô tả cho giá trị  trung bình của một dãy số và có rất nhiều kiểu biểu diễn central tendency. 

## Central Tendency
Các các biểu diễn central tendency cơ bản 

### Mean (arithmetic)

Là cách đo phổ biến của central tendency 

$$ \frac{1 + 1 + 2 + 3 + 4}{5} = \frac{11}{5} = 2.2 $$

```python 
import numpy as np
np.mean([1, 1, 2, 3, 4])

# Result :  2.2
```

### Median 

Median là giá trị ở giữa khi chúng ta sắp sếp dãy số 
```
  1 2 | 3 | 4 4 
  median = 3
```

Với trường hợp dãy số có số lượng phần tử chẵn không tìm đc giá trị ở giữa ta có thể lấy kết quả trung bình của 2 số ở giữa ví dụ 

```
1 2 | 3 4 | 4 5
median = 3.5 
```
Để tính median trong numpy ta thực hiện như sau 4

```python 
np.median([1, 2, 3, 4, 4, 5])

```

## Mode 

Mode là số có tần xuất xuất hiện nhiều nhất trong dãy số, nếu một dãy số có nhiều phần tử có tần xuất xuất hiện bằng nhau thì người ta thường lấy số có giá trị nhỏ nhất.
Các bạn có thể quan sát ảnh sau 

![central tendency mode ](https://statistics.laerd.com/statistical-guides/img/mode-1.png)

![Central tendency mode](https://statistics.laerd.com/statistical-guides/img/mode-1a.png)


