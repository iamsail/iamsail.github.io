---
title: 解决冲突
date: 2017-03-16 22:47:27
categories: Git
---

今天在[coalball](https://github.com/iamsail/coalball) merge其他开发人员的commit的时候，出现了冲突。

挑部分记录下。

比如执行命令

    git diff

查看冲突如图

![resolve-conflict.jpg](/img/git/resolve-conflict.jpg)


从图中我们可以看到

    <<<<<<<<<< HEAD

        #########

    ===========

        %%%%%%%%

    >>>>>>>>>>

如何知道哪些是我们自己的代码，哪些是别人提交的呢。

以===========为分界线

因为HEAD指向的就是当前分支,所以

上面部分是我们自己的代码,即<code>#########</code>
下面部分是别人提交的代码,即<code>%%%%%%%%%</code>

***************************

然后根据自己的实际情况，修改冲突就ok了。

vim中dd删除当前行,ndd删除n行。

更多的vim操作自行百度0.0

**************

<div width="100%" align="center"><div name="dashmain" id="dash-main-id-87905c" class="dash-main-2 87905c-3"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>




