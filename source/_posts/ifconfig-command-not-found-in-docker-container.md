---
title: docker容器中ifonfig not found
date: 2017-08-19 1:40:50
categories: Docker
---
### ** 前言 **

在docker容器中执行`ifconfig`,出现了`bash: ifconfig: command not found`的错误

**************

### ** 解决 **

```
### 拉取镜像
docker pull ubuntu

### 运行一个可交互的shell终端
docker run -it ubuntu /bin/bash
或者
docker run -i -t ubuntu /bin/bash

#-i 表示启动一个可交互的容器
#–t表示使用pseudo-TTY，关联到容器的stdin和stdout
#在终端中，如果输入exit命令将会停止当前容器；因此如果只是取消关联，可以键入ctrl-p或者ctrl-q
#你可以在其他终端通过docker ps 查看已经运行的容器列表

```
执行完以上命令后,执行了`ifconfig`,出现了`bash: ifconfig: command not found`

这里我先安装了vim

```
apt-get update
#这个命令的作用是：同步 /etc/apt/sources.list 和 /etc/apt/sources.list.d 中列出的源的索引，
这样才能获取到最新的软件包。 

apt-get install vim

#如果是：bash:ping: command not found
#apt-get install iputils-ping
```
再执行

`apt-get install net-tool`

即可
**********

### ** 补充命令 **

```
$ docker ps # 查看运行中的容器
$ docker ps -a # 查看所有容器

# 创建并启动容器
$ JOB=$(docker run -d ubuntu /bin/sh -c "while true; do echo Hello world; sleep 1; done")

# 停止一个容器
$ docker stop $JOB

# 启动一个已经创建的容器
$ docker start $JOB

# 重启一个容器
$ docker restart $JOB

# 停止一个容器
$ docker kill $JOB

# 删除一个容器
$ docker stop $JOB # 必须先停止
$ docker rm $JOB
```
**********

### ** 进入容器 ** 


```
docker attach CONTAINER ID

## eg
docker attach a7f843f07886
```
具体可以参考[这篇文章](http://blog.csdn.net/u010397369/article/details/41045251)

如果这种方法失败

可以使用
```
docker exec 

##eg
docker exec -it 775c7c9ee1e1 /bin/bash   
```

**********

### ** 参考 **

[Why isn't ifconfig available in Ubuntu Docker container?](https://serverfault.com/questions/613528/why-isnt-ifconfig-available-in-ubuntu-docker-container)
[Docker：bash: vi: command not found](http://blog.csdn.net/silentwolfyh/article/details/52336007)
