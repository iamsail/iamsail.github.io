---
title: .gitignore
date: 2017-07-25 17:45:27
categories: Git
---

###  ** 背景 **

本文是对`.gitignore`文件的一些介绍

`.gitignore`文件可以通过写入一些规则指定尚未commit提交的文件被git忽略,使得与规则匹配的文件,不进行版本管理。粗暴的说,就是`.gitignore`可以使一些文件不被添加到github上。且已经commit的文件不受.gitignore影响。

当然这个我们是可以解决的,这个我在后面会介绍。

**********

### ** 规范 **

`#` 为注释
`/` 以`/`开头表示(忽略)目录
`!` 否定模式,任何由先前模式排除的匹配文件将被再次包含,即不忽略。如果该文件的父目录被排除，则不可能重新包含文件


可以使用shell所使用的正则表达式来进行模式匹配   
如果模式不包含斜杠`/`,Git将其视为`shell glob`模式，并检查与`.gitignore`文件位置相对的路径名的匹配（相对于工作树的顶点，如果不是从` .gitignore`文件）

<span class="under0"> 两个连续的 `** `与完整路径名匹配的模式可能有特殊含义 </span>


尾随` /**`匹配内部的一切。例如` abc/**`匹配目录` abc `内的所有文件，相对于` .gitignore `文件的位置，具有无限深度


**********

### ** 模式 **

`.gitignore`文件过滤有两种模式,开放模式和保守模式

#### ** 开放模式 **

开放模式设置过滤哪些文件和文件夹

```
# 过滤文件夹
/directoryName

#指定过滤某种类型的文件
*.zip
*.rar

#指定过滤某个具体文件
/directoryName/fileName

```

#### ** 保守模式 **
保守模式负责设置哪些文件不被过滤，也就是哪些文件要被跟踪。
```
# 跟踪文件夹
!/directoryName

#跟踪某种类型的文件
!*.zip
！*.rar

#跟踪某个具体文件
！/directoryName/fileName
```
#### ** 配置准则 **

共享模式与保守模式相结合。

比如,只想跟踪某个目录下的其中一个文件,可以先共享模式将整个目录设置为不跟踪,再通过保守模式把需要跟踪的文件设置为被跟踪

***********

### ** 问题解决 **

开篇提到了如果在设置`.gitignore`之前,有的文件已经commit过,即已经被git管理了的,`.gitignore`的规则是不会起作用的

这个问题有一个解决方案

需要对已经提价的文件执行如下命令,即可

```
git rm --cached FILENAME
```




**********


### ** 参考 **

[gitignore](https://git-scm.com/docs/gitignore)
[Ignoring files](https://help.github.com/articles/ignoring-files/)
[ Github使用gitignore忽略增加指定文件](http://blog.csdn.net/cscmaker/article/details/8553980)
[Git忽略规则.gitignore梳理](http://www.cnblogs.com/kevingrace/p/5690241.html)
[.gitignore](http://blog.csdn.net/liuqiaoyu080512/article/details/8648266)
