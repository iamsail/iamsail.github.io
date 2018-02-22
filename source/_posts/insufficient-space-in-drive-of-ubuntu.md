---
title: Linux更新磁盘空间不足
date: 2017-10-14 09:18:30
categories: Linux 
---

## ** preface **

** 贴吧真的是大神多啊！ **

**************

## ** 问题 **

Ubuntu提示有些更新,在更新的时候给出如下消息

这个更新需要花去 92.1 M 磁盘上总计 /boot 的空间。请在 19.5 M 磁盘上留出 /boot 空间。清空您的回收站和临时文件，用“sudo apt-get clean”清理以前的安装文件。

但是执行`sudo apt-get clean`并没有什么作用

***************

## ** 解决 **


执行以下命令

`sudo apt-get remove --purge $(dpkg -l 'linux-*' | sed '/^ii/!d;/'"$(uname -r | sed "s/\(.*\)-\([^0-9]\+\)/\1/")"'/d;s/^[^ ]* [^ ]* \([^ ]*\).*/\1/;/[0-9]/!d')`

**<span class="under0"> 除了本机正在使用中的最新内核，删除所有旧内核。</span> **

然后执行

`sudo updategrub`

即可

***************

## ** 参考 **
[磁盘空间不足，怎么办？](http://tieba.baidu.com/p/2813472589)
***************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
