---
title: Ctrl+C不能结束程序进程
date: 2017-09-03 12:23:00
categories: Developer Tools
---

重装系统了,出现几个bug。其中一个是在git bash中使用ctrl+c不能终止进程。

这就很蛋疼了,在写博客和node相关开发的时候十分不方便

*********************

当然可以手动kill掉对用端口的PID

```
### 列出所有端口的情况
netstat -ano

### 查看被占用端口对应的PID
netstat -aon|findstr "xxxx"

### 终止进程
taskkill (/f ) PID
```
*******************

这个问题的具体原因我还没找出,如果你知道,可以联系我。

后来我试了试cmder,一切正常。

******************

### ** 参考 **

[ windows下taskkill命令简介](http://blog.csdn.net/taozpwater/article/details/19242603)

