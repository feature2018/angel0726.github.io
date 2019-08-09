---
title: SQL
date: 2019-07-31 19:24:57
tags: [数据库,编程语言]
categories: SQL
---

# 名词解释

| 名称             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| 候选码（超级码） | 关系中的一个属性组，其值能唯一标识一个元组，若从该属性组中去掉任何一个属性，它就不具有这一性质了，这样的属性组称为候选码。 |
| 主码             | 当有多个候选码时，可以选定一个作为主码。                     |
| 主属性           | 包含在任何一个候选码中的属性被称为主属性。                   |
| 全码             | All-key关系模型的所有属性组组成该关系模式的候选码，称为全码。即所有属性当作一个码。若关系中只有一个候选码,且这个候选码中包含全部属性,则该候选码为全码。 |
| 外码             | 关系R中的一个属性组，它不是R的候选码，但它与另一个关系S的候选码相对应，则称为这个属性组为R的外码或外键。s |
| 实体完整性       | 关系主码中的属性值不能为空值。                               |

<!--more-->

# [关系运算](.\关系运算-SQL.md) 

<table>
  <tr>
    <th colspan="2">运算符</th>
    <th colspan="2">说明</th>
  </tr>
  <tr>
    <td rowspan="4">集合</td>
    <td>∪</td>
    <td>并-Union</td>
    <td rowspan="3">关系R和关系S具有相同的属性，且相应的属性来自同一个值域<br>`Select * from R Union Select * from S;`<br>`Select * from R Except Select * from S;`<br>`Select * from R Intersect Select * from S;`<br></td>
  </tr>
  <tr>
    <td>-</td>
    <td>差-Except</td>
  </tr>
  <tr>
    <td>∩</td>
    <td>交-Except</td>
  </tr>
  <tr>
    <td>×</td>
    <td>笛卡尔积</td>
    <td>R: n个属性， k1个元组；S: m个属性， k2个元组<br>R×S：（n+m） 列元组的集合<br>行： k1×k2个元组<br>`Select * from R,S;`<br></td>
  </tr>
  <tr>
    <td rowspan="6">关系</td>
    <td>σ</td>
    <td>选择</td>
    <td>从关系R中选取符合条件的元组，<br>`SELECT R.学号，R.课程名, R.分数 from R WHERE 分数&gt;85`</td>
  </tr>
  <tr>
    <td>π </td>
    <td>投影</td>
    <td>选取属性，选取的记过会删除重复的元组<br>`SELECT 品名，数量 FROM R;`</td>
  </tr>
  <tr>
    <td rowspan="3">连接</td>
    <td>θ连接</td>
    <td>从两个关系的笛卡尔积中选取属性间满足一定条件的元组</td>
  </tr>
  <tr>
    <td>自然连接</td>
    <td>从两个关系的笛卡尔积中选取相同属性分量相等的元组</td>
  </tr>
  <tr>
    <td>外连接</td>
    <td>如果把悬浮元组也保存在结果关系中，而在其他属性，上填空值(Null)，就叫做外连接</td>
  </tr>
  <tr>
    <td>÷ </td>
    <td>除</td>
    <td>给定关系R (X， Y) 和S (Y， Z)， 其中X， Y， Z为属性组。R中的Y与S中的Y出自相同的域集。R与S的除运算得到一个新的关系P(X)。其中P(x)与S(Y)组成的元组都在R(X,Y)中<br>`SELECT DISTINCT R.X FROM R  R1<br>WHERE NOT EXISTS <br>(	<br>    SELECT S.Y FROM S <br>    WHERE NOT EXISTS <br>    (<br>        SELECT * FROM R R2 <br>        where R1.X=R2.X and R2.Y=S.Y<br>    )<br>)`</td>
  </tr>
</table>

# [数据定义语言-DDL](DDL-SQL.md)

| 命令   | 描述                                   |
| ------ | -------------------------------------- |
| CREATE | 创建新的表、视图或者其他数据库中的对象 |
| ALTER  | 修改现存数据库对象，比如一张表         |
| DROP   | 删除表、视图或者数据库中的其他对象     |

# [数据操纵语言-DML](./DML-SQL.md)

| 命令   | 描述                             |
| ------ | -------------------------------- |
| INSERT | 创建一条新记录                   |
| UPDATE | 修改记录                         |
| DELETE | 删除记录                         |
| SELECT | 从一张或者多张表中检索特定的数据 |

# [数据控制语言-DCL](./DCL-SQL.md)

| 命令   | 描述               |
| ------ | ------------------ |
| GRANT  | 赋予用户特权       |
| REVOKE | 收回赋予用户的特权 |

