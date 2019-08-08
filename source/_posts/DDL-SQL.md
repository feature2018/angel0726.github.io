---
title: DDL-SQL
date: 2019-08-06 21:07:59
tags: [数据库,编程语言]
categories: SQL
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
CREATE TABLE table_name
(
    列名1  数据类型(size)  约束条件,
    列名2  数据类型(size)  约束条件,
    列名3  数据类型(size)  约束条件,
    ....
);
```

| 参数     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 列名     | 规定表中列的名称                                             |
| 数据类型 | 例如`varchar、integer、decimal、date`                        |
| 约束条件 | `Primary key` &emsp;&emsp;&emsp;&emsp;&emsp;主键约束。每个表只能创建一个主键约束<br> `Unique`&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;唯一性约束（即候选键）。可以有多个唯一性约束。<br/> `Not null`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&emsp;&emsp;&emsp;&emsp;&emsp;非空约束。是指该列允许不允许有空值出现，如选择了Not null表明该列不允许有空值出现。<br/>`CHECK (search_cond)`&nbsp;&nbsp;&nbsp;&nbsp;列值满足条件，条件只能使用列当前值。<br/>`search_cond`为条件 <br/>`FOREIGN KEY ` 保证一个表中的数据匹配另一个表中的值的参照完整性。 |

&nbsp;

