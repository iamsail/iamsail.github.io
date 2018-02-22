---
title: coalball搬迁记录
date: 2017-06-05 22:23:45
categories: Linux
---

这两天开始部署coalball准备上线。

已经踩了不少坑,** 当然现在也还有坑还没解决完。**

### ** 先做些记录 **

**********************

- 服务器重启后,因为某些服务还没设置成自动启动,所以还得手动开启。

  nodebb项目重启,在目录下执行<code>./nodebb start</code>

- node项目之前肖高阳使用的是pm2,而我使用的是forever。需要学习下pm2

********************

### ** [搭PHP环境](http://bbs.qcloud.com/thread-1316-1-1.html) **

```
安装搭建论坛必要的软件 apache  php  mysql
yum install -y httpd php php-fpm mysql mysql-server php-mysql

将相应服务启动
service httpd start
service mysqld start
service php-fpm start

检查服务的运行情况
netstat -tunlp

【可选？】给mysql设定一个初始的root密码，可以让root用户去访问数据库
mysqladmin -u root password "XXXXXXXX"

```
*******************

### ** Mysql **

** ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES) **

- 背景:我自己的服务器是腾讯云centos7.x,所以数据库是mariadb,更多可以看我的博文[一次搬迁](http://www.sail.name/2017/04/15/a-removal/)。而工作室的服务器是centos6.8,所以数据库是Mysql。

- 问题原因,[戳这儿](http://www.cnblogs.com/kerrycode/p/4368312.html)

- [解决方案](https://stackoverflow.com/questions/21944936/error-1045-28000-access-denied-for-user-rootlocalhost-using-password-y)

```
#Stop MySQL
$ service mysqld stop

#Start it in safe mode:
$ (sudo)mysqld_safe --skip-grant-tables

#This will be an ongoing command until the process is finished so open another shell/terminal
#window, log in without a password:

$ mysql -u root
mysql> UPDATE mysql.user SET Password=PASSWORD('password') WHERE User='root';

#Start MySQL
$ service mysqld start

#your new password is 'password'.
```

后来我在[百度知道上看到一个回答](https://zhidao.baidu.com/question/1603863845338636507.html),也挺不错,可以参考着看

```
#1.停止mysql数据库
/etc/init.d/mysqld stop
 
#2.执行如下命令
mysqld_safe --user=mysql --skip-grant-tables --skip-networking &
 
#3.使用root登录mysql数据库
mysql -u root mysql
 
#4.更新root密码
mysql> UPDATE user SET Password=PASSWORD('newpassword') where USER='root';
#最新版MySQL请采用如下SQL：
mysql> UPDATE user SET authentication_string=PASSWORD('newpassword') where USER='root';
 
#5.刷新权限 
mysql> FLUSH PRIVILEGES;
 
#6.退出mysql
mysql> quit
 
#7.重启mysql
/etc/init.d/mysqld restart
 
#8.使用root用户重新登录mysql
mysql -uroot -p 
Enter password: <输入新设的密码newpassword>
```


#### ** Can’t connect to local MySQL server through socket **

```
yum install mysql-server

更多[戳这儿](http://www.d5s.cn/archives/9)
```
********************

### ** PHP **

- ThinkPHP上线记得删除掉`Runtime`目录

- 要注意权限问题,某些目录需要修改权限,`chomd -R`才是递归,否则没有递归效果

- 学会看日志,查找问题

- <span class="under0">修改服务器相关配置文件后,要重启服务器</span>

*******************
### **Nginx **

```
#nginx重启
$ nginx -s  reload
```

******************

### ** URL重写 **

<span class="under0">现在是6月20号晚上,折腾了两周服务器(想哭),总算搞定</span>

中途踩了很多坑,试了不少方法,做下记录

** 部署到工作室服务器(Linux和Win),均有一个test接口请求404,然而在自己的腾讯云服务器是正常的 **

解决办法

最后查看了** ThinkPHP文档中的URL重写 **

可以通过URL重写隐藏应用的入口文件index.php,下面是相关服务器的配置参考：

```
[ Apache ]

    httpd.conf配置文件中加载了mod_rewrite.so模块
    AllowOverride None 将None改为 All
    把下面的内容保存为.htaccess文件放到应用入口文件的同级目录下

<IfModule mod_rewrite.c>
 RewriteEngine on
 RewriteCond %{REQUEST_FILENAME} !-d
 RewriteCond %{REQUEST_FILENAME} !-f
 RewriteRule ^(.*)$ index.php/$1 [QSA,PT,L]
</IfModule>
```
*******************

### ** MySQL的乱码 **

** 默认都是latin编码,需要将各个项设置为utf8 **

网上有很多参考文章

****************

### ** 升级PHP **

centos下升级php5.3到php5.6

[戳这儿](http://blog.csdn.net/na_beginning/article/details/53414122)
```
yum install php56w-fpm
```
*****************
### ** vim 批量替换 **

```
#语法
:[addr]s/源字符串/目的字符串/[option]

#全局替换命令
:%s/源字符串/目的字符串/g

[addr] 表示检索范围，省略时表示当前行。
“1,20” ：表示从第1行到20行；
“%” ：表示整个文件，同“1,$”；
“. ,$” ：从当前行到文件尾；

s : 表示替换操作

[option] : 表示操作类型
g 表示全局替换;
c 表示进行确认
p 表示替代结果逐行显示（Ctrl + L恢复屏幕）;
省略option时仅对每行第一个匹配串进行替换;
如果在源字符串和目的字符串中出现特殊字符，需要用”\”转义 如 \t
```


*****************

### ** 上传文件的服务器相关配置 **

```
file_uploads 
## 设为On，允许通过HTTP上传文件 

upload_tmp_dir 
## 文件上传至服务器时用于临时存储的目录，如果没指定，系统会使用默认的临时文件夹（我的机器是/tmp）。 

upload_max_filesize 
## 允许上传文件大小的最大值，默认为2M。 

post_max_size 
## Php可接收的post数据的最大值（包括表单里的所有值的总合），默认为8M。 

memory_limit 
## 每个php所最占的最大内存数，这个值要大于允许上传的文件大小。 

max_execution_time 
## 每个php运行的最长时间（秒），默认30秒。 

## max_input_time 
Php解析POST/GET数据的最长时间（秒），默认60秒。This sets the maximum time in seconds a scripts 
is allowed to parse input data, like POST and GET.It is measured from the mement of receiving
 all data on the server to the start of script execution.
```

如果服务器上有装nginx,也需要对nginx进行配置

在`nginx.conf`文件的http模块中,增加
```
client_max_body_size xxm
```
*****************

### ** 文件上传保存错误 **

如果在线上环境遇到这个问题,需要将文件的保存目录重新创建,创建之前记得保存文件。

*****************

### ** 写在最后 **

这学期学习新技术,巩固基础的时间不是很多。这几天也折腾了四个服务器,仿佛变身运维工程师。

** 解决bug不要太急躁 **

希望在即将到来的暑假,不要颓废。

*******************

### ** 参考 **


- [使用PM2来部署nodejs项目](http://www.jianshu.com/p/d2a640b8661c)
- [使用 PM2 部署 Nodejs 项目](http://haoduoshipin.com/v/203.html)
- [ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)](https://stackoverflow.com/questions/21944936/error-1045-28000-access-denied-for-user-rootlocalhost-using-password-y)
- [vim批量替换命令实践](http://www.cnblogs.com/beenoisy/p/4046074.html)
- [ThinkPHP3.2.3完全开发](https://www.kancloud.cn/manual/thinkphp/1678)
- [配置php.ini实现PHP文件上传功能](http://www.cnblogs.com/52php/p/5665419.html)
*******************************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>

