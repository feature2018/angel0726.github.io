---
title: shell
date: 2019-07-30 10:29:25
tags: [操作系统,编程语言]
categories: linux
---



Shell 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。

# 运行脚本

运行 Shell 脚本有两种方法：**1、作为可执行程序**；**2、作为解释器参数**

## 1、作为可执行程序

```shell
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```

## 2、作为解释器参数

```shell
/bin/sh test.sh
/bin/php test.php
```

<!--more-->

# 变量

## 变量名 

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线（_）。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

## 使用变量

```shell
your_name="qinjx"
echo ${your_name}
```

## 只读变量

使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。

```shell
#!/bin/bash
myUrl="http://www.google.com"
readonly myUrl
```

## 删除变量

使用 unset 命令可以删除变量，变量被删除后不能再次使用。unset 命令不能删除只读变量。

```shell
unset variable_name
```

## 变量类型

- **1) 局部变量** 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
- **2) 环境变量** 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
- **3) shell变量** shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

# Shell 字符串

| 符号     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| ‘-单引号 | 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的； |
| “-双引号 | 双引号里可以有变量，双引号里可以添加转义字符                 |



## 拼接字符

```shell
your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

输出

```shell
hello, runoob ! hello, runoob !
hello, runoob ! hello, ${your_name} !
```

## 获取字符串长度

```shell
string="abcd"
echo ${#string} #输出 4
```

## 提取子字符串

```shell
string="runoob is a great site"
echo ${string:1:4} # 输出 unoo
```

## 查找子字符串

```shell
string="runoob is a great site"
echo `expr index "$string" io`  # 输出 4
```

# 数组

bash支持一维数组（不支持多维数组），并且没有限定数组的大小。数组元素的下标由 0 开始编号。获取数组中的元素要利用下标，下标可以是整数或算术表达式，其值应大于或等于 0。

```shell
array_name=(value0 value1 value2 value3)  #定义数组

#### 读取数据
valuen=${array_name[n]}    #读取单个元素
echo ${array_name[@]}      #读取所有元素

#### 数组长度
length=${#array_name[@]}   #取得数组所有元素的个数
lengthn=${#array_name[n]}  #取得数组单个元素的长度
```

# 传递参数

我们可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n**。**n** 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推

| 参数处理 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| $n       | n代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推 |
| $#       | 传递到脚本的参数个数                                         |
| $*       | 以一个单字符串显示所有向脚本传递的参数。 <br>如"\$\*"用「"」括起来的情况、以"\$1 ​\$2 … $n"的形式输出所有参数。 |
| $@       | 与\$*相同，但是使用时加引号，并在引号中返回每个参数。<br> 如"​\$@"用「"」括起来的情况、以"​\$1" "​\$2" … "$n" 的形式输出所有参数。 |
| $$       | 脚本运行的当前进程ID号                                       |
| $!       | 后台运行的最后一个进程的ID号                                 |
| $-       | 显示Shell使用的当前选项，与set命令功能相同。                 |
| $?       | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

**注意**：\$* 与 \$@ 区别：

- 相同点：都是引用所有参数。

- 不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）。

  ```shell
  #!/bin/bash
  # author:菜鸟教程
  # url:www.runoob.com
  
  echo "-- \$* 演示 ---"
  for i in "$*"; do
      echo $i
  done
  
  echo "-- \$@ 演示 ---"
  for i in "$@"; do
      echo $i
  done
  ```

  输出

  ```shell
  $ chmod +x test.sh 
  $ ./test.sh 1 2 3
  -- $* 演示 ---
  1 2 3
  -- $@ 演示 ---
  1
  2
  3
  ```

  

# 运算符

| 运算符 | 说明                                                  | 举例                                      |
| ------ | ----------------------------------------------------- | ----------------------------------------- |
| %      | 取余                                                  | `expr $b % $a` 结果为 0。                 |
| =      | 赋值                                                  | `a=$b` 将把变量 b 的值赋给 a。            |
| ==     | 相等。用于比较两个数字，相同则返回 true。             | `[$a == $b]` 返回 false。                 |
| !=     | 不相等。用于比较两个数字，不相同则返回 true。         | `[$a != $b ]`返回 true。                  |
| -eq    | 检测两个数是否相等，相等返回 true。                   | `[$a -eq $b]` 返回 false。                |
| -ne    | 检测两个数是否不相等，不相等返回 true。               | `[$a -ne $b]` 返回 true。                 |
| -gt    | 检测左边的数是否大于右边的，如果是，则返回 true。     | `[$a -gt $b]` 返回 false。                |
| -lt    | 检测左边的数是否小于右边的，如果是，则返回 true。     | `[$a -lt $b]` 返回 true。                 |
| -ge    | 检测左边的数是否大于等于右边的，如果是，则返回 true。 | `[$a -ge $b]` 返回 false。                |
| -le    | 检测左边的数是否小于等于右边的，如果是，则返回 true。 | `[$a -le $b]` 返回 true。                 |
| !      | 非运算，表达式为 true 则返回 false，否则返回 true。   | `[!false]` 返回 true。                    |
| -o     | 或运算，有一个表达式为 true 则返回 true。             | `[$a -lt 20 -o $b -gt 100]` 返回 true。   |
| -a     | 与运算，两个表达式都为 true 才返回 true。             | `[$a -lt 20 -a $b -gt 100] `返回 false。  |
| &&     | 逻辑的 AND                                            | `[[$a -lt 100 && $b -gt 100]]` 返回 false |
| &#124;&#124; | 逻辑的 OR                                             | `[[\$a -lt 100` &#124;&#124; `$b -gt 100 ]] `返回 true |

```shell
a=10
b=20

if [[ $a -lt 100 && $b -gt 100 ]]
then
   echo "返回 true"
else
   echo "返回 false"
fi
```



## 字符串运算符

| 运算符 | 说明                                      | 举例                       |
| :----- | :---------------------------------------- | :------------------------- |
| =      | 检测两个字符串是否相等，相等返回 true。   | [ $a = $b ] 返回 false。   |
| !=     | 检测两个字符串是否相等，不相等返回 true。 | [ 、$a != $b ] 返回 true。 |
| -z     | 检测字符串长度是否为0，为0返回 true。     | [ -z $a ] 返回 false。     |
| -n     | 检测字符串长度是否为0，不为0返回 true。   | [ -n "$a" ] 返回 true。    |
| $      | 检测字符串是否为空，不为空返回 true。     | [ $a ] 返回 true。         |

## 文件测试运算符

| 操作符  | 说明                                                         | 举例                      |
| :-----: | :----------------------------------------------------------- | :------------------------ |
| -b file | 检测文件是否是块设备文件，如果是，则返回 true。              | [ -b $file ] 返回 false。 |
| -c file | 检测文件是否是字符设备文件，如果是，则返回 true。            | [ -c $file ] 返回 false。 |
| -d file | 检测文件是否是目录，如果是，则返回 true。                    | [ -d $file ] 返回 false。 |
| -f file | 检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。 | [ -f $file ] 返回 true。  |
| -g file | 检测文件是否设置了 SGID 位，如果是，则返回 true。            | [ -g $file ] 返回 false。 |
| -k file | 检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。  | [ -k $file ] 返回 false。 |
| -p file | 检测文件是否是有名管道，如果是，则返回 true。                | [ -p $file ] 返回 false。 |
| -u file | 检测文件是否设置了 SUID 位，如果是，则返回 true。            | [ -u $file ] 返回 false。 |
| -r file | 检测文件是否可读，如果是，则返回 true。                      | [ -r $file ] 返回 true。  |
| -w file | 检测文件是否可写，如果是，则返回 true。                      | [ -w $file ] 返回 true。  |
| -x file | 检测文件是否可执行，如果是，则返回 true。                    | [ -x $file ] 返回 true。  |
| -s file | 检测文件是否为空（文件大小是否大于0），不为空返回 true。     | [ -s $file ] 返回 true。  |
| -e file | 检测文件（包括目录）是否存在，如果是，则返回 true。          | [ -e $file ] 返回 true。  |

# echo命令

| 说明                  | 输入                                                         | 输出                         |
| --------------------- | ------------------------------------------------------------ | ---------------------------- |
| 显示普通字符串        | echo "It is a test"                                          | echo It is a test            |
| 显示转义字符          | echo "\"It is a test\""                                      | "It is a test"               |
| 显示变量              | echo "$name It is a test"                                    | ok It is a test              |
| 显示换行              | echo -e "OK! \n" # -e 开启转义<br>echo "It is a test"        | OK!<br><br>OK!  It is a test |
| 显示不换行            | echo -e "OK! \c" # -e 开启转义 \c 不换行<br>echo "It is a test" | OK! It is a test             |
| 显示结果定向至文件    | echo "It is a test" > myfile                                 |                              |
| 原样输出字符串-单引号 | echo '$name\\"'                                              | $name\"                      |
| 显示命令执行结果      | echo \`date\`                                                | Thu Jul 24 10:08:46 CST 2014 |



# printf

```shell
printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg  
printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234 
printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543 
printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876 
```

- %-10s 指一个宽度为10个字符（-表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。
- %-4.2f 指格式化为小数，其中.2指保留2位小数。

# 转义字符

| 序列  | 说明                                                         |
| :---- | :----------------------------------------------------------- |
| \a    | 警告字符，通常为ASCII的BEL字符                               |
| \b    | 后退                                                         |
| \c    | 抑制（不显示）输出结果中任何结尾的换行字符（只在%b格式指示符控制下的参数字符串中有效），而且，任何留在参数里的字符、任何接下来的参数以及任何留在格式字符串中的字符，都被忽略 |
| \f    | 换页（formfeed）                                             |
| \n    | 换行                                                         |
| \r    | 回车（Carriage return）                                      |
| \t    | 水平制表符                                                   |
| \v    | 垂直制表符                                                   |
| \\    | 一个字面上的反斜杠字符                                       |
| \ddd  | 表示1到3位数八进制值的字符。仅在格式字符串中有效             |
| \0ddd | 表示1到3位的八进制值字符                                     |

# 流程控制

## if else

```shell
if condition
then
    command1 
    command2
    ...
    commandN 
fi
```

## if else-if else

```shell
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

## for循环

```shell
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done

```

## while 语句

```shell
while condition
do
    command
done

```

## until 循环

until 循环执行一系列命令直至条件为 true 时停止。until 循环与 while 循环在处理方式上刚好相反。

```shell
until condition
do
    command
done

```

## case语句

```shell
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2）
    command1
    command2
    ...
    commandN
    ;;
esac

```

## break

跳出所有的循环

## continue

跳出当前循环

# 函数

```shell
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com

funWithParam(){
    echo "第一个参数为 $1 !"
    echo "第二个参数为 $2 !"
    echo "第十个参数为 $10 !"
    echo "第十个参数为 ${10} !"
    echo "第十一个参数为 ${11} !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
funWithParam 1 2 3 4 5 6 7 8 9 34 73

```

输出结果：

```shell
第一个参数为 1 !
第二个参数为 2 !
第十个参数为 10 !
第十个参数为 34 !
第十一个参数为 73 !
参数总数有 11 个!
作为一个字符串输出所有参数 1 2 3 4 5 6 7 8 9 34 73 !

```

| 参数处理 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| $#       | 传递到脚本的参数个数                                         |
| $*       | 以一个单字符串显示所有向脚本传递的参数                       |
| $$       | 脚本运行的当前进程ID号                                       |
| $!       | 后台运行的最后一个进程的ID号                                 |
| $@       | 与$*相同，但是使用时加引号，并在引号中返回每个参数。         |
| $-       | 显示Shell使用的当前选项，与set命令功能相同。                 |
| $?       | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

# Shell 输入/输出重定向

| 命令            | 说明                                                         |
| :-------------- | :----------------------------------------------------------- |
| command > file  | 将输出重定向到 file。任何file内的已经存在的内容将被新内容替代 |
| command < file  | 将输入重定向到 file。本来需要从键盘获取输入的命令会转移到文件读取内容。 |
| command >> file | 将输出以追加的方式重定向到 file。                            |
| n > file        | 将文件描述符为 n 的文件重定向到 file。                       |
| n >> file       | 将文件描述符为 n 的文件以追加的方式重定向到 file。将新内容添加在文件末尾 |
| n >& m          | 将输出文件 m 和 n 合并。                                     |
| n <& m          | 将输入文件 m 和 n 合并。                                     |
| << tag          | 将开始标记 tag 和结束标记 tag 之间的内容作为输入。           |

## 重定向深入讲解

- 标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据。

- 标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据。

- 标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息。

  

```shell
 command >> file 2>&1  #将 stdout 和 stderr 合并后重定向到 file

```

# Shell 文件包含

和其他语言一样，Shell 也可以包含外部脚本。这样可以很方便的封装一些公用的代码作为一个独立的文件。

```shell
. filename   # 注意点号(.)和文件名中间有一空格

或

source filename
```

# 日期

| 命令                                | 说明                  |
| ----------------------------------- | --------------------- |
| `date +%Y%m%d`<br>`$(date +%Y%m%d)` | 获取今天日期          |
| `date -d -2day +%Y%m%d`             | 获取前天日期（2天前） |
| `date -d 2day +%Y%m%d`              | 获取后天日期（2天后） |

| 命令  | 说明                          | 命令  | 说明                                   |
| ----- | ----------------------------- | ----- | -------------------------------------- |
| `%H`  | 小时（00..23）                | `%I ` | 小时（01..12）                         |
| `%k ` | 小时（0..23）                 | `%l ` | 小时（1..12）                          |
| `%M`  | 分（00..59）                  | `%p`  | 显示出AM或PM                           |
| `%r ` | 时间(hh:mm:ss AM或PM)，12小时 | `%s ` | 从1970年1月1日00:00:00到目前经历的秒数 |
| `%S` | 秒（00..59）                  |` %T `  | 时间（24小时制）（hh:mm:ss）      |
| `%X ` | 显示时间的格式（％H:％M:％S） | `%Z `  | 时区 日期域                                |
| `%a`  | 星期几的简称（ Sun..Sat）                  | `%A`   | 星期几的全称（ Sunday..Saturday）          |
| `%b`  | 月的简称（Jan..Dec）                       | `%B`   | 月的全称（January..December）              |
| `%c ` | 日期和时间（ Mon Nov 8 14:12:46 CST 1999） | `%d`   | 一个月的第几天（01..31）                   |
| `%D`  | 日期（mm／dd／yy）                         | `%h`   | 和%b选项相同 |
| `%j`  | 一年的第几天（001..366） | `%m` | 月（01..12） |
| `%w` | 一个星期的第几天（0代表星期天） | `%W` | 一年的第几个星期（00..53，星期一为第一天） |
| `%x` | 显示日期的格式（mm/dd/yy）                 | `%y`   | 年的最后两个数字（ 1999则是99）            |
| `%Y`  | 年（例如：1970，1996等） |       |                                        |

