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

Median 
```
  1 2 | 3 | 4 4
```
