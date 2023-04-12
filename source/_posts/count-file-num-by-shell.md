---
title: Shell统计文件数量
date: 2018-12-09 23:06:18
tags: Shell
---
### ** 通过shell统计文件数目 **

统计某文件夹下文件的个数
`ls -l |grep "^-"|wc -l`

统计某文件夹下目录的个数
`ls -l |grep "^ｄ"|wc -l`

统计文件夹下文件的个数，包括子文件夹里的
`ls -lR|grep "^-"|wc -l`

***********************

### ** 文件类型 **

Linux中文件类型只有以下这几种： 
1.-，普通文件。 
2.d，目录文件，d是directory的简写。 
3.l，软连接文件，亦称符号链接文件，s是soft或者symbolic的简写。 
4.b，块文件，是设备文件的一种（还有另一种），b是block的简写。 
5.c，字符文件，也是设备文件的一种（这就是第二种），c是character的文件。 


*****************
### ** 参考 **
[Linux统计某文件夹下文件、文件夹的个数](http://blog.sina.com.cn/s/blog_464f6dba01012vwv.html)
[Linux系统中普通文件和目录文件的区别](https://my.oschina.net/michaelyuanyuan/blog/109147)

