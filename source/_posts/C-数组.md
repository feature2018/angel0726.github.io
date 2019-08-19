---
title: C++数组
date: 2017-08-29 19:10:45
tags: [变量作用域,语言]
categories: C++
---
# 数组

```C++
type arrayName [ arraySize ];

double balance[5] = {1000.0, 2.0, 3.4, 7.0, 50.0};
```
<!--more-->

# 多维数组
```C++
type name[size1][size2]...[sizeN];

//二维数组
int a[3][4] = {
 {0, 1, 2, 3} ,   /*  初始化索引号为 0 的行 */
 {4, 5, 6, 7} ,   /*  初始化索引号为 1 的行 */
 {8, 9, 10, 11}   /*  初始化索引号为 2 的行 */
};
```

# 指向数组的指针

数组名是一个指向数组中第一个元素的常量指针。balance 是一个指向 &balance[0] 的指针，即数组 balance 的第一个元素的地址。因此，下面的程序片段把 p 赋值为 balance 的第一个元素的地址：
```C++
double *p;
double balance[10];

p = balance;
```
使用数组名作为常量指针是合法的，反之亦然。因此，*(balance + 4) 是一种访问 balance[4] 数据的合法方式。

# 传递数组给函数
## 方式 1
形式参数是一个指针：
```C++
void myFunction(int *param)
{
.
.
.
}
```
## 方式 2
形式参数是一个已定义大小的数组：
```C++
void myFunction(int param[10])
{
.
.
.
}
```
## 方式 3
形式参数是一个未定义大小的数组：
```C++
void myFunction(int param[])
{
.
.
.
}
```

# 从函数返回数组
C++ 不允许返回一个完整的数组作为函数的参数。但是，您可以通过指定不带索引的数组名来返回一个指向数组的指针。

如果您想要从函数返回一个一维数组，您必须声明一个返回指针的函数，如下
```C++
int * myFunction()
{
.
.
.
}
```

## 实例
```C++
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

// 要生成和返回随机数的函数
int * getRandom( )
{
  static int  r[10];

  // 设置种子
  srand( (unsigned)time( NULL ) );
  for (int i = 0; i < 10; ++i)
  {
    r[i] = rand();
    cout << r[i] << endl;
  }

  return r;
}

// 要调用上面定义函数的主函数
int main ()
{
   // 一个指向整数的指针
   int *p;

   p = getRandom();
   for ( int i = 0; i < 10; i++ )
   {
       cout << "*(p + " << i << ") : ";
       cout << *(p + i) << endl;
   }

   return 0;
}
```
