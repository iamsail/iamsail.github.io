---
title: Isb_release
date: 2018-01-06 08:36:00
categories: Linux 
---
`lsb_release`是查看系统版本信息的工具。

类似的有`uname -a`,`cat /proc/version`命令,不过这两个命令是用于打印当前系统相关信息（内核版本号、硬件架构、主机名称和操作系统类型等）。也就是使用该命令只能查看到内核版本,却不知道系统版本。

***************
### ** lsb_release **

检查是否安装了`lsb_release`

```
lsb_release -r
```

安装`lsb_release`
```
yum install -y redhat-lsb
```

查看系统版本

```
lsb_release -a
```

`lsb_release`适用于所有的Linux发行版，包括Redhat、SuSE、Debian…等发行版
***************

### ** 补充 **

其他查看系统版本信息的命令有

`cat /etc/redhat-release`  这种方法只适合Redhat系的Linux

`cat /etc/issue` 此命令也适用于所有的Linux发行版(这个命令,在我自己的服务器测试失败)

***************

`/etc/issue` 和 `/etc/redhat-release`都是系统安装时默认的发行版本信息，通常安装好系统后文件内容不会发生变化。
`lsb_release -a`:FSG（Free Standards Group）组织开发的LSB (Linux Standard Base)标准的一个命令，用来查看linux兼容性的发行版信息。

** 关于`lsb_release -a`和`/etc/issue`显示的发行版本号不同，原因只有一个：系统内核手动升级了。**

***************

### ** 参考 **

[解决-bash: lsb_release: command not found](https://blog.slogra.com/post-338.html)
[（原创）Linux下查看系统版本号信息的方法](http://www.ha97.com/2987.html)
[Linux中 cat /etc/issue 和lsb_release命令显示的结果会不同么](https://zhidao.baidu.com/question/365547310.html)
