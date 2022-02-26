---
title: git分支设置upstream
date: 2018-12-15 11:04:00
categories: Git
---

### ** Preface **

如果本地的分支没有和远程的分支进行关联,在`git pull/fetch`的时候，会抛出大致如下的错误信息

```
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

git branch --set-upstream-to=origin/<branch> release
```

** 建立本地分支与远程分支的映射关系（或者为跟踪关系track）。这样使用`git pull`或者`git push`时就不必每次都要指定从远程的哪个分支拉取合并和推送到远程的哪个分支了。**

*****************

#### ** 查看本地分支与远程分支的映射关系 **

```
git branch -vv
```
***************

### ** upstream的设置 **
#### ** 基本设置 **

执行如下命令即可将远程分支与本地分支关联

`git branch --set-upstream-to=origin/remote_branch  your_branch`
`origin/remote_branch`是你本地分支对应的远程分支；`your_branch`是你当前的本地分支。

把当前分支的upstream为origin远程仓库的dev分支
```
git branch --set-upstream-to=origin/dev
or
git branch -u origin/dev
```
***************

#### ** 在推送的同时，同时设置upstream **

```
git push -u origin master
```
推送master分支到远程origin仓库master分支，并且建立本地分支master的upstream为origin/master

*******************

#### ** 不切换分支直接设置其他分支的upstream **
```
git br -u origin/br01-remote br01
```
设置本地分支br01的upstream为origin/br01-remote

或push的时候直接设置
```
git push -u origin br03:br03
```

**********************************

#### ** 撤销本地分支与远程分支的映射关系 **

```
# 取消当前分支的upstream
git branch --unset-upstream

# 取消其他分支的upstream
git branch --unset-upstream [分支名]
```

*****************
### ** 参考 **

[設定 Upstream](https://zlargon.gitbooks.io/git-tutorial/content/remote/upstream.html)
[Git branch upstream](https://blog.csdn.net/tterminator/article/details/78108550)
[Git远程03：分支的upstream](https://higoge.github.io/2015/07/06/git-remote03/)
[git branch --set-upstream 本地关联远程分支](https://blog.csdn.net/z1137730824/article/details/78254564)