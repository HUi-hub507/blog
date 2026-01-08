---
title: SQL-我的易错知识
published: 2026-01-08
description: 一些SQL容易忘记的东西
image: ./image/background.png
tags: ["SQL", "学习"]
category: 学习
draft: false
---

# 易忘知识点

一、LEFT JOIN 和RIGHT JOIN的区别

LEFT JOIN 和RIGHT JOIN 都是连接方式，LEFT JOIN会保留左边表的全部列，RIGHT JOIN 则是保留右边表的全部列。

```sql
SELECT ... FROM 左表 LEFT JOIN 右表 ON 连接条件
-- 保留左表的所有行，即使右表没有匹配的行，右表没有匹配的行时，结果表中右表列将包含NULL值。
-- 右连接同理
SELECT ... FROM 左表 RIGHT JOIN 右表 ON 连接条件
```

二、 OVER函数

OVER()是窗口函数，在我的理解里面是直接返回一个新行，具体可以看下面的例子

```SQL
SELECT 
	student_name,
	grade
	AVG(grade) OVER() AS avg_grade
FROM student_grade;
-- 最终返回结果是学生名字，学生成绩，平均成绩，三个字段。
-- 平均成绩：每行都会显示全班学生的平均成绩。

SELECT
	student_name,
	major,
	grade
	AVG(grade) OVER(PARTITION BY major) AS avg_major_grade
FROM student_grade;
-- 最终返回结果是学生名字，学生成绩，专业平均成绩，三个字段。
-- 专业平均成绩：每行都会显示该学生所在专业的平均成绩。

SELECT
	student_name,
	grade
	SUM(grade) OVER(ORDER BY grade) AS cumulative_salary
FROM student_grade;
-- 最终返回结果是学生名字，学生成绩，成绩累计分数，三个字段。
-- 成绩累计字段：每行都会显示一个成绩累计分数，升序排序。如60,110,190....


```

三、CASE WHEN THEN ELSE END

```SQL
SELECT ... 
	CASE
		WHEN 条件1 THEN 结果1
		WHEN 条件2 THEN 结果2
		WHEN 条件3 THEN 结果3
		ELSE 默认结果
	END AS 起个名字
FROM ...

-- 如果是比较固定值的话
CASE 列名
	WHEN 值1 THEN 结果1
	WHEN 值2 THEN 结果2
	...
	ELSE 默认结果
END

-- 如果是条件判断
CASE
	WHEN 条件1 THEN 结果1
	WHEN 条件2 THEN 结果2
	...
	ELSE 默认结果
END
```

