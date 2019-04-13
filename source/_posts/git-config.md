---
title: git config
date: 2018-04-10 21:15:00
categories: Git
---

###  ** Preface **

本文是对`git config`部分参数的一点介绍。

最好的教程就是`man git config`。

******************
```
-e, --edit

Opens an editor to modify the specified config file; either --system, --global, or repository (default).
```

`git config -e`， 就是对配置文件进行编辑。 

这里还有几个参数,分别是`--local`, `--global`, `--system`,
```
# git config -e --local
# git config -e --global
# git config -e --system

--local
    For writing options: write to the repository .git/config file. This is the default behavior.
    For reading options: read only from the repository .git/config rather than from all available files.
    See also the section called “FILES”.

--global
    For writing options: write to global ~/.gitconfig file rather than the repository .git/config, write to $XDG_CONFIG_HOME/git/config file if this file
    exists and the ~/.gitconfig file doesn’t.
    For reading options: read only from global ~/.gitconfig and from $XDG_CONFIG_HOME/git/config rather than from all available files.
    See also the section called “FILES”.

--system
    For writing options: write to system-wide $(prefix)/etc/gitconfig rather than the repository .git/config.
    For reading options: read only from system-wide $(prefix)/etc/gitconfig rather than from all available files.
    See also the section called “FILES”.
```

简单总结下,`--local`是修改`.git/config`,`--global`是修改 `~/.gitconfig`,`--system`是修改 `/etc/gitconfig`.分别是仓库的配置文件,当前用户的配置文件,本机的配置文件。

`git config -e` 等同于 `git config -e --local`

`优先级是git config > git config --global > git config --system`,因为配置文件是就近查找的,如果没有,再向外查找配置文件。

**********************

** 如果Github没有记录上你的Contributions,可能就是因为你的用户名或者邮箱跟github没有关联上,github认为不是你提交的,不统计。**

对当前仓库做设置

```
git config --local user.name "Sail"
git config --local user.email "865605793@qq.com"
```


***********************
### ** 参考链接 **

[【GIT问题】--为什么Github没有记录你的Contributions - 简书](https://www.jianshu.com/p/56cb8a5d7379)