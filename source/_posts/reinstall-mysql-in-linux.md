---
title: 重装MySQL
date: 2018-5-05 18:53:45
categories: 数据库
tags: [MySQL]
---

### ** preface **

因为我的一大波骚操作导致MySQL使用中出现这个下面这个错误,记作A
```
update-alternatives: 错误: 候选项路径 /etc/mysql/mysql.cnf 不存在
dpkg: 处理软件包 mysql-server-5.7 (--configure)时出错：
 子进程 已安装 post-installation 脚本 返回错误状态 2
dpkg: 依赖关系问题使得 mysql-server 的配置工作不能继续：
 mysql-server 依赖于 mysql-server-5.7；然而：
  软件包 mysql-server-5.7 尚未配置。

dpkg: 处理软件包 mysql-server (--configure)时出错：
 依赖关系问题 - 仍未被配置
因为错误消息指示这是由于上一个问题导致的错误，没有写入 apport 报告。
                                                                    在处理时有错误发生：
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
```

折腾了很久,搜索的方法没有奏效。

于是决定卸载重装。应该是卸载的时候没有卸载干净,导致依旧会抛错。

最终看到[这篇文章](https://blog.csdn.net/luoww1/article/details/53741509),搞定了。


执行以下两个命令

```
sudo apt-get remove --purge mysql-\*
sudo apt-get install mysql-server mysql-client
```

****************************

### ** 參考 **

[linux mysql 安装，重装遇到问题](https://blog.csdn.net/luoww1/article/details/53741509)
[ubuntu完全卸载mysql](https://blog.csdn.net/w3045872817/article/details/77334886)
