---
title: TypeError:Cannot read property 'COLLATION' of undefined 
date: 2021-09-26 23:11:01
categories: [TypeOrm, nest]
---

最近用nest写应用的时候，orm用的是`typeorm`遇到了一个报错。
`ERROR [TypeOrmModule] Unable to connect to the database. TypeError: Cannot read property 'COLLATION' of undefined `

折腾了半天，发现是数据库库名首字母大写导致的。最后我将库名从`Bookkeeping`改成了`bookkeeping`就可以了。把这个记录下来了，帮助后面踩坑的朋友。

**<span class="under0">日常编码的时候还是要养成良好的习惯，比如不要用中文命名文件夹，数据库/表名，用小写。就可以直接避免类似的问题。</span>**

***********************

### ** 参考链接 **

- [TypeError: Cannot read property 'COLLATION' of undefined](https://github.com/typeorm/typeorm/issues/2403)

