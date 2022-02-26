---
title: Git fatal 拒绝合并无关的历史
date: 2022-02-26 12:44:45
categories: Git
---

今天在git合并分支的时候报了这个错误`Git fatal:拒绝合并无关的历史`。

以前没有遇到过类似的问题。查了下是因为从Git 2.9版本开始这个命令有了些变化

```
 * "git merge" used to allow merging two branches that have no common
   base by default, which led to a brand new history of an existing
   project created and then get pulled by an unsuspecting maintainer,
   which allowed an unnecessary parallel history merged into the
   existing project.  The command has been taught not to allow this by
   default, with an escape hatch "--allow-unrelated-histories" option
   to be used in a rare event that merges histories of two projects
   that started their lives independently.

 * "git pull" has been taught to pass the "--allow-unrelated-histories"
   option to underlying "git merge".
```

上面这段changelog大意是说：`git merge`之前允许合并两个没有公共提交记录的分支，这会导致不必要的提交记录历史被合并到当前分支。现在这个命令默认(从2.9版本开始)不允许这样做了。但是使用`-allow unrelated history`选项依然可以。

所以给`git merge`命令加上`–allow-unrelated-histories`参数就可以了

执行以下命令即可
```
git merge branchName --allow-unrelated-histories
```

*****************
### ** 参考 **

- [Git refusing to merge unrelated histories on rebase](https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories-on-rebase)
- [Git2.9 changelog](https://github.com/git/git/blob/master/Documentation/RelNotes/2.9.0.txt#L58-L68)