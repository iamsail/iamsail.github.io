---
title: linux输出重定向
date: 2018-04-06 23:01:00
categories: Linux
tags: Shell
---

### ** Preface **

本文是对`2>&1`的学习记录.

最初本文的标题就是`2>&1`,限于hexo的限制,变成了现在的样子。

本文主要参考了[Linux里的2>&1究竟是什么](https://blog.csdn.net/GGxiaobai/article/details/53507530)

*******************

### ** 基础概念介绍 **

linux中有三种标准输入输出，分别是 STDIN，STDOUT，STDERR，对应的数字是 0，1，2。

STDIN 是标准输入，默认从键盘读取信息； 
STDOUT 是标准输出，默认将输出结果输出至终端，也就是显示器之类的东西； 
STDERR 是标准的错误信息，默认也会显示在终端上。 
由于STDOUT与STDERR都会默认显示在终端上，为了区分二者的信息，就有了编号的0，1，2的定义，用1表示STDOUT，2表示STDERR。
/dev/null 表示空设备文件


### ** command>/dev/null **

其实这条命令是一个缩写版，对于一个重定向命令，肯定是a > b这种形式，那么command > /dev/null难道是command充当a的角色，/dev/null充当b的角色。这样看起来比较合理，其实一条命令肯定是充当不了a，肯定是command执行产生的输出来充当a，其实就是标准输出stdout。** 所以command > /dev/null相当于执行了command 1 > /dev/null。执行command产生了标准输出stdout(用1表示)，重定向到/dev/null的设备文件中。 **

### ** 2>1, 2>&1 **

2就是标准错误,1是标准输出, 2>1 就是把标准错误重定向标准输出。那么2>1 和 2>&1 有什么区别呢

<span class="under0">** &相当于等效于标准输出 **</span>

在实际应用中,我们肯定是将一个操作的输出进行重定向,大概格式类似这样

`command>a 2>a` , `command>a 2>&1`

等价于

`command 1>a 2>a`(记作A) , `command 1>a 2>&1`(记作B)

<span class="under0">** A、B区别就在于前者只打开一次文件a，后者会打开文件两次,后者并导致stdout被stderr覆盖。&1的含义就可以理解为用标准输出的引用，引用的就是重定向标准输出产生打开的a。**</span>

从IO效率上来讲,A 比 B 的效率更高。





*******************

### ** 参考 **

[Linux里的2>&1究竟是什么](https://blog.csdn.net/GGxiaobai/article/details/53507530)
[linux shell 中的 2>&1 用法说明](https://blog.csdn.net/huangfei711/article/details/51059310)
[linux shell中"2>&1"含义](https://www.cnblogs.com/zhenghongxin/p/7029173.html)
