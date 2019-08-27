---
title: DDL-SQL
date: 2019-07-31 21:07:59
tags: [数据库,编程语言]
categories: SQL
permalink: SQL/DDL-SQL.md
---

# 数据库

```sql
-- 创建数据库
Create database my_db; 
-- 删除数据库
Drop database my_db;
-- 指定数据库
use my_db;
-- 关闭数据库
close my_db; 
```

<!--more-->

# 表

```sql
--  创建表格
CREATE TABLE table_name
--  修改表格
alter table tablename 
--  删除表格
DROP TABLE Persons
```

## 创建表格

```sql
create table 表名 as 
	select 列名 from 表名
```

```sql
CREATE TABLE Persons
(
    P_Id int NOT NULL PRIMARY KEY CHECK (P_Id>0),  --不为空，主键，删选条件：P_Id>0
    LastName varchar(255) NOT NULL,      		   --不为空
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) DEFAULT 'Sandnes'            --默认值为'Sandnes'
);
```

```sql
CREATE TABLE table_name
(
    列名1  数据类型(size)  约束条件,
    列名2  数据类型(size)  约束条件,
    列名3  数据类型(size)  约束条件,
    ....
);
```

<table>
  <tr>
    <th>参数</th>
    <th colspan="2">说明</th>
  </tr>
  <tr>
    <td>列名</td>
    <td colspan="2">规定表中列的名称</td>
  </tr>
  <tr>
    <td>数据类型</td>
    <td colspan="2">例如varchar、integer、decimal、date。不同的数据库有不同的数据类型</td>
  </tr>
  <tr>
    <td rowspan="7">约束条件</td>
    <td>Primary key</td>
    <td>主键约束。每个表只能创建一个主键约束</td>
  </tr>
  <tr>
    <td>Unique</td>
    <td>唯一性约束（即候选键）。每个表可以有多个唯一性约束，但只能有一个Primary key。</td>
  </tr>
  <tr>
    <td>Not null</td>
    <td>非空约束。是指该列允许不允许有空值出现，如选择了Not null表明该列不允许有空值出现。</td>
  </tr>
  <tr>
    <td>CHECK (search_cond)</td>
    <td>约束用于限制列中的值的范围,search_cond为条件。如果对单个列定义 CHECK 约束，那么该列只允许特定的值；如果对一个表定义 CHECK 约束，那么此约束会在特定的列中对值进行限制。</td>
  </tr>
  <tr>
    <td>FOREIGN KEY</td>
    <td>一个表中的 FOREIGN KEY指向另一个表中的PRIMARY KEY</td>
  </tr>
  <tr>
    <td>DEFAULT</td>
    <td>如果没有规定其他的值，那么会将默认值添加到所有的新记录。</td>
  </tr>
  <tr>
    <td>AUTO_INCREMENT</td>
    <td>每次插入时，自动生成主键的值</td>
  </tr>
</table>

## 修改表格

```sql
alter table tablename 
    - add      增加新列 
    - drop     删除列或者完整性约束条件 
    - modify   修改列定义
```

```sql
-- 在表 "Person" 中添加一个名为 "Birthday" 的新列。
ALTER TABLE Person ADD Birthday date;
-- 删除 "Person" 表中的 "Birthday" 列：
ALTER TABLE Person DROP COLUMN Birthday;
-- 删除 "Person" 表中 "P_Id" 的主键：
ALTER TABLE Person DROP PRIMARY KEY(P_Id);
-- 改变 "Person" 表中 "Birthday" 列的数据类型。
ALTER TABLE Person Modify Birthday year;
```

## 删除表格

```sql
DROP TABLE table_name   -- 删除表
```

# 视图

表中存储的是实际数据，而视图中保存的是从表中取出数据所使用的` SELECT `语句。一般来说你可以用`update，insert，delete`等sql语句修改表中的数据，而对视图只能进行select操作。但是也存在可更新的视图，对于这类视图的`update，insert和delete`等操作最终会作用于与其相关的表中数据。

## 创建视图

<font color=red>**定义视图时不能使用 ORDER BY 子句**</font>

```sql
CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition
[with check option]  -- 指明当对视图进行insert，update，delete时，要检查进行insert/update/delete的元组是否满足视图定义中子查询中定义的条件表达式
```

```sql
CREATE VIEW CUSTOMERS_VIEW AS
SELECT name, age
FROM  CUSTOMERS
WHERE age IS NOT NULL
WITH CHECK OPTION; --这里 WITH CHECK OPTION 使得视图拒绝任何 AGE 字段为 NULL 的条目，因为视图的定义中，AGE 字段不能为空。对视图不管修改前还是修改后都必须遵从此规定。
```

## 使用视图

```sql
Select * From view_name
```

## 视图的更新（增、删、改）

一般来说你可以用`update，insert，delete`等sql语句修改表中的数据，而对视图只能进行select操作。但是也存在可更新的视图，对于这类视图的`update，insert`和`delete`等操作最终会作用于与其相关的表中数据。

对于可更新的视图，在视图中的行和基表中的行之间必须具有一对一的关系。还有一些特定的其他结构，这类结构会使得视图不可更新。如果视图包含下述结构中的任何一种，那么它就是不可更新的：

| 分类     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 非一对一 | DISTINCT关键字、GROUP BY子句、UNION运算符、位于选择列表中的子查询 |
| 未知     | 聚合函数、ORDER BY子句、HAVING子句、FROM子句中包含多个表、WHERE子句中的子查询，引用FROM子句中的表 |
| 其他     | SELECT语句中引用了不可更新视图<br>ALGORITHM 选项指定为TEMPTABLE（使用临时表总会使视图成为不可更新的） |

### 插入数据

```sql
INSERT INTO CUSTOMERS_VIEW
     VALUES('李牧',50);
```

### 修改数据

```sql
UPDATE CUSTOMERS_VIEW SET age = 58 where name = '李牧';
```

### 删除数据

```sql
DELETE FROM CUSTOMERS_VIEW  WHERE name = '李牧';
```

## 删除视图

```sql
Drop View view_name
```
