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

二、计算固定数量间隔的总和或平均（比如1-5,2-6,3-7这种）

```python
df表['字段'].rolling(window=间隔).聚合函数()
#案例，每隔五个计算一次平均分数，1号到5号，2号到6号...
df_avg = df_score["score"].rolling(window = 5).mean()
```

三、pd.data_range()用法

```python
#语法规则
pd.date_range(start=None, end=None, periods=None, freq='D', tz=None, normalize=False, name=None, closed=None, **kwargs)
#start：开始日期；end：结束日期；periods：需要生成的时间数量，
#freq：频率或者说计算单位，默认是“D”，表示天，常见的还有“B”，工作日；“W”，周；“M”，月末；“MS”，月初；“Y”,年末；“YS”，月初；还可以使用复合频率，比如“2D”表示每两天。
#closed：表示是否闭合，可以是“left”或者“right”，默认是None，表示两端闭合，“left”表示左端闭合，右端开，即不包括最后一天。

#案例，从2023-01-10开始的日期，一共一百天
dates = pd.date_range(start='2023-01-01', periods=100)
#案例，从2023-01-01开始，到2023-12-31结束
dates = pd.date_range(start="2023-01-01", end="2023-12-31")
#案例，从2023-12-31结束，往前算5天
dates = pd.date_range(end="2023-12-31", periods=5,freq="D")
```

四、groupby()用法

```python
df表.groupby("字段")['字段'].聚合函数()
#举例
import pandas as pd
import numpy as np

# 创建示例数据
np.random.seed(42)
df = pd.DataFrame({
    'Product': ['A', 'B', 'A', 'C', 'B', 'A', 'C', 'B', 'A', 'C'],
    'TotalSale': [100, 200, 150, 300, 250, 120, 400, 180, 210, 350],
    'Quantity': [5, 10, 8, 15, 12, 6, 20, 9, 11, 18]
})

print("原始数据：")
print(df)
print("\n按产品类型分组计算价格总额", df.groupby('Product')['TotalSale'].sum())
```

五、sort_values()用法

```python
series.sort_values(ascending=True/False)
#将数组进行排序，ascending=True代表升序，Flase代表降序
#组合使用，按照产品类型分组计算价格总额，并且降序排列
product_sales = df.groupby('Product')['TotalSale'].sum().sort_values(ascending=False)
```

