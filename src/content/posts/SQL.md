---
title: SQL学习
published: 2025-10-13
description: 简单的SQL笔记
image: ./cover.jpg
tags: ["SQL", "学习"]
category: 学习
draft: false
---



这是SQL学习笔记，包括简单的SQL代码，不涉及具体的名词解释和含义解释。

## 一、DDL（Data Definition Language）数据定义语言

### 1.对数据库进行操作

```sql
-- 创建一个名位“db”的数据库
create database db;
-- 检查是否“db”数据库是否存在，不存在则创建
create database if not exists db;
-- 查看所有数据库
show database;
-- 查看某个数据库的定义信息
show create database db1;
-- 修改数据库字符信息
alter datagbase db character set utf8;
-- 删除数据库
drop database db1;
-- 查看当前数据库；
select database();
```

### 2.对表进行操作

```sql
-- 创建表
create table student(
	id int comment "编号", 
	name varchar(32),
	age int,
	score double(4,1),
	birthday date,
    address varchar(10),
	insert_time timestamp
) comment "学生表";
-- 查询当前数据库内的所有表
show tables;
-- 查询表的结构
desc 表名;
-- 查询指定表的创建语句
show create table 表名;
-- 修改表名
alter table 表名 rename to 新表名;
-- 向表内添加新字段
alter table 表名 add 字段名 数据类型 comment 注释;
-- 修改数据类型
alter table 表名 modify 字段名 新数据类型;
-- 修改字段名和字段类型
alter table 表名 change 旧字段名 新字段名 类型长度 comment 注释;
-- 删除字段
alter table 表名 drop 字段名 数据类型;
-- 删除表
drop table 表名;
drop table 表名 if exists 表名;
-- 删除指定表，并重新创建该表
truncate table 表名;
```

## 二、DML(Data manipulation Language)数据操作语言

### 1. 增加 insert into

```sql
-- 给指定字段添加数据
insert into 表名(字段名1, 字段名2, ..., 字段名n) values(值1, 值2, ..., 值n);
-- 给全部字段添加数据
insert into 表名 values(值1, 值2, ...);
-- 批量添加数据
insert into 表名(字段名1, 字段名2, ...) values(值1, 值2, ...),(值1, 值2, ...),(值1, 值2, ...);
insert into 表名 values(值1, 值2, ...),(值1, 值2, ...),(值1, 值2, ...);
```

### 2. 修改 updata

```sql
-- 修改数据
update 表名 set 字段名1 = 值1, 字段名2 = 值2, ...[where 条件];
-- 修改student表里面id为1的数据，将name修改为Alice, age修改为14岁
update student set name = "Alice", age = 14 where id = 1;
```

### 3.删除delete

```sql
-- 删除数据
delete from 表名[where条件];
-- 删除student表里面name为“black goat”的数据
delete from student where name = "black goat";
```

## 三、DQL（Data Query Language）数据查询语言

## 基本格式

```sql
--查询数据
select 
	字段列表
from
	表名
where
	条件列表
group by
	分组字段列表
having
	分组后条件列表
order by
	排序字段列表
limit
	分页参数
```

## 1.基本查询

```sql
-- 查询多个字段
select 字段1, 字段2, 字段3, ...from 表名;
select * from 表名;
-- 设置别名
select 字段1[as 别名1], 字段2[as 别名2] from 表名;
-- 去除重复记录
select distinct 字段列表 from 表名;

```

## 2.条件查询

```sql
select 字段列表 from 表名 where 条件列表;
-- 查询名字叫Alice的信息
select * from studet where name = "Alice";
-- 查询性别为女并且年龄小于20岁的信息
select * from student where gender = "女" and age < 20;
-- 查询名字为两个字的信息
select * from student where name like "__";
-- 查询姓克的信息
select * from student where name like "王%";
```

### 3.聚合函数

```sql
-- 查询所有学生数量
select count(*) from student;
-- 查询学生的平均年龄
select avg(age) from sudent;
-- 查询学生的最大年龄
select max(age) from student;
-- 查询学生的最小年龄
select min(age) from student;
-- 统计学生年龄之和
select sum(age) from student;
```

### 4.分组查询

```sql
-- 基本格式
select 字段列表 from 表名 [where 条件] group by 分组字段名 [having 分组后过滤条件];
-- 根据性别分组，统计男性学生和女性学生的数量
select gender, count(*) from student group by gender;
-- 根据性别分组，统计男性学生和女性学生的平均年龄
select gender, avg(age) from student group by gender; 
-- 查询年龄小于20岁的学生，并根据家庭住址分组，获取家庭住址数量大于3个的地址
select address, count(*) as address_count from student where age < 20 group by address having address_count > 3;
```

### 5.排序查询

```sql
-- 基本格式
select 字段列表 from 表名 order by 字段1 排序方式1, 字段2 排序方式2;
-- 根据年龄对学生进行升序排序
select * from student order by age asc;
-- 根据年龄对学生进行降序排序
select * from student order by age desc;
-- 根据年龄对学生进行升序排序，年龄相同，按照id号进行降序排序
select * from student order by age asc, id desc;
```

### 6.分页查询

```sql
-- 基本格式
select 字段列表 from 表名 limit 起始索引, 查询记录数;
-- 查询第一页数据，每页展示10条记录
select * from student limit 0, 10;
select * from student limit 10;
-- 查询第二页数据，每页展示10条记录(页码-1)*页展示记录数
select * from student limit 10, 10;
```

## 三、外键约束

```sql
-- 添加外键
create table 表名(
	字段名 数据类型,
    ...,
    [constraint][外键名称] foreign key(外键字段名) references 主表 (主表列名)
);

alter table add constraint 外键名称 foreign key (外键字段名) references 主表 (主表列名);
```
