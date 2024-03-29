---
title: PSI
date: 2019-08-26 14:24:22
categories: [机器学习]
permalink: 机器学习/PSI.md
---

# 简介

由于模型是以特定时期的样本所开发的，此模型是否适用于开发样本之外的族群，必须经过稳定性测试才能得知。稳定度指标(population stability index ,PSI)可衡量测试样本及模型开发样本评分的的分布差异，为最常见的模型稳定度评估指针。其实PSI表示的就是按分数分档后，针对不同样本，或者不同时间的样本，population分布是否有变化，就是看各个分数区间内人数占总人数的占比是否有显著变化。

| PSI<0.1    | 0.1~0.25 | PSI>0.25​ |
| ---------- | -------- | -------- |
| 稳定性很高 | 一般     | 稳定性差 |

<!--more-->

# 计算

$$
PSI=\sum_i^n {(Ac-Ex)} \times {ln (Ac/Ex)}
$$

其中：$Ac$是实际占比；$Ex$是期望占比

## 计算PSI

将数据集划分为`base`与`test`两个数据集。

### 模型

1. 将基准数据集`base`的score划分为10个区间，将测试数据集`test`的score按照相同的边界值划分为10个区间
2. 分别统计各个分区基准score的个数$B_i$、预测score的个数$T_i$
3. 分别统计各个分区基准score的个数比例$P_B$、预测score的个数比例$T_B$
4. 计算 $PSI=\sum {\left(P_B(i)-P_T(i) \right)} \times {ln(P_B(i)/P_T(i))}$

### 特征

1. 将基准数据集`base`的特征划分为10个区间，将测试数据集`test`的特征按照相同的边界值划分为10个区间
2. 分别统计各个分区基准`feature`的个数$B_i$、预测`feature`的个数$T_i$
3. 分别统计各个分区基准`feature`的个数比例$P_B$、预测`feature`的个数比例$T_B$
4. 计算 $PSI=\sum {(P_B(i)-P_T(i))} \times {ln(P_B(i)/P_T(i))}$
   