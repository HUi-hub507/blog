---
title: numpy和pandas基本以及常忘知识点
published: 2026-01-08
description: 一些numpy和pandas的写法
image: ./image/background.png
tags: ["Python", "学习"]
category: 学习
draft: false

---

## numpy和pandas基本以及常忘知识点

一、如果要把分数低于60的标记为不合格，高于60分标记为合格

```Python
import pandas as pd
import numpy as np

# 示例数据
df_students = pd.DataFrame({
    'name': ['张三', '李四', '王五', '赵六'],
    'score': [85, 59, 72, 45]
})

# np.where
df_students['result'] = np.where(df_students['score'] >= 60, '合格', '不合格')

print("添加'result'列后:")
print(df_students)
```

np.where语法

```python
import numpy as np
np.where(条件式, '成立后返回的结果', '不成立返回的结果')
#np.where一般只能返回两个结果
```

有多个等级(不合格，合格，良好，优秀)时的写法

```python
# 创建更复杂的数据
df_students = pd.DataFrame({
    'name': ['张三', '李四', '王五', '赵六', '孙七'],
    'score': [95, 59, 72, 45, 88]
})

# 定义条件和对应的结果
conditions = [
    df_students['score'] >= 90,            # 优秀
    df_students['score'] >= 80,            # 良好
    df_students['score'] >= 70,            # 中等
    df_students['score'] >= 60,            # 及格
    df_students['score'] < 60              # 不及格
]

choices = ['优秀', '良好', '中等', '及格', '不及格']

df_students['grade'] = np.select(conditions, choices, default='未知')

print("多条件判断结果:")
print(df_students)
```

np.select语法

```python
import numpy as np
np.select(条件, 结果, default=‘默认值’)
```

