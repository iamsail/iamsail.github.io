---
title: CMD命令
date: 2017-11-28 21:43:00
categories: CMD
---

### ** Preface **

本文是对自己用到的不熟悉的CMD命令的整理。虽然用到CMD的时候很少,毕竟windows下有cmder这种利器,大部分开发都在linux。

***************

### ** 删除文件夹 **

`rd directoryName`

`rd`的另外一个写法是`rmdir`,源自ReMakeDirectory。它支持带路径的文件夹名，例如：`rd d:\test`。

倘若删除目录下有其他文件,即被删除目录为非空目录,需要加上`/s`参数,如下

`rd /s test`

删除目录时,系统会询问 是否确认(Y/N)?

加上`/q`【quiet】(安静模式)参数,即可。如下

`rd /q /s test`
***************
### ** 参考 **

[cmd rd命令 删除文件夹](http://www.jb51.net/article/18985.htm)

