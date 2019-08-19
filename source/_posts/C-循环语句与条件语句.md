---
title: C++循环语句与条件语句
date: 2017-08-29 16:31:00
tags: [循环语句,条件语句,语言]
categories: C++
---
# 循环语句
循环类型 | 描述
-|-
while 循环 | 当给定条件为真时，重复语句或语句组。它会在执行循环主体之前测试条件。
for 循环 | 多次执行一个语句序列，简化管理循环变量的代码。
[do...while 循环](http://www.runoob.com/cplusplus/cpp-do-while-loop.html) | 除了它是在循环主体结尾测试条件外，其他与 while 语句类似。
嵌套循环 | 您可以在 while、for 或 do..while 循环内使用一个或多个循环。
<!--more-->
## 循环控制语句
控制语句 | 描述
- | -
[break 语句](http://www.runoob.com/cplusplus/cpp-break-statement.html) | 终止 loop 或 switch 语句，程序流将继续执行紧接着 loop 或 switch 的下一条语句。
[continue 语句](http://www.runoob.com/cplusplus/cpp-continue-statement.html) | 引起循环跳过主体的剩余部分，立即重新开始测试条件。
[goto 语句](http://www.runoob.com/cplusplus/cpp-goto-statement.html) | 将控制转移到被标记的语句。但是不建议在程序中使用 goto 语句。


# 判断语句
语句 | 描述
-|-
if 语句 | 一个 if 语句 由一个布尔表达式后跟一个或多个语句组成。
if...else 语句 | 一个 if 语句 后可跟一个可选的 else 语句，else 语句在布尔表达式为假时执行。
嵌套 if 语句 | 您可以在一个 if 或 else if 语句内使用另一个 if 或 else if 语句。
switch 语句 | 一个 switch 语句允许测试一个变量等于多个值时的情况。
嵌套 switch 语句 | 您可以在一个 switch 语句内使用另一个 switch 语句。

## ? : 运算符
```C++
Exp1 ? Exp2 : Exp3;
```
- Exp1为真，则计算Exp2
- Exp1为假，则计算Exp3
