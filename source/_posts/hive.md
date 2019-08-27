---
title: hive
date: 2019-08-13 11:42:07
tags: [数据库,编程语言]
categories: Hadoop
permalink: HDFS/hive.md
---

# 查看表结构

| 命令                                                         | 说明                   |
| ------------------------------------------------------------ | ---------------------- |
| `show tables like '*name*'`                                  | hive模糊搜索表         |
| `desc formatted table_name`<br>`desc table_name`             | 查看表结构信息         |
| `show partitions table_name`                                 | 查看分区信息           |
| `select table_coulm from table_name where partition_name = '2014-02-25';` | 根据分区查询数据       |
| `dfs -ls /user/hive/warehouse/table02;`                      | 查看hdfs文件信息       |
| `dfs -tail /user/hive/warehouse/table02;`                    | 显示hdfs文件的一行信息 |

# 创建表格

| 命令              | 说明             |
| ----------------- | ---------------- |
|                   |                  |
| `create table as` | 选中表格创建表格 |
|                   |                  |

## create table as

create创建部分可以指定表的存储格式等属性，比如指定新表的行列分隔符，存储格式等。

```sql
CREATE TABLE temp_copy
   ROW FORMAT DELIMITED
      FIELDS TERMINATED BY '\t'
      LINES TERMINATED BY '\n';
   STORED AS textfile
AS
SELECT *  FROM temp WHERE start_date IS NOT NULL;
```

1. `hive`中用`CTAS `创建表，所创建的表统一都是非分区表，不管源表是否是分区表。所以对于分区表的创建使用`create table ..as`一定要注意分区功能的丢失。当然创建表以后可以添加分区，成为分区表。

2. 如果使用`create table as  select  *  `创建表时源表是分区表，则新建的表会多字段，具体多的字段个数和名称就是源表分区的个数和名称。当然如果`select`选择的是指定的列则不会有这种问题。
3. 如果源表的存储格式不是`textfile`。则使用`CTAS`创建的表存储格式会变成默认的格式`textfile`。比如这里源表是`RCFILE`。而新建的表则是`textfile`。当然可以在使用`create table ....as`创建表时指定存储格式和解析格式，甚至是列的名称等属性。具体参考博客：hive使用create as创建表指定存储格式等属性
4. 使用`CTAS`方式创建的表不能是外部表。
5. 使用`CTAS`创建的表不能分桶表。对于每一个表或者是分区，Hive可以进一步组织成桶，也就是说桶是更为细粒度的数据范围划分。

