---
title: 提交镜像到Docker Hub
date: 2017-10-05 13:20:20
categories: Docker
---

### ** 写在前面 **

本文是如果将本地镜像提交到`Docker Hub`的记录。

***************

### ** PUSH **

#### ** 注册 **

首先得有一个帐号23333333

[注册传送门](http://docker.com/)


**************

#### ** 登录帐号 **

打开终端

```
##使用docker login命令登入Docker Hub
$ docker login
Username: your Username 
Password: your Password

Login Succeeded
```
*************

#### ** 生成镜像 **

这里我只介绍如何将容器生成镜像。这样开发环境就可以放在云端,敲击几个命令即可搭建好开发环境。

`docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`

```
Create a new image from a container's changes

Options:
  -a, --author string    Author (e.g., "John Hannibal Smith <hannibal@a-team.com>")
  -c, --change list      Apply Dockerfile instruction to the created image
      --help             Print usage
  -m, --message string   Commit message
  -p, --pause            Pause container during commit (default true)

```

```
## 示范
## d09cdedcfb69 是 对应容器ID

docker commit d09cdedcfb69 sail97/mysql
OR
sudo docker commit  -m"a new mysql" --author='Sail' d09cdedcfb69 sail97/mysql:tagName
```

***************
#### ** 提交 **

`docker push your your Username/repoName[:TAG]`


```
## 示范
docker push sail97/mysql
docker push sail97/mysql:v0.0.1
```

***************

### ** 参考 **

[Docker学习小记——Docker的镜像和仓库](https://lucifaer.github.io/2017/01/18/Docker%E5%AD%A6%E4%B9%A0%E5%B0%8F%E8%AE%B0%E2%80%94%E2%80%94Docker%E7%9A%84%E9%95%9C%E5%83%8F%E5%92%8C%E4%BB%93%E5%BA%93/)
