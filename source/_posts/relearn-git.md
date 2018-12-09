---
title: 重学Git
date: 2018-01-27 16:55:27
categories: Git
---

###  ** Preface ** 

最近做项目的过程中,发现自己对git的掌握并不牢固,有的用法还比较生疏。当然也和我以往面对的场景不同有关。本文做一些记录。

***************

### ** 寻找历史命令 **

当我们处在terminal,可以通过`history`来查看历史命令。**<span class="under0"> 其实还可以通过ctrl+r,来搜索历史命令。</span>**

****************

### ** git log **

`git log`可以查看提交历史。

默认不用任何参数的话，`git log `会按提交时间列出所有的更新，最近的更新排在最上面。每次更新都有一个 SHA-1 校验和、作者的名字和电子邮件地址、提交时间，最后缩进一个段落显示提交说明。

![1.png](/img/git/relearn-git/1.png)

辅助一些参数的话,可以发挥更强大的功能。

#### ** -p ** ####

`-p` 选项展开显示每次提交的内容差异。`git log -p`

#### ** -n ** ####

`-n` 选项显示最近的n次更新。`git log -n`

#### ** --word-diff ** ####
某些时候，单词层面的对比，比行层面的对比，更加容易观察。Git 提供了 `--word-diff` 选项。我们可以将其添加到 `git log -p` 命令的后面，从而获取单词层面上的对比。在程序代码中进行单词层面的对比常常是没什么用的。不过当你需要在书籍、论文这种很大的文本文件上进行对比的时候，这个功能就显出用武之地了。`git log -p --word-diff`

`git log`还提供了许多摘要选项可以用

#### ** --stat ** ####

仅显示简要的增改行数统计。`git log --stat`

#### ** --pretty ** ####

可以指定使用完全不同于默认格式的方式展示提交历史。
比如用` oneline `将每个提交放在一行显示，这在提交数很大时非常有用。另外还有` short`，`full` 和 `fuller` 可以用，展示的信息或多或少有些不同.

```
git log --pretty=oneline
git log --pretty=short
git log --pretty=full
git log --pretty=fuller
```

特别的是使用`format`,可以定制要显示的记录格式，这样的输出便于后期编程提取分析

`git log --pretty=format:"%h - %an, %ar : %s"`

```
ca82a6d - Scott Chacon, 11 months ago : changed the version number
085bb3b - Scott Chacon, 11 months ago : removed unnecessary test code
a11bef0 - Scott Chacon, 11 months ago : first commit
```

![2.png](/img/git/relearn-git/2.png)

#### ** --graph ** ####

用 `oneline` 或 `format` 时结合 `--graph` 选项，可以看到开头多出一些 ASCII 字符串表示的简单图形，形象地展示了每个提交所在的分支及其分化衍合情况

` git log --pretty=format:"%h %s" --graph`

#### ** 按照时间作限制 ** ####

列出所有最近两周内的提交

`git log --since=2.weeks`

![3.png](/img/git/relearn-git/3.png)

****************
### ** git cherry-pick ** ###

这个命令以前我没接触过。**<span class="under0"> 作用是将之前的提交的挑选某一个、或多个commit应用到当前分支。 </span>**

比如有master和dev两个分支,master分支有a1,a2两个commit,dev分支有b1,b2,b3三个commit,如果想将b2分支合并到master。

```
git checkout master

git cherry-pick b2-commit-id

## cherry-pick过后,如果出现了冲突,就解决冲突后再提交

```

****************
### ** git rebase ** ###

[rebase](http://gitbook.liuhui998.com/4_2.html)

****************
### ** git stash ** ###

[这篇文章](https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%82%A8%E8%97%8F%EF%BC%88Stashing%EF%BC%89)讲得很详细

总结下常用的几个命令

```
# 将修改暂存到栈中
git stash

# 查看现有的储藏
git stash list

# 应用指定的储藏  apply 选项只尝试应用储藏的工作——储藏的内容仍然在栈上。
git stash apply stash@{n}

# 要移除它,运行
git stash drop  stash@{n}

# 重新应用储藏，同时立刻将其从堆栈中移走
git stash pop  stash@{n}

```
****************
### ** git reset ** ###

Git中，用`HEAD`表示当前版本,也就是最新的提交,上一个版本就是`HEAD^`,上上一个版本就是`HEAD^^`,当然往上100个版本写100个^比较容易数不过来,所以写成`HEAD~100`

这个命令的难点在于理解这三个参数:`soft,mixed(默认),hard`
```
soft  就是只动repo
mixed 就是动repo还有staging
hard  就是动repo还有staging还有working
```
这里又涉及了三个概念,分别是`Working Tree,Index,Repository`

1. Working Tree (工作目录): Git管理的目录，也就是我们实际操作的目录

2. Index (系统索引): 存放一堆需要被commit的(异动)文件内容集合，把档案加入索引称Stage 或Cache。

3. Repository (仓库): 是Git存放文件的位置，许多commit结点(版本)记录于此。


****************
### ** git add ** ###

`git add . `：他会监控工作区的状态树，使用它会把工作时的所有变化提交到暂存区，包括文件内容修改(modified)以及新文件(new)，但不包括被删除的文件。

`git add -u `：他仅监控已经被add的文件（即`tracked file`），他会将被修改、删除的文件提交到暂存区。`git add -u `不会提交新文件（`untracked file`）。（`git add --update`的缩写）

`git add -A `：是上面两个功能的合集（`git add --all`的缩写）
****************
### ** 删除分支 ** ###

#### ** 删除远程分支 ** ####

`git push origin --delete remote-branch-name`

#### ** 删除本地分支 ** ####

`git branch -d local-branch-name`

若分支有修改还未合并，会提示还没合并。

强行删除本地分支

`git branch -D local-branch-name`

****************
### ** 分支管理 ** ###

#### ** 本地从当前所在分支上创建一个新分支 ** ####

`git checkout -b newBranchName`

#### ** 拉取远程某个分支到本地 ** ####

`git checkout -b local-branch-name origin/remote-branch-name`

****************

### ** 写在最后 **

最近才发现自己对git掌握得很皮毛。想起之前觉得自己掌握得不错,无地自容.....

****************


###  ** 参考 ** 

[ Git 基础 - 查看提交历史](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2)
[git-cherry-pick](https://git-scm.com/docs/git-cherry-pick)
[cherry-pick](https://backlog.com/git-tutorial/cn/stepup/stepup7_4.html)
[git stash和git stash pop](http://blog.csdn.net/wh_19910525/article/details/7784901)
[rebase](http://gitbook.liuhui998.com/4_2.html)
[Git 工具 - 储藏（Stashing）](https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%82%A8%E8%97%8F%EF%BC%88Stashing%EF%BC%89)
[版本回退](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)
[git reset soft,hard,mixed之区别深解](http://www.cnblogs.com/kidsitcn/p/4513297.html)
[git reset hard/soft/mixed区别](http://blog.csdn.net/carolzhang8406/article/details/49761927)
[Git Reset - mixed, hard and soft](https://dotblogs.com.tw/wasichris/2016/04/29/225157)
[git reset详解](https://segmentfault.com/a/1190000009658888)
[Git reset](https://www.cnblogs.com/qianqiannian/p/6010238.html)
[ git add .和git add -u和git add -A的区别](http://blog.csdn.net/lcxywfe/article/details/53260338)
[Git 如何删除本地分支和远程分支](http://blog.csdn.net/sub_lele/article/details/52289996)
[Git本地从某个分支上创建新分支以及拉取远程分支到本地分支](http://blog.csdn.net/bin622/article/details/69948525)
