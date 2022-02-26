---
title: github提交的commit,contributions没有显示绿色
date: 2018-3-03 21:12:45
categories: github
---

### ** preface **

因为到百度实习,工作繁忙且周末要补学校的课程作业,这几个月以来几乎没往github提交过commit,只写过几篇博客。博客使用的是hexo搭建的,也是托管在github上。

然而这几次提交的commit,在`contributions`统计处却没有出现绿色,误以为是因为在多个电脑,操作系统写博客,出现了一些错误操作,导致的。

可今天在向其他repo提交commit的时候,发现依旧没被统计上,才发现是其他的原因。

****************

先说结论:<span class="under0"> ** 出现上面所说的情况,是因为邮箱用户名不对。** </span >

在本地执行

```
git config --list 

or 

git config user.name
git config user.email
```

这里查询出来的email是我的百度邮箱。

问题就出在这儿

![github账户邮箱](/img/github/the-contributions-of-github-donnot-appear-green/1.png)

如上图,在我的github账户的setting中email中,并没有添加我的百度邮箱,所以`contributions`那儿是没有显示绿色的,但是commit都是记录上的,在`Add email address`处添加上邮箱就好了。

****************

### ** 写在后面 **

不过因为我的对自己的博客管理在多台电脑,多个操作系统使用的时候,操作有些失误,倒是减少了几百个commit。2333333心累.....


****************
### ** 参考 **

[解决github提交commit,contributions不统计显示绿色的问题](http://blog.csdn.net/e62ces0iem/article/details/73441144)

