title: github多个帐号使用
date: 2017-10-02 23:52:20
categories: github
---

### ** 写在前面 **

除了自己的github帐号还有工作室的github帐号,本文记录下多个帐号的使用。

****************

### ** hexo **

这里简要叙述下hexo的搭建

node.js和git是前提条件,不再罗嗦

安装hexo
`npm install -g hexo`

进入blog目录

初始化,生成模板
`hexo init`

预览
`hexo server `


然后放入自己的主题文件和曾经的md文件就可以了 

我自己是多个分支进行管理,其中一个分支就是用来管理md文件以及配置文件的
**************

### ** 多个帐号使用 **

<span class="under0">新建user的SSH Key</span>

```
ssh-keygen -t rsa -C "username" 

## (注：username为你git上的用户名)
## (注：username为你git上的用户名)
## (注：username为你git上的用户名)

# 设置名称
Enter file in which to save the key (/c/Users/Administrator/.ssh/id_rsa): 

/c/Users/Administrator/.ssh/id_rsa_user2

```

**************

<span class="under0">添加密钥到`SSH agent`中</span>

因为默认只读取`id_rsa`，为了让SSH识别新的私钥，需将其添加到`SSH agent`中
```
ssh-add ~/.ssh/id_rsa_user2

## 如果出现Could not open a connection to your authentication agent的错误，就试着用以下命令：
ssh-agent bash
ssh-add ~/.ssh/id_rsa_user2
```
***************


<span class="under0">修改`config`文件</span>
```
 在~/.ssh目录下找到config文件，如果没有就创建：
touch config    
然后修改我的config配置如下：
如果存在的话，其实就是往这个config中添加一个Host：
#建一个github别名，新建的帐号使用这个别名做克隆和更新
其规则就是：从上至下读取config的内容，在每个Host下寻找对应的私钥。
这里将GitHub SSH仓库地址中的git@github.com替换成新建的Host别名如：github2，那么原地址 是
：git@github.com:test/Mywork.git，替换后应该是：github2:test/Mywork.git.


## 示范

Ｈost github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentifyFile ~/.ssh/id_rsa

## 设置第二个用户
## 新建一个github别名,新建的帐号使用这个别名做克隆和更新

Ｈost github2
    HostName github.com
    PreferredAuthentications publickey
    IdentifyFile ~/.ssh/id_rsa_user2  
```

*****************

<span class="under0"> 添加到github帐号</span>

将新生成的`~/.ssh/id_rsa_user2.pub`文件，将里面的内容添加到GitHub对应帐号`setting`中的`SSH key`

***************

### ** 参考 **

[手把手教你同时使用多github帐号的SSH key](https://jingyan.baidu.com/article/948f592414ad67d80ef5f966.html)
[git "Could not read from remote repository.Please make sure you have the correct access rights."解决方案](http://blog.csdn.net/u014343528/article/details/48787221)

