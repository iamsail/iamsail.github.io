---
title: Ubuntu20中安装MySQL5.7
date: 2021-10-18 22:04:45
categories: 数据库
tags: [MySQL]
---

### ** Preface **

本文是对在`Ubuntu20.04`中安装`MySQL5.7`的记录

*******************

### ** 安装MySQL **

首先在MySQL官网根据你的需求找到所需要安装的版本链接
- https://dev.mysql.com/downloads/mysql/
- https://downloads.mysql.com/archives/community/

![1.png](/img/mysql/1.png)

** 下载deb安装包 **
```shell
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-server_5.7.31-1ubuntu18.04_amd64.deb-bundle.tar
```


** 新建目录 **
`mkdir mysql5.7.31`
`mv mysql-server_5.7.31-1ubuntu18.04_amd64.deb-bundle.tar ./mysql5.7.31`

** 解压 **
`cd mysql5.7.31`
`sudo tar -vxf mysql-server_5.7.31-1ubuntu18.04_amd64.deb-bundle.tar`

** 解压出来的deb安装包如下 **
```
libmysqlclient20_5.7.31-1ubuntu18.04_amd64.deb
mysql-client_5.7.31-1ubuntu18.04_amd64.deb
mysql-community-source_5.7.31-1ubuntu18.04_amd64.deb
mysql-server_5.7.31-1ubuntu18.04_amd64.deb
mysql-common_5.7.31-1ubuntu18.04_amd64.deb
mysql-testsuite_5.7.31-1ubuntu18.04_amd64.deb
libmysqlclient-dev_5.7.31-1ubuntu18.04_amd64.deb
mysql-community-client_5.7.31-1ubuntu18.04_amd64.deb
mysql-community-server_5.7.31-1ubuntu18.04_amd64.deb
libmysqld-dev_5.7.31-1ubuntu18.04_amd64.deb
mysql-community-test_5.7.31-1ubuntu18.04_amd64.deb
```

** 删除2个测试相关的包 **
`sudo rm -f mysql-testsuite_5.7.31-1ubuntu18.04_amd64.deb`
`sudo rm -f mysql-community-test_5.7.31-1ubuntu18.04_amd64.deb`

** 安装依赖 **
`sudo apt-get install libtinfo5`
`sudo apt-get install libmecab2`

** 使用deb安装 **
`sudo dpkg -i mysql-*.deb`


*******************

### ** 基本命令 **
```
#启动mysql
sudo service mysql start

#停止mysql
sudo service mysql stop

#重启mysql
sudo service mysql restart

#查看mysql状态
sudo service mysql status
```

*******************
### ** 参考链接 **

- [Ubuntu20安装MySQL5.7](https://viencoding.com/article/295)
- [Ubuntu20.04 安装 MySQL5.7](https://www.jianshu.com/p/ba48f1e386f0)
- [Ubuntu安装mysql5.7（诲人不倦，记点干货）](https://cloud.tencent.com/developer/article/1655900)
- [ubuntu20.04 安装mysql5.7配置](https://www.cnblogs.com/MaggieForest/p/14868085.html)


