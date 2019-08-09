---
title: DML-SQL
date: 2019-07-31 21:07:59
tags: [数据库,编程语言]
categories: SQL
permalink: SQL/DML-SQL.md
---

| 命令     | 作用     |
| -------- | -------- |
| `insert` | 插入语句 |
| `UPDATE` | 更新语句 |
| `DELETE` | 删除语句 |

<!--more-->

# 增、删、改

```sql
-- 插入语句
Insert Into Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
Insert Into St (S#, Sname, avgScore)
            Select S#, Sname, Avg(Score) From Student, SC
            Where Student.S# = SC.S#
            Group by Student.S# ;
-- 更新语句-UPDATE  修改某一行数据
UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing' WHERE LastName = 'Wilson'

-- 删除语句-DELETE
DELETE FROM Person WHERE LastName = 'Wilson'        --删除行名为Wilson
```

# 查询语句

```sql
select expr,列名 as 列的别名,function(列名) as 列的别名
from 表名 as 表的别名
where 条件(对每一个元组进行过滤)
group by 列名(分组) having 对每一组进行过滤
Order by 列名 [asc|desc] 
```

<table>
  <tr>
    <th>命令</th>
    <th>关键字</th>
    <th colspan="2">说明</th>
  </tr>
  <tr>
    <td rowspan="16">select</td>
    <td>expr</td>
    <td colspan="2">常量</td>
  </tr>
  <tr>
    <td>when case</td>
    <td colspan="2">select when st.score&gt;90 then 1<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;when st.score&lt;60 then 0<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;else 0<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;end label</td>
  </tr>
  <tr>
    <td rowspan="14">function</td>
    <td>count</td>
    <td>求个数</td>
  </tr>
  <tr>
    <td>sum</td>
    <td>求和</td>
  </tr>
  <tr>
    <td>avg</td>
    <td>求平均</td>
  </tr>
  <tr>
    <td>max</td>
    <td>求最大</td>
  </tr>
  <tr>
    <td>min</td>
    <td>求最小</td>
  </tr>
  <tr>
    <td>first</td>
    <td>返回列中第一个记录的值</td>
  </tr>
  <tr>
    <td>last </td>
    <td>返回列中最后一个记录的值</td>
  </tr>
  <tr>
    <td>UCASE</td>
    <td>把字段的值转换为大写</td>
  </tr>
  <tr>
    <td>LCASE</td>
    <td>把字段的值转换为小写</td>
  </tr>
  <tr>
    <td>MID</td>
    <td>从文本字段中提取字符<br>SELECT MID(column_name,start[,length]) FROM table_name;<br>column_name：必需。要提取字符的字段。<br>Start：必需。规定开始位置（起始值是 1）。<br>Length：可选。要返回的字符数。如果省略，则 MID() 函数返回剩余文本。<br></td>
  </tr>
  <tr>
    <td>LEN</td>
    <td>函数返回文本字段中值的长度</td>
  </tr>
  <tr>
    <td>ROUND</td>
    <td>函数用于把数值字段舍入为指定的小数位数。<br>SELECT ROUND(column_name,decimals) FROM table_name;<br>column_name 必需。要舍入的字段。<br>decimals 必需。规定要返回的小数位数。</td>
  </tr>
  <tr>
    <td>NOW</td>
    <td>函数返回当前系统的日期和时间</td>
  </tr>
  <tr>
    <td>FORMAT</td>
    <td>FORMAT 函数用于对字段的显示进行格式化。<br><br><br>SELECT ProductName, UnitPrice, FORMAT(Now(),'YYYY-MM-DD') as PerDate<br>FROM Products<br></td>
  </tr>
  <tr>
    <td rowspan="5">from</td>
    <td>原理</td>
    <td colspan="2">从表格中选取数据，采用<span style="font-weight:bold">笛卡尔积</span></td>
  </tr>
  <tr>
    <td rowspan="4">join连接</td>
    <td>join on<br>inner join on</td>
    <td>INNER JOIN 与 JOIN 是相同的<br>不保留空值</td>
  </tr>
  <tr>
    <td>Left join on</td>
    <td>保留左表中所有的数据，右表中不能匹配的数据使用空值填充</td>
  </tr>
  <tr>
    <td>Right join on</td>
    <td>保留右表中所有的数据，左表中不能匹配的数据使用空值填充</td>
  </tr>
  <tr>
    <td>Full join on</td>
    <td>保留两个表中所有的数据，，两个表中不能匹配的数据使用空值填充</td>
  </tr>
  <tr>
    <td rowspan="8">where</td>
    <td>运算符</td>
    <td colspan="2">=、&lt;&gt;、&gt;、&lt;、&gt;=、&lt;=</td>
  </tr>
  <tr>
    <td rowspan="7">函数</td>
    <td>between</td>
    <td>BETWEEN ... AND 会选取介于两个值之间的数据范围。这些值可以是数值、文本或者日期</td>
  </tr>
  <tr>
    <td rowspan="5">like</td>
    <td>"%" : 可以匹配0个或者多个字符 <br></td>
  </tr>
  <tr>
    <td>“ _ ” :只可以匹配一个字符 <br></td>
  </tr>
  <tr>
    <td>“\” : 转义字符，用于去掉一些特殊字符 ，使其变为普通字符。比如用"\%"可以去匹配字符%,而“”是去匹配字符“_”.<br></td>
  </tr>
  <tr>
    <td>[charlist]：字符列中的任何单一字符</td>
  </tr>
  <tr>
    <td>[^charlist]或者[!charlist]：不在字符列中的任何单一字符</td>
  </tr>
  <tr>
    <td>in = exists</td>
    <td>是否存在</td>
  </tr>
  <tr>
    <td>group by</td>
    <td>列名</td>
    <td colspan="2">分组计算</td>
  </tr>
  <tr>
    <td rowspan="2">having</td>
    <td rowspan="2">条件</td>
    <td>函数</td>
    <td>count、sum、avg、max、min、first、last、UCASE、LCASE、MID、LEN、ROUND、NOW、FORMAT</td>
  </tr>
  <tr>
    <td>运算符</td>
    <td>=、&lt;&gt;、&gt;、&lt;、&gt;=、&lt;=；like；in = exists</td>
  </tr>
</table>

# 关系代数操作

```sql
-- 并：求学过002号课的同学或学过003号课的同学学号
Select S# From SC Where C# = ‘002’
UNION [ALL]     --使用ALL命令之后会保留所有重复的元组
Select S# From SC Where C# = ‘003’;

-- 交：求既学过002号课，又学过003号课的同学学号
Select S# From SC Where C# = ‘002’
INTERSECT
Select S# From SC Where C# = ‘003’;

-- 差：假定所有学生都有选课，求没学过002号课程的学生学号
Select DISTINCT S# From SC
EXCEPT
Select S# From SC Where C# = ‘002’;
```

