---
title: linux软件安装原理
date: 2019-09-26 14:20:47
tags: [操作系统，编程语言]
categories: linux
---

在linux下所有的东西都是以“文件”的形式表示的，那些可以运行的程序有2种，

- 脚本文件，脚本文件由解释程序执行，一般有shell脚本、perl脚本、python脚本等等。

- 二进制文件，也就是经过编译器编译、联接形成的只有0和1组成的文件（计算机只运行0和1组成的程序），c、java等程序都是这种程序。

因此，**只要某个程序所需要的全部“文件”都存在于正确的位置上，那么这个程序就可以运行。**（这个现象在windows下是不全部适用的，如果你复制某个缺少的文件到windows的系统目录，并不一定能使你需要的程序运行起来。）对程序而言，还有一些是以纯文本形式存在的配置文件，用户可以通过定制配置文件来控制程序的运行结果等等。

<!--more-->

| 安装方式                                       | 说明                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| 源码包-》需要编译成二进制文件                  | **优点：**开源，如果有足够的能力，**可以修改源代码**；<br/>&emsp;&emsp;&emsp;可以自由选择所需的功能；<br/>&emsp;&emsp;&emsp;**软件是编译安装，所以更加适合自己的系统，更加稳定、效率更高；**<br>&emsp;&emsp;&emsp;卸载方便<br>**缺点：**安装过程步骤较多，尤其安装较大的软件集合时（如`LAMP`环境搭建），容易出现拼写错误；<br/>&emsp;&emsp;&emsp;编译过程时间较长，安装比二进制安装时间长；<br/>&emsp;&emsp;&emsp;因为是编译安装，安装过程中一旦报错新手很难解决； |
| 二进制包（`RPM`包-->Red Hat、.deb包-->Debian） | **优点：**包管理系统简单，只通过几个命令就可以实现包的安装、升级、查询和卸载<br>&emsp;&emsp;&emsp;安装速度比源码包快<br>**缺点：**经过编译，不再可以看到源代码；<br>&emsp;&emsp;&emsp;功能选择不如源码包灵活；<br>&emsp;&emsp;&emsp;依赖性 |
| yum、apt-get在线安装                           | 可以方便的解决`RPM`安装依赖文件，一条命令就可以帮用户从网上（本地也可以）找到安装包进行安装。 |
| 脚本安装包                                     | 所谓的脚本安装包如：`lnmp/lamp` [LNMP一键安装包](https://lnmp.org/)，就是**把复杂的软件包安装过程写成了程序脚本**，初学者可以执行脚本实现一键安装。但**实际安装的还是**`源码包和二进制包` |



# 源码包安装

## 安装位置

- 源码保存位置：`/usr/local/src`
- 软件安装位置：`/usr/local`

## 安装步骤

### 环境准备


1. 由于源码都是`c`语言写的，所以要先安装`c`语言编译器：`gcc`

2. 确保`gcc`编译器安装成功

   ```shell
   gcc -v # 是否能打印你使用gcc版本信息
   ```

3. 下载源码包，解压

   ```shell
   http://mirror.bit.edu.cn/apache/httpd/  #下载apache2
   tar -zvxf httpd-2.2.31.tar.gz           #解压apache2
   cp .. /usr/local/src                    #将源代码保存到/usr/local/src目录
   ```

### 安装

4. 在源码包目录，执行`./configure`，配置安装程序

   执行`./configure`命令，该命令用于软件配置与检查（基本上每个源码包都会有该命令，即使个别的没有该命令，也会提供相关替代命令）

   - 定义需要的功能选项；

   - 检测系统环境是否符合安装要求；

   - 把第一项中定义好的功能选项和第二项中检测系统环境的信息都写入`Makefile`文件，用于后续的编辑。（后续的【`make`】和【`make install`】命令都会依赖该文件）

   执行命令`./configure --prefix=/usr/local/apache2`，该命令用于指定安装位置为：`/usr/local/apache2`（其中的`apache2`目录不需要提前创建，`make install`命令执行时会自动创建）。命令执行后，会在当前目录生成`Makefile`文件。在用源码包进行安装时，**最好指定路径，因为如果指定路径只要删除/usr/local/XXX就可以了；如果不指定路径，此时程序的文件将保存在/usr/local/bin、/use/local/etc等文件夹中，卸载较麻烦**

5. 执行`make depend`**命令检查依赖库**

6. 执行`make`**编译源码**

7. 执行`make install`命令，**安装程序**，此时会创建`/usr/local/apache2`目录

# RPM命令管理（包依赖很难解决）

 rpm 只能安装已经下载到本地机器上的rpm 包。RPM包命名规则如下：

```shell
#软件包名-软件版本-软件发布的次数-适合的`Linux`平台-适合的硬件平台-包扩展名
httpd-2.2.15-15.el6.centsos.1.i686.rpm
#httpd软件包名-2.2.15软件版本-15发布的次数-el6.centos适合的Linux平台-i686适应的硬件平台-rpm包扩展名,el6是redhat的企业版
```

## RPM 包默认安装位置

| 目录            | 说明                       |
| --------------- | -------------------------- |
| /etc/           | 配置文件安装目录           |
| /usr/bin/       | 可执行的命令安装目录       |
| /usr/lib/       | 程序所使用的函数库保存位置 |
| /usr/share/doc/ | 基本的软件使用手册保存位置 |
| /usr/share/man/ | 帮助文件保存位置           |

# yum在线安装

将所有软件包放到官方服务器上，当进行`yum`在线安装时，可以**自动解决依赖性问题**。（**rpm缺点**：安装过程中，`rpm`包依赖性太强）。

| 命令             | 说明                                      |
| ---------------- | ----------------------------------------- |
| `yun list`       | 查询所有可用软件包列表                    |
| `yum search`     | 关键字 --搜索服务器上所有和关键字相关的包 |
| `yum -y install` | `-y` 自动回答`yes`                        |
| `yum -y update`  | 升级                                      |
| `yum -y remove`  | 卸载                                      |

# 脚本安装



# 安装路径说明

## /usr和/usr/local目录

- 在传统的unix系统中，/usr通常只包含系统发行时自带的程序，而/usr/local则是本地系统管理员用来自由添加程序的目录。（这样可能在升级新版系统或新distribution时无须重新安装全部程序. ）

- 对于Linux发行版，如 RedHat， Debian 等等，**一个可能的规定是：**/usr目录只能由发行版的软件包管理工具负责管理，而对/usr/local却没有这样做。正是因为采用这种方式，软件包管理工具的数据库才能知道在/usr目录内的每一个文件。

## /bin,/sbin,/usr/sbin,/usr/bin 

- **/sbin** 一般是指超级用户指令。主要放置一些系统管理的必备命令例如:cfdisk、dhcpcd、dump、e2fsck、fdisk、halt、ifconfig、ifup、 ifdown、init、insmod、lilo、lsmod、mke2fs、modprobe、quotacheck、reboot、rmmod、 runlevel、shutdown等。

- **/bin** 超级用户和一般的用户都可以使用。。bin为binary的简写主要放置一些普通命令例如:cat、cp、chmod df、dmesg、gzip、kill、ls、mkdir、more、mount、rm、su、tar等。

- **/usr/bin**　是你在后期安装的一些软件的运行脚本。主要放置一些应用软件工具的必备命令例如c++、g++、gcc、chdrv、diff、dig、du、eject、elm、free、gnome*、 gzip、htpasswd、kfm、ktop、last、less、locale、m4、make、man、mcopy、ncftp、 newaliases、nslookup passwd、quota、smb*、wget等。

- **/usr/sbin** 放置一些用户安装的系统管理的命令例如:dhcpd、httpd、imap、in.*d、inetd、lpd、named、netconfig、nmbd、samba、sendmail、squid、swap、tcpd、tcpdump等。

## opt目录

/opt这个目录是一些大型软件的安装目录，或者是一些服务程序的安装目录，当不使用时，直接删除目录就可以了

