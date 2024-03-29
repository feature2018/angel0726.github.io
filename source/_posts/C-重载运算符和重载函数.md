---
title: C++重载运算符和重载函数
date: 2017-08-29 21:42:15
tags: [指针,语言]
categories: C++
---
- C++ 允许在同一作用域中的某个函数和运算符指定多个定义，分别称为函数重载和运算符重载。
- 重载声明是指一个与之前已经在该作用域内声明过的函数或方法具有相同名称的声明，但是它们的参数列表和定义（实现）不相同。
- 当您调用一个重载函数或重载运算符时，编译器通过把您所使用的参数类型与定义中的参数类型进行比较，决定选用最合适的定义。选择最合适的重载函数或重载运算符的过程，称为重载决策。
<!--mpre-->

# C++ 中的函数重载
在同一个作用域内，可以声明几个功能类似的同名函数，但是这些同名函数的形式参数（指参数的个数、类型或者顺序）必须不同。您不能仅通过返回类型的不同来重载函数。
```C++
#include <iostream>
using namespace std;

class printData
{
   public:
      void print(int i) {
        cout << "整数为: " << i << endl;
      }

      void print(double  f) {
        cout << "浮点数为: " << f << endl;
      }

      void print(char c[]) {
        cout << "字符串为: " << c << endl;
      }
};

int main(void)
{
   printData pd;

   // 输出整数
   pd.print(5);
   // 输出浮点数
   pd.print(500.263);
   // 输出字符串
   char c[] = "Hello C++";
   pd.print(c);

   return 0;
}
```


# C++ 中的运算符重载
重载的运算符是带有特殊名称的函数，函数名是由关键字 operator 和其后要重载的运算符符号构成的。与其他函数一样，重载运算符有一个返回类型和一个参数列表。

## 一元运算符
```C++
#include <iostream>
using namespace std;

class Distance
{
private:
	int feet;             // 0 到无穷
	int inches;           // 0 到 12
public:
	// 所需的构造函数
	Distance(){
		feet = 0;
		inches = 0;
	}
	Distance(int f, int i){
		feet = f;
		inches = i;
	}
	// 显示距离的方法
	void displayDistance()
	{
		cout << "F: " << feet << " I:" << inches << endl;
	}
	// 重载负运算符（ - ）
	Distance operator- ()
	{
		feet = -feet;
		inches = -inches;
		return Distance(feet, inches);
	}
};
int main()
{
	Distance D1(11, 10), D2(-5, 11);

	D1.displayDistance();
	D2.displayDistance();

	-D1;                     // 取相反数
	D1.displayDistance();    // 距离 D1

	-D2;                     // 取相反数
	D2.displayDistance();    // 距离 D2

	return 0;
}
```
- 输出
```C++
F: 11 I:10
F: -5 I:11
F: -11 I:-10
F: 5 I:-11
```

## 二元运算符

```C++
#include <iostream>
using namespace std;

class Box
{
   public:

      double getVolume(void)
      {
         return length * breadth * height;
      }
      void setLength( double len )
      {
          length = len;
      }

      void setBreadth( double bre )
      {
          breadth = bre;
      }

      void setHeight( double hei )
      {
          height = hei;
      }
      // 重载 + 运算符，用于把两个 Box 对象相加
      Box operator+(const Box& b)
      {
         Box box;
         box.length = this->length + b.length;
         box.breadth = this->breadth + b.breadth;
         box.height = this->height + b.height;
         return box;
      }
   private:
      double length;      // 长度
      double breadth;     // 宽度
      double height;      // 高度
};
// 程序的主函数
int main( )
{
   Box Box1;                // 声明 Box1，类型为 Box
   Box Box2;                // 声明 Box2，类型为 Box
   Box Box3;                // 声明 Box3，类型为 Box
   double volume = 0.0;     // 把体积存储在该变量中

   // Box1 详述
   Box1.setLength(6.0);
   Box1.setBreadth(7.0);
   Box1.setHeight(5.0);

   // Box2 详述
   Box2.setLength(12.0);
   Box2.setBreadth(13.0);
   Box2.setHeight(10.0);

   // Box1 的体积
   volume = Box1.getVolume();
   cout << "Volume of Box1 : " << volume <<endl;

   // Box2 的体积
   volume = Box2.getVolume();
   cout << "Volume of Box2 : " << volume <<endl;

   // 把两个对象相加，得到 Box3
   Box3 = Box1 + Box2;

   // Box3 的体积
   volume = Box3.getVolume();
   cout << "Volume of Box3 : " << volume <<endl;

   return 0;
}
```

## 关系运算符重载
```C++
#include <iostream>
using namespace std;

class Distance
{
   private:
      int feet;             // 0 到无穷
      int inches;           // 0 到 12
   public:
      // 所需的构造函数
      Distance(){
         feet = 0;
         inches = 0;
      }
      Distance(int f, int i){
         feet = f;
         inches = i;
      }
      // 显示距离的方法
      void displayDistance()
      {
         cout << "F: " << feet << " I:" << inches <<endl;
      }
      // 重载负运算符（ - ）
      Distance operator- ()
      {
         feet = -feet;
         inches = -inches;
         return Distance(feet, inches);
      }
      // 重载小于运算符（ < ）
      bool operator <(const Distance& d)
      {
         if(feet < d.feet)
         {
            return true;
         }
         if(feet == d.feet && inches < d.inches)
         {
            return true;
         }
         return false;
      }
};
int main()
{
   Distance D1(11, 10), D2(5, 11);

   if( D1 < D2 )
   {
      cout << "D1 is less than D2 " << endl;
   }
   else
   {
      cout << "D2 is less than D1 " << endl;
   }
   return 0;
}
```

## C++ 输入/输出运算符重载
```C++
#include <iostream>
using namespace std;

class Distance
{
private:
	int feet;             // 0 到无穷
	int inches;           // 0 到 12
public:
	// 所需的构造函数
	Distance(){
		feet = 0;
		inches = 0;
	}
	Distance(int f, int i){
		feet = f;
		inches = i;
	}
	friend ostream &operator<<(ostream &output,
		const Distance &D)
	{
		output << "F : " << D.feet << " I : " << D.inches;
		return output;
	}

	friend istream &operator>>(istream  &input, Distance &D)
	{
		input >> D.feet >> D.inches;
		return input;
	}
};
int main()
{
	Distance D1(11, 10), D2(5, 11), D3;

	cout << "Enter the value of object : " << endl;
	cin >> D3;
	cout << "First Distance : " << D1 << endl;
	cout << "Second Distance :" << D2 << endl;
	cout << "Third Distance :" << D3 << endl;

	return 0;
}
```

# 可重载运算符
类别|运算符
-|-
双目算术运算符 | + (加)，-(减)，*(乘)，/(除)，% (取模)
关系运算符 | ==(等于)，!= (不等于)，< (小于)，> (大于>，<=(小于等于)，>=(大于等于)
逻辑运算符 | &#124;&#124;(逻辑或)，&&(逻辑与)，&#124;(逻辑非)
单目运算符 | + (正)，-(负)，*(指针)，&(取地址)
自增自减运算符 | ++(自增)，--(自减)
位运算符 | &#124; (按位或)，& (按位与)，~(按位取反)，^(按位异或),，<< (左移)，>>(右移)
赋值运算符 | =, +=, -=, *=, /= , % = , &=, &#124;=, ^=, <<=, >>=
空间申请与释放 | new, delete, new[ ] , delete[]
其他运算符 | ()(函数调用)，->(成员访问)，,(逗号)，[](下标)



[参考](http://www.runoob.com/cplusplus/cpp-overloading.html)
