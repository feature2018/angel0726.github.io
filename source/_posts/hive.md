---
title: hive
date: 2019-08-13 11:42:07
tags: [数据库,编程语言]
categories: Hadoop
permalink: HDFS/hive.md
---

# 查看表结构

| 命令                                                         | 说明             |
| ------------------------------------------------------------ | ---------------- |
| `show tables like '*name*'`                                  | hive模糊搜索表   |
| `desc formatted table_name`<br>`desc table_name`             | 查看表结构信息   |
| `show partitions table_name`                                 | 查看分区信息     |
| `select table_coulm from table_name where partition_name = '2014-02-25';` | 根据分区查询数据 |
| `dfs -ls /user/hive/warehouse/table02;`                      | 查看hdfs文件信息 |

