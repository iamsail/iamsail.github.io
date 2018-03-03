---
title: 安装双系统
date: 2017-09-03 13:16:17
categories: 代码人生
---

本文是对安装win10+ubuntu的记录,具体的细节不作介绍，文末有参考链接。

<span class="under0">主要记录我踩的一些坑。</span>

**********

因为一些误操作,电脑只有ubuntu,** 在装win10的时候(先装win10,再装linux),显示界面只有两个磁盘分区0和1,而且还不能操作。**

在[贴吧中找到了解决方案](http://tieba.baidu.com/p/1371438126)

**********
```
以win7光盘安装为例我们可以在安装完系统后分区，也可以在安装时分区，安装程序创建的都是主分区，并没有创建逻辑分区的任何选项，这样的
情况导致创建4个主分区后剩余的空间无法继续分配，用windows的Diskpart命令可以很简单的帮助我们解决这个问题。
Diskpart命令是Windows环境下的一个命令，利用diskpart可实现对硬盘的分区管理，包括创建分区、删除分区、合并（扩展
）分区，而且设置分区后不用重启电脑也能生效。 利用Diskpart命令来分区，既不用借助第三方工具，也不会产生100MB的“系统保留”分区，其次分区操作直接设置即刻生效
，不用重新启动计算机。

以一块98G的盘为例
40G【主分区】+20G+20G+18G【逻辑分区】
在安装windows7过程中，到磁盘分区这一步时停下，按组合键“Shift+10”进入cmd窗口。

输入diskpart 回车即可启动diskpart工具，其提示符为“DISKPART>”。

输入List Disk回车，显示本机所有磁盘，便于操作正确的磁盘。

输入Select Disk 0选择要操作的磁盘

输入Clean 清除已选硬盘上的所有分区。

输入Create Partition Primary Size=40960 在已选硬盘上创建容量为40960MB（即40G——40*1024=40960）的主磁盘分
区。

输入Active 激活当前磁盘分区，即刚分好的主磁盘分区。

输入format quick　快速格式化当前磁盘分区。

输入Create Partition Extended将剩余空间全部划分为扩展磁盘分区。

输入Create Partition Logical Size=20480在扩展磁盘分区上创建容量为20G的逻辑磁盘分区。

输入format quick　快速格式化当前磁盘分区。

输入Create Partition Logical Size=20480 在扩展磁盘分区上创建容量为20G的第二个逻辑磁盘分区

输入Format Quick　快速格式化当前磁盘分区。

输入Create Partition Logical 在扩展磁盘分区上将剩余的磁盘空间创建逻辑磁盘分区。

输入Format Quick　快速格式化当前磁盘分区。

输入Exit 　退出diskpart工具

刷新
```
***********

### ** 安装Ubuntu,空闲分区不可用 **

[主要参考了这篇文章](http://blog.csdn.net/d202x/article/details/53312210)

这篇文章中总结道

（1）先设置  交换空间，\ ，\home(可以不设置)这三个挂载点，都用逻辑分区，最后设置主分区挂载\boot,实在不行所有的都用逻辑分区
（2）如果上一步不行，那就说明你电脑里的硬盘已经有4个主分区了，或者是ubuntu认为你有4个主分区了，而linux系统最多只能有4个主分区，所以这样你就需要重新对电脑进行分盘分区，建议就一个主分区，其他都是逻辑分区，再从逻辑分区分出空闲空间挂载linux系统。

当然这个总结在我安装中并没有起作用,** 我是最后设置的 \ (主分区的挂载),搞定的 **


***********

### ** 丢失MSVCR110.dll **

装完系统,在安装wamp的时候出现了这个错误

** 无法启动此程序，因为计算机中丢失 MSVCR110.dll。尝试重新安装该程序以解决此问题 **

(这里多说一句,如果安装64位的不成功,可以安装32位的。)

这里的这个问题,是需要安装vc库文件,链接在wamp官网安装的时候就有提示,** 关键是把32位和64位的都安装即可。**

**********

### ** MySQL密码设置 **

此外安装完wamp后,mysql密码默认为空,可以像如下这样设置密码

```
mysql -u root

mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('xxxxx');
```
***********

### ** 补充 **

今天是2017年10月4日。昨晚帮两位朋友装了系统,记录一些补充的东西。

在安装的时候选择自己划分区

```
安装的过程中需要涉及到分区，为了以免日后重装，我的建议是如下分区：
1）、5G(20G),主分区,空间起始位置,Ext4日志文件系统,/
2）、内存的大小,逻辑分区,空间起始位置,swap交换空间,无挂载点
3）、200MB,逻辑分区,空间起始位置,Ext4日志文件系统,/boot
4）、剩余的空间,逻辑分区,空间起始位置,Ext4日志文件系统,/home


主分区：ubuntu系统程序区域，包括日后的程序更新，安装软件等。
交换分区：当物理内存不足时，可以取出这部分当做内存使用。
启动分区：linux的grub启动数据区域
用户数据目录：存放个人数据，当然也可以不给，因为ubuntu里面是可以操作windows空间的。


大概是：5G+8G+200M+5G=20G左右

```

***********
### ** 参考 **

[Windows10+Ubuntu双系统安装[多图]](http://www.jianshu.com/p/2eebd6ad284d)
[Ubuntu 16.04与Win10双系统双硬盘安装图解](http://blog.csdn.net/fesdgasdgasdg/article/details/54183577)
[Windows10系统怎么安装,win10系统安装的方法](http://jingyan.baidu.com/article/656db918824e77e381249cac.html)
[windows无法安装到这个硬盘空间。必须安装在ntfs的分区](http://tieba.baidu.com/p/1921063462#25238222438l)
[windows7安装中使用diskpart为硬盘分区](http://tieba.baidu.com/p/1371438126)
[关于解决安装ubuntu双系统中出现的不能识别磁盘分区、空闲空间变不可用问题](http://blog.csdn.net/d202x/article/details/53312210)
[MySQL修改root密码的多种方法](http://www.cnblogs.com/liufei88866/p/5619215.html)
