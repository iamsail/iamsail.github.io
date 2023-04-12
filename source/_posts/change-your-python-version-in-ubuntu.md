---
title: 在ubuntu中修改python版本
date: 2018-04-06 21:21:00
categories: Python
---

### ** Preface **

我们可能需要使用多个python版本,对于管理多个python版本的情况,我所知道的有两种方案：一是[Anaconda](http://www.sail.name/2017/08/11/Anaconda/),二则是通过docker镜像进行管理。

而Ubuntu很多底层采用的是Python2.*,Python3和Python2是互相不兼容的，所以此时不能卸载Python2，需要将默认Python的指向Python3。

*******************

像我系统装有python2.7,python3,python3.5.

首先,移除`/usr/bin` 下面默认的python文件

```shell
sudo rm /usr/bin/python
```

再将需要设置为默认版本的python link到上一步的位置即可,比如我这里是3.5版本

```shell
sudo ln -s /usr/bin/python3.5 /usr/bin/python 
```

*******************

### ** 参考 **

[ubuntu 将python从默认的2.7升级到3.*](https://blog.csdn.net/bvl10101111/article/details/53117504)