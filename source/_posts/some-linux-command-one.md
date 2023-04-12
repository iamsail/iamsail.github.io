---
title: 一些Linux命令(一)
date: 2017-04-01 21:15:59
categories: Linux
---
** 切换到root权限 **

```
sudo su

```

** 查看系统安装了哪些shell **

```
chsh -l
cat /etc/shells
```

** 切换shell **
```
    chsh -s /bin/
```
** 移动/重命名文件 **

[<code>mv</code>](http://man.linuxde.net/mv)

*********************

** 显示电脑以及操作系统的相关信息 **

[uname](http://man.linuxde.net/uname)

该命令用于打印当前系统相关信息（内核版本号、硬件架构、主机名称和操作系统类型等）

```
-a或--all：显示全部的信息；
-m或--machine：显示电脑类型；
-n或-nodename：显示在网络上的主机名称；
-r或--release：显示操作系统的发行编号；
-s或--sysname：显示操作系统名称；
-v：显示操作系统的版本；
-p或--processor：输出处理器类型或"unknown"；
-i或--hardware-platform：输出硬件平台或"unknown"；
-o或--operating-system：输出操作系统名称；
--help：显示帮助；
--version：显示版本信息。
```

** 正在运行的内核版本 **
```
cat /proc/version
```
** 发行版本信息 **
```
cat /etc/issue
```
*******************

** 检查当前开发的端口 **

```
netstat -an
```

** 重新启动iptables **

```
service iptables restart
```

******************

### ** SELinux **

** 查看现在的支持http的端口有哪些 **

```
semanage port -l|grep http
```

** 为http服务添加新的端xx **

```
semanage port -a -t http_port_t -p tcp 81
```

** 为http服务删除端口xx **


```
semanage port -d -t http_port_t -p tcp 81
```
*******************

** 参考 **
- [Linux命令大全](http://man.linuxde.net/)
- [Centos端口关闭与打开命令](https://yq.aliyun.com/ziliao/56702)\
- [apache2.x修改默认端口后报 Starting httpd: (13)Permission denied: make_sock: could not bind to address](http://blog.csdn.net/bjbs_270/article/details/6948074)
- [ centos下 httpd 进程只有 ipv6的80端口开放，没有 ipv4的端口](http://bbs.chinaunix.net/thread-4147071-1-1.html)
