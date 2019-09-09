---
title: ssh
date: 2019-09-03 17:49:28
tags: [git,分布式]
categories: 远程登陆
---

# 远程登陆服务器

## shell脚本远程自动登陆服务器

目前远程登陆服务器一般需要1. 登陆跳板机；2. 登陆服务器。

1. ssh跳板机->输入静态密码+token码
2. 在跳板机ssh服务器->输入密码

### 解决方法

```shell
sudo apt-get install expect   #安装expect
```

在expect中写入，不同公司的登陆流程不一样，需要修改登陆流程。但是登陆模板如图所示。其中`set`是设置变量；`expect`是设置返回的字符串；`send`是发送的字符串。

```shell
#!/usr/bin/expect

set salt [lindex $argv 0]   #跳板机的token码
set username 跳板机地址
set password 跳板机静态密码
set serverIP 服务器IP地址
set server 服务器地址
set serverpass  服务器密码
spawn ssh "$username"
expect {
    "*yes/no*" {            #如果遇到yes/no输入yes
        send "yes\n";
        exp_continue;
    }
    "*Password:" {          #如果遇到Password
        send "$password $salt\n";    #静态密码+' '+token密码
        exp_continue;
    }
    "Please input server keyword" {  #输入服务器IP地址
        send $serverIP;
        exp_continue;
    }
    "Select account" {               #选择账户
        send "powerop\r";
        exp_continue;
    }
    "server" {                       #从跳板机ssh服务器    
        send "ssh $server\r";
        exp_continue;
    }
    "*password:" {                   #输入服务器密码
        send "$serverpass\r";
        exp_continue;
    }
}
interact
```

