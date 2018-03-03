---
title: 添加到docker用户组
date: 2017-06-4 9:53:50
categories: Docker
---

### ** 背景 **

如果没有将用户添加到docker用户组,需要每次切换到root权限（sudo su）。

这样很麻烦,可以将用户添加到docker用户组,来解决这个问题。

************************

### ** 环境 **

- Ubuntu Trusty 14.04(TLS)

- 更多可以看我的博文[如何安装/更新/卸载Docker](http://www.sail.name/2017/03/05/how-to-install-docker/)

************************

** 添加docker group(已经有了可以跳过) **

<code>sudo groupadd docker</code>


** 将用户加入该 group 内。然后退出并重新登录即生效。**

<code>sudo [gpasswd](http://man.linuxde.net/gpasswd) -a ${USER} docker</code>

** 重启 docker 服务 **

<code>sudo service docker restart</code>

** 切换当前会话到新 group 或者重启 X 会话 **
<code>newgrp - docker</code>
OR
<code>[pkill](http://man.linuxde.net/pkill) X</code>

注意，最后一步是必须的，否则因为 groups 命令获取到的是缓存的组信息，刚添加的组信息未能生效，所以 docker images 执行时同样有错。

*********************

### ** 写在最后 **

添加几个小tips,仅作备忘

```
虚拟机全屏: Ctrl+Alt+Enter
打开终端:   Ctrl + Alt + T
外部定位到虚拟机: Ctrl+ G
虚拟机定位到外部: Ctrl + Alt
```

**************

#### ** 参考 **

- [Ubuntu16.04添加Docker用户组](http://blog.csdn.net/qq_22841811/article/details/53447570)

