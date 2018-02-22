---
title: 重命名Git分支
date: 2017-08-03 15:43:00
categories: Git
---

### ** 前言 **

** 本文是对重命名Git分支名字方法的记录 **

************
### ** 方法 **

#### ** 思路 **

以下讨论均建立在本地分支和远程对应分支名称相同的前提下

<span class="under0">先重命名本地分支,然后删除远程分支,最后重新提交一个远程分支。</span>

重命名本地分支
```
Git branch -m oldBranchName newBranchName

```

删除远程分支

```
git push origin --delete oldBranchName

## 或者

git push origin :oldBranchName

```

提交
```
git push origin newBranchName
```

************

### ** 参考 **

[ git 分支重命名](http://blog.csdn.net/yy20071313/article/details/49930493)
[Git查看、删除、重命名远程分支和tag](https://blog.zengrong.net/post/1746.html)

************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>