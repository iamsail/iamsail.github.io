---
title: Ubuntu中的拼音问题
date: 2017-02-28 23:16:17
categories: Linux
---
** 先分享两个资源[工具] **
- [Linux命令大全](http://man.linuxde.net/)
- [linuxde.net](http://www.linuxde.net)

****************

今天在Ubuntu,发现打汉字有问题,例如，输入gong却会出现guoneng

![pinying.png](/img/linux/pinying.png)

#### 解决办法
- [参考](http://www.xitongzhijia.net/xtjc/20160229/68044.html)
- 在终端输入ibus-daemon -drx 即可
- 解决完毕

