---
title: SSH Could not resolve hostname ssh.github.com
date: 2017-07-22 09:16:31
categories: github
---

### ** 问题 **

昨天提交github,出现了如下的错误

```
ssh: Could not resolve hostname ssh.github.com: Name or service not known 
fatal: Could not read from remote repository.

Please make sure you have the correct access rights 
and the repository exists. 

```
*******************

### ** 解决 **

##### ** 环境: **

Win10 
Git bash

```
ping github.com
```
 
获取到github.com的ip为192.30.255.113

<span class="under0">注意,这个ip不是稳定不变的,以自己电脑ping出来的为准确</span>

进入/etc目录修改hosts文件

```
vi /etc/hosts
```

文件末尾添加 ip   github.com

```
192.30.255.113  github.com
```
*****************

### ** 更新 **

现在是9月3日,前几天装了win10+unbuntu的双系统。装完过后在win10下又出现了这个问题。本文一开始写的方法不在生效,我又尝试了一些其他方案,有时候可以有时候不可以,原因未知。

稳妥起见,大部分项目都是使用https连接了,不得已放弃了ssh。希望过段时间可以解决。把尝试方案的参考链接更新下





******************

### ** 参考 **

[Push to GitHub：could not resolve host: github.com](http://www.cnblogs.com/thqy39/p/5341911.html)
[ssh connect to host github.com port 22 Connection refused](https://www.iwwenbo.com/git-connection-refused/)
[提交代码到GitHub SSH错误解决方案](http://www.shenyanchao.cn/blog/2013/09/16/git-ssh-connection/)

