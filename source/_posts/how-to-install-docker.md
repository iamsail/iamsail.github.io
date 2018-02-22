---
title: 如何安装/更新/卸载Docker
date: 2017-03-5 11:05:50
categories: Docker
---
因为项目的驱动，开始学习Docker。
这里不讲解什么是Docker，只谈怎样安装,更新，卸载Docker。

************************

### 注意事项
- Docker只能运行在Linux环境中
- Docker可以在Windows和Mac系统中使用(需要借助boot2Docker)
- Docker要求必须为64位操作系统
- Linux内核版本最小为3.10(3.10以下的内核存在一些bug,在某些特定场景中有可能会引起容器中的数据丢失)


### 安装步骤
- 我的安装环境是Ubuntu Trusty 14.04(TLS)

- 关于如何查看本机的位数和内核版本

位数：
** uname -m **
如果返回结果是i686, 说明是32位
如果返回结果是x86_64，说明是64位

内核版本：
** uname -r **
返回结果为形如3.13.0-93-generic，内核在3.10及以上即可

** sudo -s **
【切换到root】

** which wget **
【检查是否安装wget工具。如果安装了，将看到wget的路径。反之，会提示没有wget。倘若没有安装wget，则执行以下的命令安装wget
** sudo apt-get update **
** sudo apt-get install wget **】

** wget -qO- htts://get.Docker.com/ | sh **
【安装完wget之后，我们就可以使用wget获取Docker安装包】

** (sudo) docker run hello-world **
【执行命令验证是否安装成功。成功将看到Hello from Docker.....
如果你安装失败，你可以看看上面的注意事项】


### 更新Docker
** wget -qO- htts://get.Docker.com/ | sh **


### 卸载Docker
** sudo apt-get purge lxc-Docker **
【卸载Docker】

** sudo apt-get autoremove --purge lxc-Docker **
【卸载Docker安装包和Docker所有的依赖模块】

以上两条命令,仅仅是删除了安装包和依赖包，Docker所存储的image、container以及Docker所创建的配置文件,都还保留在系统目录下。执行下面的命令可以彻底清楚Docker所保留的数据

** rm -rf /var/lib/Docker **

*************

# 更新

今天是2017年9月18日,因为前段时间转为了双系统,win10 + ubuntu,在ubuntu中重新安装了docker。前文所记录的方法是在虚拟机中尝试的,在本机安装中发现该方法没有效果,特此记录下我在Ubuntu Xenial 16.04(TLS)的安装过程。

** 升级包信息，确保APT使用https的方法工作，与安装CA证书 **
```
$ sudo apt-get update  
  
$ sudo apt-get install apt-transport-https ca-certificates  
```

** 添加新的GPG key **
```
$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```

** 找到你的Ubuntu操作系统的条目，它决定了APT将搜索的包。可能的项 **


Ubuntu version | Repository
-|-
Precise 12.04 (LTS) | deb https://apt.dockerproject.org/repo ubuntu-precise main
Trusty 14.04 (LTS) | deb https://apt.dockerproject.org/repo ubuntu-trusty main
Xenial 16.04 (LTS) | deb https://apt.dockerproject.org/repo ubuntu-xenial main


** 运行以下命令,将占位符<REPO>替换为您的操作系统的条目（Repository） **

```
$ echo "<REPO>" | sudo tee /etc/apt/sources.list.d/docker.list  

例如：Ubuntu 16.04使用如下命令：
$ echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list
```

** 升级APT包索引 **

```
$ sudo apt-get update  
```

** 验证APT从正确的库拉取。
   运行下面的命令时，将返回每个可供您安装的Docker版本的条目。每个条目应该有URL   https://apt.dockerproject.org/repo/ **

```
apt-cache policy docker-engine  
```
************

### 各Ubuntu版本的必备条件
· Ubuntu Xenial 16.04 (LTS)
· Ubuntu Trusty 14.04 (LTS)
对于Ubuntu Trusty和Xenial，建议安装`linux-image-extra-* `内核包。这些`linux-image-extra-* `包允许你使用aufs存储驱动。
 
安装`linux-image-extra-*`包：
 
 1.在你的Ubuntu主机打开一个终端
 2.升级你的包管理器

```
$ sudo apt-get update  
```
安装建议的包
```
$ sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual  
```

### 安装

作为sudo特权用户登入你的Ubuntu进行安装
升级你的APT包索引

```
$ sudo apt-get update  
```

安装Docker
```
$ sudo apt-get install docker-engine  
```


启动docker守护进程

```
$ sudo service docker start  
```


确认docker安装正确
```
$ sudo docker run hello-world  
```

该步如果失败,可能是没有权限,执行
```
$ sudo -s

$ sudo docker run hello-world  
```

又或者可以将当前用户添加到docker用户组,具体可以参考我的博文[添加到docker用户组](http://www.sail.name/2017/06/04/add-to-docker-user-group/)

************

** 参考资料 **
 [docker-ubuntu14.04下的安装](http://blog.csdn.net/qq_25730711/article/details/53508780)
《Docker全攻略》ISBN 978-7-121-28238-6
 [Ubuntu安装Docker（官方文档翻译）](http://blog.csdn.net/a787202867/article/details/53036866)
 [Ubuntu16.04安装docker](http://www.cnblogs.com/lighten/p/6034984.html)
 [Ubuntu安装docker run hello-world无法连接仓库？1](https://segmentfault.com/q/1010000008664120/a-1020000008799199)   
*************
<div width="100%" align="center"><div name="dashmain" id="dash-main-id-87905c" class="dash-main-2 87905c-3"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>

