---
title: C++结构体
date: 2017-08-29 21:28:32
tags: [结构体,语言]
categories: C++
---
# 结构体声明
```c++
struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在学习小组
    float score;  //成绩
} stu1, stu2;            //stu1与stu2为结构体变量

//给结构体成员赋值
    stu1.name = "Tom";
    stu1.num = 12;
    stu1.age = 18;
    stu1.group = 'A';
    stu1.score = 136.5;
```
<!--more-->
# 结构体数组
```c++
#include <stdio.h>

struct{
	char *name;  //姓名
	int num;  //学号
	int age;  //年龄
	char group;  //所在小组
	float score;  //成绩
}class1[] = {
	{ "Li ping", 5, 18, 'C', 145.0 },
	{ "Zhang ping", 4, 19, 'A', 130.5 },
	{ "He fang", 1, 18, 'A', 148.5 },
	{ "Cheng ling", 2, 17, 'F', 139.0 },
	{ "Wang ming", 3, 17, 'B', 144.5 }
};

int main(){
	int i, num_140 = 0;
	float sum = 0;
	for (i = 0; i<5; i++){
		sum += class1[i].score;
		if (class1[i].score < 140) num_140++;
	}
	printf("sum=%.2f\naverage=%.2f\nnum_140=%d\n", sum, sum / 5, num_140);
	for (i = 0; i<5; i++){
		cout << "name:" << class1[i].name << endl;
	}
	return 0;
}
```
- 输出
```C++
sum=707.50
average=141.50
num_140=2
name:Li ping
name:Zhang ping
name:He fang
name:Cheng ling
name:Wang ming
```
# 结构体枚举数据类型
```c++
enum week{ Mon, Tues, Wed, Thurs, Fri, Sat, Sun };   //枚举值默认从 0 开始，往后逐个加 1（递增）；也就是说，week 中的 Mon、Tues ...... Sun 对应的值分别为 0、1 ...... 6。
```

# 结构体作为函数参数
```c++
struct Books
{
  char  title[50];
  char  author[50];
  char  subject[100];
  int  book_id;
};

void printBook( struct Books book )
{
  printf( "Book title : %s\n", book.title);
  printf( "Book author : %s\n", book.author);
  printf( "Book subject : %s\n", book.subject);
  printf( "Book book_id : %d\n", book.book_id);
}
```
# 指向结构的指针
为了使用指向该结构的指针访问结构的成员，您必须使用 -> 运算符
```c++
struct Books *struct_pointer;
struct_pointer = &Book1;
struct_pointer->title;   //为了使用指向该结构的指针访问结构的成员，您必须使用 -> 运算符
```
