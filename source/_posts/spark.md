---
title: spark
date: 2019-08-09 17:08:07
tags: [人工之恩呢,分布式系统]
categories: spark
---

# spark简介

Spark是开发通用的大数据处理框架。Spark应用程序可以使用R语言、Java、Scala和Python进行编写，极少使用R语言编写Spark程序，Java和Scala语言编写的Spark程序的执行效率是相同的，但Java语言写的代码量多，Scala简洁优雅，但可读性不如Java，Python语言编写的Spark程序的执行效率不如Java和Scala。

## 运行模式

Spark有4中运行模式：

| 名称       | 说明                                          |
| ---------- | --------------------------------------------- |
| local      | 适用于测试                                    |
| standalone | 并非是单节点，而是使用spark自带的资源调度框架 |
| yarn       | 最流行的方式，使用yarn集群调度资源            |
| mesos      | 国外使用的多                                  |

## RDD

RDD是**弹性分布式数据集**，**是Spark中最基本的数据抽象**。

<center>

```mermaid
graph TD
[]
```

</center>



