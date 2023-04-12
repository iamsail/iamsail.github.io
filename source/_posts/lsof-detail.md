---
title: 详解lsof命令
date: 2021-11-06 21:17:00
categories: Linux
tags: Shell
---

### ** Preface **

本文是对`lsof`命令的一点记录。

要详细的学习某个shell命令，可以参考我之前的博文[《十分钟解决你的shell命令烦恼》](https://www.sail.name/2020/09/19/solve-your-shell-command-troubles-in-ten-minutes/)

******************

### ** 杀死占用某个端口的进程 **

在mac/linux上我们如何杀死占用某个端口的进程，比如3000端口。执行`lsof -i tcp:3000` 或 `lsof -i :3000`，得到以下结果
![1.png](/img/linux/lsof-detail/1.png)
可以看PID(进程标识符)，为94611，执行 `kill 94611`即可。

******************

### ** 输出列含义 **

这里补充下上图`lsof`命令输出的各列的含义。

```
COMMAND: 进程的名称
PID: 进程标识符
USER: 进程所有者
FD: 文件描述符，应用程序通过文件描述符识别该文件
TYPE: 文件类型
DEVICE: 以逗号分隔设备编号(磁盘名称)
SIZE: 文件的大小(bytes)
NODE: 索引节点(文件在磁盘上的标识)
NAME: 打开文件的确切名称
```

#### ** FD(文件描述符列表) **

```
cwd：表示current work dirctory，即：应用程序的当前工作目录，这是该应用程序启动的目录，除非它本身对这个目录进行更改
txt：该类型的文件是程序代码，如应用程序二进制文件本身或共享库，如上列表中显示的 /sbin/init 程序
lnn：library references (AIX);
er：FD information error (see NAME column);
jld：jail directory (FreeBSD);
ltx：shared library text (code and data);
mxx ：hex memory-mapped type number xx.
m86：DOS Merge mapped file;
mem：memory-mapped file;
mmap：memory-mapped device;
pd：parent directory;
rtd：root directory;
tr：kernel trace file (OpenBSD);
v86  VP/ix mapped file;
0：表示标准输出
1：表示标准输入
2：表示标准错误
```

一般在标准输出、标准错误、标准输入后还跟着文件状态模式：

```
u：表示该文件被打开并处于读取/写入模式。
r：表示该文件被打开并处于只读模式。
w：表示该文件被打开并处于。
空格：表示该文件的状态模式为unknow，且没有锁定。
-：表示该文件的状态模式为unknow，且被锁定。
```

#### ** TYPE(文件类型) **

```
REG：文件
DIR：表示目录。
CHR：表示字符类型。
BLK：块设备类型。
UNIX： UNIX 域套接字。
FIFO：先进先出 (FIFO) 队列。
IPv4：网际协议 (IP) 套接字。
```

*****************

### ** lsof常用参数以及实战 **

```
-a：列出打开文件存在的进程；
-c<进程名>：列出指定进程所打开的文件；
-g：列出GID号进程详情；
-d<文件号>：列出占用该文件号的进程；
+d<目录>：列出目录下被打开的文件；
+D<目录>：递归列出目录下被打开的文件；
-n<目录>：列出使用NFS的文件；
-i<条件>：列出符合条件的进程。（4、6、协议、:端口、 @ip ）
-p<进程号>：列出指定进程号所打开的文件；
-u：列出UID号进程详情；
-h：显示帮助信息；
-v：显示版本信息
```

#### ** 查看哪些进程打开了某个文件 **
`lsof /Library/Fonts/Arial.ttf`
![3.png](/img/linux/lsof-detail/3.png)
`lsof /dev/null`
![2.png](/img/linux/lsof-detail/2.png)


#### ** 查看哪些进程打开了某个目录 **
`lsof ~/learn/repo/blog`

#### ** 查看某个进程程序所打开的文件信息 **
`lsof -c mysql`，查看mysql这个进程打开的文件



*****************

### ** 参考链接 **

- [3. lsof 一切皆文件](https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/lsof.html)
- [Linux lsof 命令](https://www.cnblogs.com/sparkdev/p/10271351.html)
- [lsof命令](https://man.linuxde.net/lsof)
- [Mac系统查看端口占用和杀死进程](https://blog.csdn.net/ch717828/article/details/46663595)
- [lsof(8) — Linux manual page](https://man7.org/linux/man-pages/man8/lsof.8.html)







