---
title: linux子系统-win10
date: 2019-08-05 17:29:40
tags: [操作系统,WSL]
categories: linux
---

# Windows10安装Ubuntu子系统

## 一、开启开发模式

“设置 - 更新和安全 - 针对开发人员”设置页面，选中“开发人员模式”。

![tempsnip](linux子系统-win10/tempsnip.png)

<!--more-->

## 二、启用或关闭Windows功能

![1565005612829](linux子系统-win10/1565005612829.png)

## 三、安装 Linux 子系统

打开 Windows 应用市场，输入 linux 搜索，选择你自己想要的系统版本

![Windows10å®è£Linuxå­ç³»ç»Ubuntu](linux子系统-win10/20171212111834391.jpg)

## 四、zsh

[zsh](https://link.zhihu.com/?target=http%3A//www.zsh.org/)（Z Shell）是一个功能强大的交互式shell脚本命令解释器。它不仅支持bash，还提供一些强大和高效的功能，例如更好的**自动补全**和**纠错**。貌似很好用

```shell
sudo apt-get install zsh     #安装oh-my-zsh首先需要安装zsh
zsh --version                #查看版本号

sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"        #使用curl安装oh-my-zsh
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"   #使用wget安装oh-my-zsh
```

在`vim ~/.bash_profile`中启用zsh，编辑文件，在末尾添加：

```shell
exec zsh
source .zshrc
```

### zsh插件

zsh插件可以分为自带插件与第三方插件。

- 官方插件： 将插件填进`~/.oh-my-zsh/plugins`
- 第三方插件：将插件填进`~/.oh-my-zsh/custom/plugins`

然后在 `~/.zshrc` 配置文件中的 `plugins` 变量中添加对应插件的名称即可，运行`source ~/.zshrc`

1. `z`:自动跳转
2. `colored-man-pages`：手册页高亮
3. `zsh-autosuggestion`：自动补全，可能导致乱码
4. `zsh-syntax-highlighting`:命令高亮 
5. `incr`：代码提示 。将zsh（[自动补全版本](/download/incr-0.2.zsh) 、[非自动补全版本](/download/incr-0.2.1.zsh)）放进`~/.oh-my-zsh/custom/plugins/incr/incr-0.2.zsh`；在`~/.zshrc`文件末尾加入`source ~/.oh-my-zsh/custom/plugins/incr/incr*.zsh
   export LC_ALL=en_US.UTF-8
   export LANG=en_US.UTF-8`

#### 插件说明

## 五、安装配置Cmder命令行终端

访问[cmder.net](https://cmder.net/)，下载mini版本即可

1. 修改启动参数

   修改启动参数填入`bash -cur_console:p`，这样我们直接打开cmder后就可以进入到linux系统了。这种方法一般vim的方向键不可以使用。

   ![img](linux子系统-win10/dff1d38a0f699e19488e71c1ad7ad8805cc.jpg)

   - 或者使用下面的方法对cmder进行修改。

     ![1566527134737](linux子系统-win10/1566527134737.png)

2. 将cmder添加进win10的右键菜单

   1. 右键点击我的电脑--属性--高级系统设置--环境变量--系统变量，**点击新建，变量名设置为：**CMDER_HOME，变量值直接粘贴刚才拷贝的地址，

   2. 然后点击系统变量中的path，点击新建，输入%CMDER_HOME%
      ![tempsnip](linux子系统-win10/tempsnip-1565012471202.png)
   3. 使用管理员权限打开cmder终端运行`Cmder.exe /REGISTER ALL`

# 文件夹互相访问

## win10访问ubuntu

```shell
C:\Users\xxx\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\xxx
```



## ubuntu访问win10

```shell
/mnt/c/Users    # 进入win10的c盘的Users
```

### 可以建立一个win10的快捷方式

```shell
ln -s /mnt/c/Users/xxx ~/win10    建立链接
```

















































