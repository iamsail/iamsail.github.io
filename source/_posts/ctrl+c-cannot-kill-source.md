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

*********************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>