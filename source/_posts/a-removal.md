---
title: 一次搬迁
date: 2017-04-15 17:15:59
categories: Linux
---

前两日参加了中国大学生计算机设计大赛。

从选出队伍到部署提交作品只有两天，时间很紧。

中途遇到了一些问题，做些记录。

**************

#### One

在Xshell中执行了reboot,再次访问站点，失败。

因为http服务不是自启动。其实机器已经跑起来了。

执行 <code>service httpd start</code>

相关的还有

<code>service mysqld start</code>

<code>service mariadb start</code>

<code>service php-fpm start</code>

可以通过 <code>netstat -tunlp</code> 检查服务的运行情况


#### Tow

紧接One,centos7.x,已经没有MySQL了,而是 MariaDB。centos7.x以下的版本仍然是MySQL。

MySQL之父Widenius先生离开了Sun之后，觉得依靠Sun/Oracle来发展MySQL，实在很不靠谱，于是决定另开分支，这个分支的名字叫做MariaDB。

** MariaDB跟MySQL在绝大多数方面是兼容的，对于开发者来说，几乎感觉不到任何不同。 **目前MariaDB是发展最快的MySQL分支版本，新版本发布速度已经超过了Oracle官方的MySQL版本

更多请看文末的参考


#### Three

** apache的web根目录：/var/www/html , 不是/var/www **

我本地开发是wamp环境,web根目录是www


#### Four

Linux下导入SQL文件

<code>mysql -u root -p dbname < filename.sql</code>

filename.sql处填写你的sql文件所在的路径

dbname是数据库名称,需要提前创建


#### Five

JS脚本中的;一开始用的是全角,导致乱码。应该使用半角的;。

#### Six

修改MariaDB的字符编码

<code>vim /etc/my.cnf</code>

在 [mysqld] 下添加：

<code>character-set-server=utf8</code>

#### Seven

** [systemctl命令](http://man.linuxde.net/systemctl)是系统服务管理器指令，它实际上将 service 和 chkconfig 这两个命令组合到一起 **

#### Eight

因为需要录制一个作品演示视频,使用了[嘉明](http://wander.leanote.com/)推荐的FSCapture

#### Nine

之前不时会有Win10应用商店不能使用,有道也不能联网的问题。

前阵子在社区看到一个回答,大概是修改Edge/IE设置中的代理。

当时试了下,解决了我的问题。

具体记不清了,链接也忘记了保存。算是一个参考吧。

*******************

** 参考 **

- [经验分享 腾讯云新手专区](http://bbs.qcloud.com/forum.php?mod=viewthread&tid=2387&extra=page%3D1)
- [经验分享 CentOS 6.3 环境搭建discuz论坛](http://bbs.qcloud.com/thread-1316-1-1.html)
- [MariaDB 和 MySQL 比较](http://www.oschina.net/translate/mariadb-vs-mysql-a-comparison)
- [MySQL和mariadb区别](http://ask.chinaunix.net/question/556)
- [MariaDB与MySQL官方版本的主要区别](https://segmentfault.com/a/1190000007092956?_ea=1234141)
- [CentOS7安装MariaDB以及编码注意事项](http://blog.csdn.net/wzqnls/article/details/53241183)
