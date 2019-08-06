---
title: linux命令
date: 2019-07-30 10:59:16
tags: [操作系统，编程语言]
categories: linux
---

# 文件基本属性

## 文件属性说明

对于文件来说，它都有一个特定的所有者，也就是对该文件具有所有权的用户。同时，在Linux系统中，用户是按组分类的，一个用户属于一个或多个组。文件所有者以外的用户又可以分为文件所有者的同组用户和其他用户。**因此，Linux系统按文件所有者、文件所有者同组用户和其他用户来规定了不同的文件访问权限。**

<!--more-->

## 查看文件属性

```shell
ls -l
```

输出

```shell
dr-xr-xr-x   2 root root 4096 Dec 14  2012 bin
dr-xr-xr-x   4 root root 4096 Apr 19  2012 boot
```

| 第一个字符                                                   | 属主                        | 属组                        | 其他用户                    |
| ------------------------------------------------------------ | --------------------------- | --------------------------- | --------------------------- |
| **d**   目录<br>**-**    文件<br>**l**    链接文档(link file)<br>**b**   装置文件里面的可供储存的接口设备(可随机存取装置)<br>**c**   装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)。 | r   读<br>w  写<br>x   执行 | r   读<br>w  写<br>x   执行 | r   读<br>w  写<br>x   执行 |

## 更改文件属性

<table>
  <tr>
    <th>功能</th>
    <th colspan="5">方法</th>
  </tr>
  <tr>
    <td>更改文件属组</td>
    <td colspan="5">chgrp [-R] 属组名 文件名<br>-R：递归更改文件属组，就是在更改某个目录文件的属组时，如果加上-R的参数，那么该目录下的所有文件的属组都会更改。<br></td>
  </tr>
  <tr>
    <td rowspan="2">更改文件属主</td>
    <td colspan="5">chown [–R] 属主名 文件名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`chown bin install.log`</td>
  </tr>
  <tr>
    <td colspan="5">chown [-R] 属主名：属组名 文件名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`chown root:root install.log`</td>
  </tr>
  <tr>
    <td rowspan="4">更改文件属性</td>
    <td colspan="5">Linux文件的基本权限就有九个，分别是owner/group/others三种身份各有自己的read/write/execute权限。</td>
  </tr>
  <tr>
    <td>第一种方式</td>
    <td colspan="4">chmod [-R] xyz 文件或目录<br>-R : 进行递归(recursive)的持续变更，亦即连同次目录下的所有文件都会变更<br>xyz : 就是刚刚提到的数字类型的权限属性<br><br>` chmod 777 test`</td>
  </tr>
  <tr>
    <td rowspan="2">第二种方式</td>
    <td>u&nbsp;&nbsp;&nbsp;属主<br>g&nbsp;&nbsp;&nbsp;同组<br>o&nbsp;&nbsp;&nbsp;其他<br>a&nbsp;&nbsp;&nbsp;所有</td>
    <td>+(加入)<br>-(除去)<br>=(设定)</td>
    <td>r<br>w<br>x</td>
    <td>文件或目录</td>
  </tr>
  <tr>
    <td colspan="4">`chmod u=rwx,g=rx,o=r&nbsp;&nbsp;test` </td>
  </tr>
</table>



# 文件与目录管理

Linux的目录结构为树状结构，最顶级的目录为根目录 /。其他目录通过挂载可以将它们添加到树中，通过解除挂载可以移除它们。

| 命令  | 说明                                                         |
| ----- | ------------------------------------------------------------ |
| ls    | **列出目录**<br>a: 全部的文件，连同隐藏文件（开头为.的文件）<br>-d ：仅列出目录本身，而不是列出目录内的文件数据(常用)<br>-l ：长数据串列出，包含文件的属性与权限等等数据；(常用) |
| cd    | **切换目录**<br># cd ~       # 表示回到自己的家目录，亦即是 /root 这个目录 |
| pwd   | **显示目前的目录**<br>-P ：显示出确实的路径，而非使用连结 (link) 路径。 |
| mkdir | **创建一个新的目录**<br>-m ：配置文件的权限喔！直接配置，不需要看默认权限 (umask) 的脸色～<br/>-p ：帮助你直接将所需要的目录(包含上一级目录)递归创建起来！ |
| rmdir | 删除一个空的目录<br>-p ：连同上一级『空的』目录也一起删除    |
| cp    | **复制文件或目录**<br>-a：相当於 -pdr 的意思，至於 pdr 请参考下列说明；(常用)<br/>-d：若来源档为连结档的属性(link file)，则复制连结档属性而非文件本身；<br/>-f：为强制(force)的意思，若目标文件已经存在且无法开启，则移除后再尝试一次；<br/>-i：若目标档(destination)已经存在时，在覆盖时会先询问动作的进行(常用)<br/>-l：进行硬式连结(hard link)的连结档创建，而非复制文件本身；<br/>-p：连同文件的属性一起复制过去，而非使用默认属性(备份常用)；<br/>-r：递归持续复制，用於目录的复制行为；(常用)<br/>-s：复制成为符号连结档 (symbolic link)，亦即『捷径』文件；<br/>-u：若 destination 比 source 旧才升级 destination ！ |
| rm    | **移除文件或目录**<br>-f ：就是 force 的意思，忽略不存在的文件，不会出现警告信息；<br/>-i ：互动模式，在删除前会询问使用者是否动作<br/>-r ：递归删除啊！最常用在目录的删除了！这是非常危险的选项！！！ |
| mv    | **移动文件与目录，或修改文件与目录的名称**<br>-f ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖；<br/>-i ：若目标文件 (destination) 已经存在时，就会询问是否覆盖！<br/>-u ：若目标文件已经存在，且 source 比较新，才会升级 (update) |

# 用户与用户组

## 用户管理

| 命令    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| useradd | **添加新的用户账号**    `useradd -s /bin/sh -g group –G adm,root gem`<br>`useradd 选项 用户名`<br>-c   comment 指定一段注释性描述。<br/>-d  目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。<br/>-g  用户组 指定用户所属的用户组。<br/>-G 用户组，用户组 指定用户所属的附加组。<br/>-s  Shell文件 指定用户的登录Shell。<br/>-u  用户号 指定用户的用户号，如果同时有-o选项，则可以重复使用其他用户的标识号。 |
| userdel | **删除帐号**   `userdel -r sam`<br>-r：把用户的主目录一起删除 |
| usermod | 修改帐号   `usermod -s /bin/ksh -d /home/z –g developer sam`<br>`usermod 选项 用户名`<br>包括`-c, -d, -m, -g, -G, -s, -u以及-o等`，这些选项的意义与`useradd`命令中的选项一样 |
| passwd  | 用户账号刚创建时没有口令，但是被系统锁定，无法使用，必须为其指定口令后才可以使用，即使是指定空口令。<br>`passwd 选项 用户名`<br>-l 锁定口令，即禁用账号。<br/>-u 口令解锁。<br/>-d 使账号无口令。<br/>-f 强迫用户下次登录时修改口令。 |

## 用户组管理

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对**/etc/group**文件的更新

| 命令     | 方法                                                         |
| -------- | ------------------------------------------------------------ |
| groupadd | **增加一个新的用户组**<br>-g GID 指定新用户组的组标识号（GID）。<br/>-o 一般与-g选项同时使用，表示新用户组的GID可以与系统已有用户组的GID相同。 |
| groupdel | 删除一个已有的用户组                                         |
| groupmod | **修改用户组的属性**<br>-g GID 为用户组指定新的组标识号。<br/>-o 与-g选项同时使用，用户组的新GID可以与系统已有用户组的GID相同。<br/>-n新用户组 将用户组的名字改为新名字 |
| newgrp   | **如果一个用户同时属于多个用户组，那么用户可以在用户组之间切换，以便具有其他用户组的权限。**<br>```newgrp root``` |

## 与用户账号有关的系统文件

完成用户管理的工作有许多种方法，但是每一种方法实际上都是对有关的系统文件进行修改。这些文件包括/etc/passwd, /etc/shadow, /etc/group等。

### 伪用户

这些用户在/etc/passwd文件中也占有一条记录，但是不能登录，因为它们的登录Shell为空。它们的存在主要是方便系统管理，满足相应的系统进程对文件属主的要求。常见的伪用户如下所示：

```shell
伪 用 户 含 义 
bin 拥有可执行的用户命令文件 
sys 拥有系统文件 
adm 拥有帐户文件 
uucp UUCP使用 
lp lp或lpd子系统使用 
nobody NFS使用
```

### 用户管理文件-/etc/passwd

```shell
用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录Shell
root:x:0:0:Superuser:/:
```

|    字段    | 说明                                                         |
| :--------: | ------------------------------------------------------------ |
|    口令    | 虽然这个字段存放的只是用户口令的加密串，不是明文，但是由于/etc/passwd文件对所有用户都可读，所以这仍是一个安全隐患。因此，现在许多Linux   系统（如SVR4）都使用了shadow技术，把真正的加密后的用户口令字存放到/etc/shadow文件中，而在/etc/passwd文件的口令字段中只存放一个特殊的字符，例如“x”或者“*”。 |
| 用户标识号 | 系统内部用它来标识用户，一般情况下它与用户名是一一对应的。如果几个用户名对应的用户标识号是一样的，系统内部将把它们视为同一个用户，但是它们可以有不同的口令、不同的主目录以及不同的登录Shell等 |
|  组标识号  | 记录的是用户所属的用户组。它对应着/etc/group文件中的一条记录。 |
| 注释性描述 | 记录着用户的一些个人情况。例如用户的真实姓名、电话、地址等， |
|   主目录   | 用户的起始工作目录                                           |
| 登陆shell  | 用户登录后，要启动一个进程，负责将用户的操作传给内核，这个进程是用户登录到系统后运行的命令解释器或某个特定的程序，即Shell |

### 用户管理文件-/etc/shadow

由于/etc/passwd文件是所有用户都可读的，如果用户的密码太简单或规律比较明显的话，一台普通的计算机就能够很容易地将它破解，因此对安全性要求较高的Linux系统都把加密后的口令字分离出来，单独存放在一个文件中，这个文件是/etc/shadow文件。有超级用户才拥有该文件读权限，这就保证了用户密码的安全性。

```shell
登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志   root:Dnakfw28zf38w:8764:0:168:7:::
```

| 字段             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| 登录名           | 与/etc/passwd文件中的登录名相一致的用户账号                  |
| 口令             | 存放的是加密后的用户口令字，长度为13个字符。如果为空，则对应用户没有口令，登录时不需要口令；如果含有不属于集合   { ./0-9A-Za-z }中的字符，则对应的用户不能登录。 |
| 最后一次修改时间 | 从某个时刻起，到用户最后一次修改口令时的天数。时间起点对不同的系统可能不一样。例如在SCO   Linux 中，这个时间起点是1970年1月1日。 |
| 最小时间间隔     | 是两次修改口令之间所需的最小天数。                           |
| 最大时间间隔     | 口令保持有效的最大天数。                                     |
| 警告时间         | 从系统开始警告用户到用户密码正式失效之间的天数。             |
| 不活动时间       | 用户没有登录活动但账号仍能保持有效的最大天数。               |
| 失效时间         | 给出的是一个绝对的天数，如果使用了这个字段，那么就给出相应账号的生存期。期满后，该账号就不再是一个合法的账号，也就不能再用来登录了。 |

### 用户组管理文件-/etc/group

每个用户都属于某个用户组；一个组中可以有多个用户，一个用户也可以属于不同的组。当一个用户同时是多个组中的成员时，在/etc/passwd文件中记录的是用户所属的主组，也就是登录时所属的默认组，而其他组称为附加组。用户要访问属于附加组的文件时，必须首先使用newgrp命令使自己成为所要访问的组中的成员。

```shell
组名:口令:组标识号:组内用户列表
root::0:root
```

| 字段         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 组名         | 用户组的名称，由字母或数字构成。与/etc/passwd中的登录名一样，组名不应重复。 |
| 口令存       | 用户组加密后的口令字。一般Linux系统的用户组都没有口令，即这个字段一般为空，或者是*。 |
| 组标识号     | 与用户标识号类似，也是一个整数，被系统内部用来标识组。       |
| 组内用户列表 | 属于这个组的所有用户的列表/b]，不同用户之间用逗号(,)分隔。这个用户组可能是用户的主组，也可能是附加组。 |

## 添加批量用户

1. 先编辑一个文本用户文件。

   每一列按照`/etc/passwd`密码文件的格式书写，要注意每个用户的用户名、UID、宿主目录都不可以相同，其中密码栏可以留做空白或输入x号。一个范例文件user.txt内容如下：

   ```txt
   user001::600:100:user:/home/user001:/bin/bash
   user002::601:100:user:/home/user002:/bin/bash
   user003::602:100:user:/home/user003:/bin/bash
   user004::603:100:user:/home/user004:/bin/bash
   user005::604:100:user:/home/user005:/bin/bash
   user006::605:100:user:/home/user006:/bin/bash
   ```

2. 以root身份执行命令 `/usr/sbin/newusers`，从刚创建的用户文件`user.txt`中导入数据，创建用户

   ```shell
   newusers < user.txt
   ```

3. 执行命令/usr/sbin/pwunconv

   将 `/etc/shadow` 产生的 `shadow` 密码解码，然后回写到 `/etc/passwd` 中，并将`/etc/shadow`的`shadow`密码栏删掉。这是为了方便下一步的密码转换工作，即先取消 `shadow password` 功能。

   ```shell
   pwunconv
   ```

4. 编辑每个用户的密码对照文件。

   ```txt
   user001:密码
   user002:密码
   user003:密码
   user004:密码
   user005:密码
   user006:密码
   ```

5. 以root身份执行命令 `/usr/sbin/chpasswd`

   创建用户密码，`chpasswd` 会将经过 `/usr/bin/passwd` 命令编码过的密码写入 `/etc/passwd` 的密码栏。

   ```shell
   chpasswd < passwd.txt
   ```

6. 确定密码经编码写入/etc/passwd的密码栏后。

   执行命令 `/usr/sbin/pwconv` 将密码编码为 `shadow password`，并将结果写入 `/etc/shadow`。

   ```shell
   pwconv
   ```


# yum 命令-包管理

- yum（ Yellow dog Updater, Modified）是一个在Fedora和RedHat以及SUSE中的Shell前端软件**包管理器**。

- 基於RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以**自动处理依赖性关系**，并且一次安装所有依赖的软体包，无须繁琐地一次次下载、安装。

- yum提供了**查找、安装、删除**某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

```shell
yum [options] [command] [package ...]
```

<table>
  <tr>
    <th>参数</th>
    <th colspan="2">说明</th>
  </tr>
  <tr>
    <td rowspan="3">options</td>
    <td>-h</td>
    <td>帮助</td>
  </tr>
  <tr>
    <td>-y</td>
    <td>当安装过程提示选择全部为"yes"</td>
  </tr>
  <tr>
    <td>-q</td>
    <td>不显示安装的过程</td>
  </tr>
  <tr>
    <td rowspan="11">command</td>
    <td>check-update</td>
    <td>列出所有可更新的软件清单命令</td>
  </tr>
  <tr>
    <td>update</td>
    <td>更新所有软件命令</td>
  </tr>
  <tr>
    <td>update&lt;package_name&gt;</td>
    <td>仅更新指定的软件命令</td>
  </tr>
  <tr>
    <td>install &lt;package_name&gt;</td>
    <td>仅安装指定的软件命令</td>
  </tr>
  <tr>
    <td>list</td>
    <td>列出所有可安裝的软件清单命令</td>
  </tr>
  <tr>
    <td>remove &lt;package_name&gt;</td>
    <td>删除软件包命令</td>
  </tr>
  <tr>
    <td>search <br>&lt;keyword&gt;</td>
    <td>查找软件包命令</td>
  </tr>
  <tr>
    <td>clean packages</td>
    <td>清除缓存目录下的软件包</td>
  </tr>
  <tr>
    <td>clean headers</td>
    <td>清除缓存目录下的 headers</td>
  </tr>
  <tr>
    <td>clean oldheaders</td>
    <td>清除缓存目录下旧的 headers</td>
  </tr>
  <tr>
    <td>clean/clean all</td>
    <td>清除缓存目录下的软件包及旧的headers</td>
  </tr>
  <tr>
    <td>package</td>
    <td colspan="2">操作的对象</td>
  </tr>
</table>



# 命令大全

| **1、文件管理**                                              |                                                              |                                                              |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [cat](http://www.runoob.com/linux/linux-comm-cat.html)       | [chattr](http://www.runoob.com/linux/linux-comm-chattr.html) | [chgrp](http://www.runoob.com/linux/linux-comm-chgrp.html)   | [chmod](http://www.runoob.com/linux/linux-comm-chmod.html)   |
| [chown](http://www.runoob.com/linux/linux-comm-chown.html)   | [cksum](http://www.runoob.com/linux/linux-comm-cksum.html)   | [cmp](http://www.runoob.com/linux/linux-comm-cmp.html)       | [diff](http://www.runoob.com/linux/linux-comm-diff.html)     |
| [diffstat](http://www.runoob.com/linux/linux-comm-diffstat.html) | [file](http://www.runoob.com/linux/linux-comm-file.html)     | [find](http://www.runoob.com/linux/linux-comm-find.html)     | [git](http://www.runoob.com/linux/linux-comm-git.html)       |
| [gitview](http://www.runoob.com/linux/linux-comm-gitview.html) | [indent](http://www.runoob.com/linux/linux-comm-indent.html) | [cut](http://www.runoob.com/linux/linux-comm-cut.html)       | [ln](http://www.runoob.com/linux/linux-comm-ln.html)         |
| [less](http://www.runoob.com/linux/linux-comm-less.html)     | [locate](http://www.runoob.com/linux/linux-comm-locate.html) | [lsattr](http://www.runoob.com/linux/linux-comm-lsattr.html) | [mattrib](http://www.runoob.com/linux/linux-comm-mattrib.html) |
| [mc](http://www.runoob.com/linux/linux-comm-mc.html)         | [mdel](http://www.runoob.com/linux/linux-comm-mdel.html)     | [mdir](http://www.runoob.com/linux/linux-comm-mdir.html)     | [mktemp](http://www.runoob.com/linux/linux-comm-mktemp.html) |
| [more](http://www.runoob.com/linux/linux-comm-more.html)     | [mmove](http://www.runoob.com/linux/linux-comm-mmove.html)   | [mread](http://www.runoob.com/linux/linux-comm-mread.html)   | [mren](http://www.runoob.com/linux/linux-comm-mren.html)     |
| [mtools](http://www.runoob.com/linux/linux-comm-mtools.html) | [mtoolstest](http://www.runoob.com/linux/linux-comm-mtoolstest.html) | [mv](http://www.runoob.com/linux/linux-comm-mv.html)         | [od](http://www.runoob.com/linux/linux-comm-od.html)         |
| [paste](http://www.runoob.com/linux/linux-comm-paste.html)   | [patch](http://www.runoob.com/linux/linux-comm-patch.html)   | [rcp](http://www.runoob.com/linux/linux-comm-rcp.html)       | [rm](http://www.runoob.com/linux/linux-comm-rm.html)         |
| [slocate](http://www.runoob.com/linux/linux-comm-slocate.html) | [split](http://www.runoob.com/linux/linux-comm-split.html)   | [tee](http://www.runoob.com/linux/linux-comm-tee.html)       | [tmpwatch](http://www.runoob.com/linux/linux-comm-tmpwatch.html) |
| [touch](http://www.runoob.com/linux/linux-comm-touch.html)   | [umask](http://www.runoob.com/linux/linux-comm-umask.html)   | [which](http://www.runoob.com/linux/linux-comm-which.html)   | [cp](http://www.runoob.com/linux/linux-comm-cp.html)         |
| [whereis](http://www.runoob.com/linux/linux-comm-whereis.html) | [mcopy](http://www.runoob.com/linux/linux-comm-mcopy.html)   | [mshowfat](http://www.runoob.com/linux/linux-comm-mshowfat.html) | [rhmask](http://www.runoob.com/linux/linux-comm-rhmask.html) |
| [scp](http://www.runoob.com/linux/linux-comm-scp.html)       | [awk](http://www.runoob.com/linux/linux-comm-awk.html)       | [read](http://www.runoob.com/linux/linux-comm-read.html)     | [updatedb](http://www.runoob.com/linux/linux-comm-updatedb.html) |
| **2、文档编辑**                                              |                                                              |                                                              |                                                              |
| [col](http://www.runoob.com/linux/linux-comm-col.html)       | [colrm](http://www.runoob.com/linux/linux-comm-colrm.html)   | [comm](http://www.runoob.com/linux/linux-comm-comm.html)     | [csplit](http://www.runoob.com/linux/linux-comm-csplit.html) |
| [ed](http://www.runoob.com/linux/linux-comm-ed.html)         | [egrep](http://www.runoob.com/linux/linux-comm-egrep.html)   | [ex](http://www.runoob.com/linux/linux-comm-ex.html)         | [fgrep](http://www.runoob.com/linux/linux-comm-fgrep.html)   |
| [fmt](http://www.runoob.com/linux/linux-comm-fmt.html)       | [fold](http://www.runoob.com/linux/linux-comm-fold.html)     | [grep](http://www.runoob.com/linux/linux-comm-grep.html)     | [ispell](http://www.runoob.com/linux/linux-comm-ispell.html) |
| [jed](http://www.runoob.com/linux/linux-comm-jed.html)       | [joe](http://www.runoob.com/linux/linux-comm-joe.html)       | [join](http://www.runoob.com/linux/linux-comm-join.html)     | [look](http://www.runoob.com/linux/linux-comm-look.html)     |
| [mtype](http://www.runoob.com/linux/linux-comm-mtype.html)   | [pico](http://www.runoob.com/linux/linux-comm-pico.html)     | [rgrep](http://www.runoob.com/linux/linux-comm-rgrep.html)   | [sed](http://www.runoob.com/linux/linux-comm-sed.html)       |
| [sort](http://www.runoob.com/linux/linux-comm-sort.html)     | [spell](http://www.runoob.com/linux/linux-comm-spell.html)   | [tr](http://www.runoob.com/linux/linux-comm-tr.html)         | [expr](http://www.runoob.com/linux/linux-comm-expr.html)     |
| [uniq](http://www.runoob.com/linux/linux-comm-uniq.html)     | [wc](http://www.runoob.com/linux/linux-comm-wc.html)         | [let](http://www.runoob.com/linux/linux-comm-let.html)       |                                                              |
| **3、文件传输**                                              |                                                              |                                                              |                                                              |
| [lprm](http://www.runoob.com/linux/linux-comm-lprm.html)     | [lpr](http://www.runoob.com/linux/linux-comm-lpr.html)       | [lpq](http://www.runoob.com/linux/linux-comm-lpq.html)       | [lpd](http://www.runoob.com/linux/linux-comm-lpd.html)       |
| [bye](http://www.runoob.com/linux/linux-comm-bye.html)       | [ftp](http://www.runoob.com/linux/linux-comm-ftp.html)       | [uuto](http://www.runoob.com/linux/linux-comm-uuto.html)     | [uupick](http://www.runoob.com/linux/linux-comm-uupick.html) |
| [uucp](http://www.runoob.com/linux/linux-comm-uucp.html)     | [uucico](http://www.runoob.com/linux/linux-comm-uucico.html) | [tftp](http://www.runoob.com/linux/linux-comm-tftp.html)     | [ncftp](http://www.runoob.com/linux/linux-comm-ncftp.html)   |
| [ftpshut](http://www.runoob.com/linux/linux-comm-ftpshut.html) | [ftpwho](http://www.runoob.com/linux/linux-comm-ftpwho.html) | [ftpcount](http://www.runoob.com/linux/linux-comm-ftpcount.html) |                                                              |
| **4、磁盘管理**                                              |                                                              |                                                              |                                                              |
| [cd](http://www.runoob.com/linux/linux-comm-cd.html)         | [df](http://www.runoob.com/linux/linux-comm-df.html)         | [dirs](http://www.runoob.com/linux/linux-comm-dirs.html)     | [du](http://www.runoob.com/linux/linux-comm-du.html)         |
| [edquota](http://www.runoob.com/linux/linux-comm-edquota.html) | [eject](http://www.runoob.com/linux/linux-comm-eject.html)   | [mcd](http://www.runoob.com/linux/linux-comm-mcd.html)       | [mdeltree](http://www.runoob.com/linux/linux-comm-mdeltree.html) |
| [mdu](http://www.runoob.com/linux/linux-comm-mdu.html)       | [mkdir](http://www.runoob.com/linux/linux-comm-mkdir.html)   | [mlabel](http://www.runoob.com/linux/linux-comm-mlabel.html) | [mmd](http://www.runoob.com/linux/linux-comm-mmd.html)       |
| [mrd](http://www.runoob.com/linux/linux-comm-mrd.html)       | [mzip](http://www.runoob.com/linux/linux-comm-mzip.html)     | [pwd](http://www.runoob.com/linux/linux-comm-pwd.html)       | [quota](http://www.runoob.com/linux/linux-comm-quota.html)   |
| [mount](http://www.runoob.com/linux/linux-comm-mount.html)   | [mmount](http://www.runoob.com/linux/linux-comm-mmount.html) | [rmdir](http://www.runoob.com/linux/linux-comm-rmdir.html)   | [rmt](http://www.runoob.com/linux/linux-comm-rmt.html)       |
| [stat](http://www.runoob.com/linux/linux-comm-stat.html)     | [tree](http://www.runoob.com/linux/linux-comm-tree.html)     | [umount](http://www.runoob.com/linux/linux-comm-umount.html) | [ls](http://www.runoob.com/linux/linux-comm-ls.html)         |
| [quotacheck](http://www.runoob.com/linux/linux-comm-quotacheck.html) | [quotaoff](http://www.runoob.com/linux/linux-comm-quotaoff.html) | [lndir](http://www.runoob.com/linux/linux-comm-lndir.html)   | [repquota](http://www.runoob.com/linux/linux-comm-repquota.html) |
| [quotaon](http://www.runoob.com/linux/linux-comm-quotaon.html) |                                                              |                                                              |                                                              |
| **5、磁盘维护**                                              |                                                              |                                                              |                                                              |
| [badblocks](http://www.runoob.com/linux/linux-comm-badblocks.html) | [cfdisk](http://www.runoob.com/linux/linux-comm-cfdisk.html) | [dd](http://www.runoob.com/linux/linux-comm-dd.html)         | [e2fsck](http://www.runoob.com/linux/linux-comm-e2fsck.html) |
| [ext2ed](http://www.runoob.com/linux/linux-comm-ext2ed.html) | [fsck](http://www.runoob.com/linux/linux-comm-fsck.html)     | [fsck.minix](http://www.runoob.com/linux/linux-comm-fsck-minix.html) | [fsconf](http://www.runoob.com/linux/linux-comm-fsconf.html) |
| [fdformat](http://www.runoob.com/linux/linux-comm-fdformat.html) | [hdparm](http://www.runoob.com/linux/linux-comm-hdparm.html) | [mformat](http://www.runoob.com/linux/linux-comm-mformat.html) | [mkbootdisk](http://www.runoob.com/linux/linux-comm-mkbootdisk.html) |
| [mkdosfs](http://www.runoob.com/linux/linux-comm-mkdosfs.html) | [mke2fs](http://www.runoob.com/linux/linux-comm-mke2fs.html) | [mkfs.ext2](http://www.runoob.com/linux/linux-comm-mkfs-ext2.html) | [mkfs.msdos](http://www.runoob.com/linux/linux-comm-mkfs-msdos.html) |
| [mkinitrd](http://www.runoob.com/linux/linux-comm-mkinitrd.html) | [mkisofs](http://www.runoob.com/linux/linux-comm-mkisofs.html) | [mkswap](http://www.runoob.com/linux/linux-comm-mkswap.html) | [mpartition](http://www.runoob.com/linux/linux-comm-mpartition.html) |
| [swapon](http://www.runoob.com/linux/linux-comm-swapon.html) | [symlinks](http://www.runoob.com/linux/linux-comm-symlinks.html) | [sync](http://www.runoob.com/linux/linux-comm-sync.html)     | [mbadblocks](http://www.runoob.com/linux/linux-comm-mbadblocks.html) |
| [mkfs.minix](http://www.runoob.com/linux/linux-comm-mkfs-minix.html) | [fsck.ext2](http://www.runoob.com/linux/linux-comm-fsck-ext2.html) | [fdisk](http://www.runoob.com/linux/linux-comm-fdisk.html)   | [losetup](http://www.runoob.com/linux/linux-comm-losetup.html) |
| [mkfs](http://www.runoob.com/linux/linux-comm-mkfs.html)     | [sfdisk](http://www.runoob.com/linux/linux-comm-sfdisk.html) | [swapoff](http://www.runoob.com/linux/linux-comm-swapoff.html) |                                                              |
| **6、网络通讯**                                              |                                                              |                                                              |                                                              |
| [apachectl](http://www.runoob.com/linux/linux-comm-apachectl.html) | [arpwatch](http://www.runoob.com/linux/linux-comm-arpwatch.html) | [dip](http://www.runoob.com/linux/linux-comm-dip.html)       | [getty](http://www.runoob.com/linux/linux-comm-getty.html)   |
| [mingetty](http://www.runoob.com/linux/linux-comm-mingetty.html) | [uux](http://www.runoob.com/linux/linux-comm-uux.html)       | [telnet](http://www.runoob.com/linux/linux-comm-telnet.html) | [uulog](http://www.runoob.com/linux/linux-comm-uulog.html)   |
| [uustat](http://www.runoob.com/linux/linux-comm-uustat.html) | [ppp-off](http://www.runoob.com/linux/linux-comm-ppp-off.html) | [netconfig](http://www.runoob.com/linux/linux-comm-netconfig.html) | [nc](http://www.runoob.com/linux/linux-comm-nc.html)         |
| [httpd](http://www.runoob.com/linux/linux-comm-httpd.html)   | [ifconfig](http://www.runoob.com/linux/linux-comm-ifconfig.html) | [minicom](http://www.runoob.com/linux/linux-comm-minicom.html) | [mesg](http://www.runoob.com/linux/linux-comm-mesg.html)     |
| [dnsconf](http://www.runoob.com/linux/linux-comm-dnsconf.html) | [wall](http://www.runoob.com/linux/linux-comm-wall.html)     | [netstat](http://www.runoob.com/linux/linux-comm-netstat.html) | [ping](http://www.runoob.com/linux/linux-comm-ping.html)     |
| [pppstats](http://www.runoob.com/linux/linux-comm-pppstats.html) | [samba](http://www.runoob.com/linux/linux-comm-samba.html)   | [setserial](http://www.runoob.com/linux/linux-comm-setserial.html) | [talk](http://www.runoob.com/linux/linux-comm-talk.html)     |
| [traceroute](http://www.runoob.com/linux/linux-comm-traceroute.html) | [tty](http://www.runoob.com/linux/linux-comm-tty.html)       | [newaliases](http://www.runoob.com/linux/linux-comm-newaliases.html) | [uuname](http://www.runoob.com/linux/linux-comm-uuname.html) |
| [netconf](http://www.runoob.com/linux/linux-comm-netconf.html) | [write](http://www.runoob.com/linux/linux-comm-write.html)   | [statserial](http://www.runoob.com/linux/linux-comm-statserial.html) | [efax](http://www.runoob.com/linux/linux-comm-efax.html)     |
| [pppsetup](http://www.runoob.com/linux/linux-comm-pppsetup.html) | [tcpdump](http://www.runoob.com/linux/linux-comm-tcpdump.html) | [ytalk](http://www.runoob.com/linux/linux-comm-ytalk.html)   | [cu](http://www.runoob.com/linux/linux-comm-cu.html)         |
| [smbd](http://www.runoob.com/linux/linux-comm-smbd.html)     | [testparm](http://www.runoob.com/linux/linux-comm-testparm.html) | [smbclient](http://www.runoob.com/linux/linux-comm-smbclient.html) | [shapecfg](http://www.runoob.com/linux/linux-comm-shapecfg.html) |
| **7、系统管理**                                              |                                                              |                                                              |                                                              |
| [adduser](http://www.runoob.com/linux/linux-comm-adduser.html) | [chfn](http://www.runoob.com/linux/linux-comm-chfn.html)     | [useradd](http://www.runoob.com/linux/linux-comm-useradd.html) | [date](http://www.runoob.com/linux/linux-comm-date.html)     |
| [exit](http://www.runoob.com/linux/linux-comm-exit.html)     | [finger](http://www.runoob.com/linux/linux-comm-finger.html) | [fwhios](http://www.runoob.com/linux/linux-comm-fwhios.html) | [sleep](http://www.runoob.com/linux/linux-comm-sleep.html)   |
| [suspend](http://www.runoob.com/linux/linux-comm-suspend.html) | [groupdel](http://www.runoob.com/linux/linux-comm-groupdel.html) | [groupmod](http://www.runoob.com/linux/linux-comm-groupmod.html) | [halt](http://www.runoob.com/linux/linux-comm-halt.html)     |
| [kill](http://www.runoob.com/linux/linux-comm-kill.html)     | [last](http://www.runoob.com/linux/linux-comm-last.html)     | [lastb](http://www.runoob.com/linux/linux-comm-lastb.html)   | [login](http://www.runoob.com/linux/linux-comm-login.html)   |
| [logname](http://www.runoob.com/linux/linux-comm-logname.html) | [logout](http://www.runoob.com/linux/linux-comm-logout.html) | [ps](http://www.runoob.com/linux/linux-comm-ps.html)         | [nice](http://www.runoob.com/linux/linux-comm-nice.html)     |
| [procinfo](http://www.runoob.com/linux/linux-comm-procinfo.html) | [top](http://www.runoob.com/linux/linux-comm-top.html)       | [pstree](http://www.runoob.com/linux/linux-comm-pstree.html) | [reboot](http://www.runoob.com/linux/linux-comm-reboot.html) |
| [rlogin](http://www.runoob.com/linux/linux-comm-rlogin.html) | [rsh](http://www.runoob.com/linux/linux-comm-rsh.html)       | [sliplogin](http://www.runoob.com/linux/linux-comm-sliplogin.html) | [screen](http://www.runoob.com/linux/linux-comm-screen.html) |
| [shutdown](http://www.runoob.com/linux/linux-comm-shutdown.html) | [rwho](http://www.runoob.com/linux/linux-comm-rwho.html)     | [sudo](http://www.runoob.com/linux/linux-comm-sudo.html)     | [gitps](http://www.runoob.com/linux/linux-comm-gitps.html)   |
| [swatch](http://www.runoob.com/linux/linux-comm-swatch.html) | [tload](http://www.runoob.com/linux/linux-comm-tload.html)   | [logrotate](http://www.runoob.com/linux/linux-comm-logrotate.html) | [uname](http://www.runoob.com/linux/linux-comm-uname.html)   |
| [chsh](http://www.runoob.com/linux/linux-comm-chsh.html)     | [userconf](http://www.runoob.com/linux/linux-comm-userconf.html) | [userdel](http://www.runoob.com/linux/linux-comm-userdel.html) | [usermod](http://www.runoob.com/linux/linux-comm-usermod.html) |
| [vlock](http://www.runoob.com/linux/linux-comm-vlock.html)   | [who](http://www.runoob.com/linux/linux-comm-who.html)       | [whoami](http://www.runoob.com/linux/linux-comm-whoami.html) | [whois](http://www.runoob.com/linux/linux-comm-whois.html)   |
| [newgrp](http://www.runoob.com/linux/linux-comm-newgrp.html) | [renice](http://www.runoob.com/linux/linux-comm-renice.html) | [su](http://www.runoob.com/linux/linux-comm-su.html)         | [skill](http://www.runoob.com/linux/linux-comm-skill.html)   |
| [w](http://www.runoob.com/linux/linux-comm-w.html)           | [id](http://www.runoob.com/linux/linux-comm-id.html)         | [free](http://www.runoob.com/linux/linux-comm-free.html)     |                                                              |
| **8、系统设置**                                              |                                                              |                                                              |                                                              |
| [reset](http://www.runoob.com/linux/linux-comm-reset.html)   | [clear](http://www.runoob.com/linux/linux-comm-clear.html)   | [alias](http://www.runoob.com/linux/linux-comm-alias.html)   | [dircolors](http://www.runoob.com/linux/linux-comm-dircolors.html) |
| [aumix](http://www.runoob.com/linux/linux-comm-aumix.html)   | [bind](http://www.runoob.com/linux/linux-comm-bind.html)     | [chroot](http://www.runoob.com/linux/linux-comm-chroot.html) | [clock](http://www.runoob.com/linux/linux-comm-clock.html)   |
| [crontab](http://www.runoob.com/linux/linux-comm-crontab.html) | [declare](http://www.runoob.com/linux/linux-comm-declare.html) | [depmod](http://www.runoob.com/linux/linux-comm-depmod.html) | [dmesg](http://www.runoob.com/linux/linux-comm-dmesg.html)   |
| [enable](http://www.runoob.com/linux/linux-comm-enable.html) | [eval](http://www.runoob.com/linux/linux-comm-eval.html)     | [export](http://www.runoob.com/linux/linux-comm-export.html) | [pwunconv](http://www.runoob.com/linux/linux-comm-pwunconv.html) |
| [grpconv](http://www.runoob.com/linux/linux-comm-grpconv.html) | [rpm](http://www.runoob.com/linux/linux-comm-rpm.html)       | [insmod](http://www.runoob.com/linux/linux-comm-insmod.html) | [kbdconfig](http://www.runoob.com/linux/linux-comm-kbdconfig.html) |
| [lilo](http://www.runoob.com/linux/linux-comm-lilo.html)     | [liloconfig](http://www.runoob.com/linux/linux-comm-liloconfig.html) | [lsmod](http://www.runoob.com/linux/linux-comm-lsmod.html)   | [minfo](http://www.runoob.com/linux/linux-comm-minfo.html)   |
| [set](http://www.runoob.com/linux/linux-comm-set.html)       | [modprobe](http://www.runoob.com/linux/linux-comm-modprobe.html) | [ntsysv](http://www.runoob.com/linux/linux-comm-ntsysv.html) | [mouseconfig](http://www.runoob.com/linux/linux-comm-mouseconfig.html) |
| [passwd](http://www.runoob.com/linux/linux-comm-passwd.html) | [pwconv](http://www.runoob.com/linux/linux-comm-pwconv.html) | [rdate](http://www.runoob.com/linux/linux-comm-rdate.html)   | [resize](http://www.runoob.com/linux/linux-comm-resize.html) |
| [rmmod](http://www.runoob.com/linux/linux-comm-rmmod.html)   | [grpunconv](http://www.runoob.com/linux/linux-comm-grpunconv.html) | [modinfo](http://www.runoob.com/linux/linux-comm-modinfo.html) | [time](http://www.runoob.com/linux/linux-comm-time.html)     |
| [setup](http://www.runoob.com/linux/linux-comm-setup.html)   | [sndconfig](http://www.runoob.com/linux/linux-comm-sndconfig.html) | [setenv](http://www.runoob.com/linux/linux-comm-setenv.html) | [setconsole](http://www.runoob.com/linux/linux-comm-setconsole.html) |
| [timeconfig](http://www.runoob.com/linux/linux-comm-timeconfig.html) | [ulimit](http://www.runoob.com/linux/linux-comm-ulimit.html) | [unset](http://www.runoob.com/linux/linux-comm-unset.html)   | [chkconfig](http://www.runoob.com/linux/linux-comm-chkconfig.html) |
| [apmd](http://www.runoob.com/linux/linux-comm-apmd.html)     | [hwclock](http://www.runoob.com/linux/linux-comm-hwclock.html) | [mkkickstart](http://www.runoob.com/linux/linux-comm-mkkickstart.html) | [fbset](http://www.runoob.com/linux/linux-comm-fbset.html)   |
| [unalias](http://www.runoob.com/linux/linux-comm-unalias.html) | [SVGATextMode](http://www.runoob.com/linux/linux-comm-svgatextmode.html) |                                                              |                                                              |
| **9、备份压缩**                                              |                                                              |                                                              |                                                              |
| [ar](http://www.runoob.com/linux/linux-comm-ar.html)         | [bunzip2](http://www.runoob.com/linux/linux-comm-bunzip2.html) | [bzip2](http://www.runoob.com/linux/linux-comm-bzip2.html)   | [bzip2recover](http://www.runoob.com/linux/linux-comm-bzip2recover.html) |
| [gunzip](http://www.runoob.com/linux/linux-comm-gunzip.html) | [unarj](http://www.runoob.com/linux/linux-comm-unarj.html)   | [compress](http://www.runoob.com/linux/linux-comm-compress.html) | [cpio](http://www.runoob.com/linux/linux-comm-cpio.html)     |
| [dump](http://www.runoob.com/linux/linux-comm-dump.html)     | [uuencode](http://www.runoob.com/linux/linux-comm-uuencode.html) | [gzexe](http://www.runoob.com/linux/linux-comm-gzexe.html)   | [gzip](http://www.runoob.com/linux/linux-comm-gzip.html)     |
| [lha](http://www.runoob.com/linux/linux-comm-lha.html)       | [restore](http://www.runoob.com/linux/linux-comm-restore.html) | [tar](http://www.runoob.com/linux/linux-comm-tar.html)       | [uudecode](http://www.runoob.com/linux/linux-comm-uudecode.html) |
| [unzip](http://www.runoob.com/linux/linux-comm-unzip.html)   | [zip](http://www.runoob.com/linux/linux-comm-zip.html)       | [zipinfo](http://www.runoob.com/linux/linux-comm-zipinfo.html) |                                                              |
| **10、设备管理**                                             |                                                              |                                                              |                                                              |
| [setleds](http://www.runoob.com/linux/linux-comm-setleds.html) | [loadkeys](http://www.runoob.com/linux/linux-comm-loadkeys.html) | [rdev](http://www.runoob.com/linux/linux-comm-rdev.html)     | [dumpkeys](http://www.runoob.com/linux/linux-comm-dumpkeys.html) |
| [MAKEDEV](http://www.runoob.com/linux/linux-comm-makedev.html) |                                                              |                                                              |                                                              |