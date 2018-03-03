---
title: phpstorm代码缩进风格设置
date: 2018-01-27 20:11:27
categories: Developer Tools
tags: 编码风格
---

### ** Preface ** ###

本文是对在phpstorm中设置代码缩进风格的记录

***************

关于缩进风格,四个空格还是tab可以说和vim还是emacs好一样都是程序员届的未解之谜。

我本人是使用四个空格作为缩进的。

***************

![1.png](/img/Developer-Tools/Code-indentation-style-settings-of-phpstorm/1.png)

`File -> Settings -> Editor -> Code Style`
`文件 -> 设置 -> 编辑器 -> Code Style`

把`Detect and use exsiting file indents for editing` 勾掉。 
不然缩进设置无效,默认设置就是使用4个空格代替tab。

![2.png](/img/Developer-Tools/Code-indentation-style-settings-of-phpstorm/2.png)

`Code Style`下面的语言可以进行更细化的设置

***************

有时候需要刷一遍tab缩进，把你不希望看到的缩进风格改成你希望的： 
使用`Ctrl + Alt + I `,直接把tab刷成4空格。

***************


### ** 参考 **

[PHPStorm IntelliJ IDEA 代码缩进风格设置](http://blog.csdn.net/cor_twi/article/details/52038301)
