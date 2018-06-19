---
title: 菜鸡拯救秘诀
date: 2018-06-19 20:45:00
categories: PHP
---

### ** Preface **

<span class="under0">** 一台没有装PHP的开发机是不完整的。**</span>

<span class="under0">**在这个或许不是那么好的时代,如果你也和我一样感觉自己很菜,可以试试写世界上最好的语言,这样的确是会好一点。**</span>

*****************************

### ** 安装 **

#### ** 安装软件源拓展工具 **

```shell
sudo apt -y install software-properties-common apt-transport-https lsb-release ca-certificates
```
#### ** 添加` Ondřej Surý `的` PHP PPA `源 **：

```shell
sudo add-apt-repository ppa:ondrej/php
```
#### ** 更新软件源缓存 **

```shell
sudo apt update
```

如果在上面的安装过程中遇到了这个错误

`You are seeing this message because you have apache2 package installed`

解决方法,卸载`apache`相关的东西

```shell
sudo apt-get purge apache2
sudo apt autoremove
sudo apt autoclean
```

其他拓展，按需安装：

```shell
#  安装其他扩展（按需安装）
sudo apt-get install php7.2-gd
sudo apt-get install php7.2-soap
sudo apt-get install php7.2-gmp    
sudo apt-get install php7.2-odbc       
sudo apt-get install php7.2-pspell     
sudo apt-get install php7.2-bcmath   
sudo apt-get install php7.2-enchant    
sudo apt-get install php7.2-imap       
sudo apt-get install php7.2-ldap       
sudo apt-get install php7.2-opcache
sudo apt-get install php7.2-readline   
sudo apt-get install php7.2-sqlite3    
sudo apt-get install php7.2-xmlrpc
sudo apt-get install php7.2-bz2
sudo apt-get install php7.2-interbase
sudo apt-get install php7.2-pgsql      
sudo apt-get install php7.2-recode     
sudo apt-get install php7.2-sybase     
sudo apt-get install php7.2-xsl
sudo apt-get install php7.2-cgi        
sudo apt-get install php7.2-dba 
sudo apt-get install php7.2-phpdbg     
sudo apt-get install php7.2-snmp       
sudo apt-get install php7.2-tidy       
sudo apt-get install php7.2-zip
```

***********************
### ** 管理 PHP **

```regexp
systemctl restart php7.2-fpm #重启
systemctl start php7.2-fpm #启动
systemctl stop php7.2-fpm #关闭
systemctl status php7.2-fpm #检查状态
```


***********************

### ** 查看php已安装扩展命令 **

```regexp
php -m
```

*********************

### ** 内置Web Server **

PHP 5.4.0起， CLI SAPI 提供了一个内置的Web服务器。

这个内置的Web服务器主要用于本地开发使用，不可用于线上产品环境。

URI请求会被发送到PHP所在的的工作目录（Working Directory）进行处理，除非你使用了-t参数来自定义不同的目录。

如果请求未指定执行哪个PHP文件，则默认执行目录内的index.php 或者 index.html。如果这两个文件都不存在，服务器会返回404错误。

当你在命令行启动这个Web Server时，如果指定了一个PHP文件，则这个文件会作为一个“路由”脚本，意味着每次请求都会先执行这个脚本。如果这个脚本返回 FALSE ，那么直接返回请求的文件（例如请求静态文件不作任何处理）。否则会把输出返回到浏览器。

#### ** 启动Web服务器 **

```regexp
php -S localhost:8000
```

#### ** 启动时指定根目录 **

```regexp
php -S localhost:8000 -t foo/
```

#### ** 使用路由（Router）脚本 **

请求图片直接显示图片，请求HTML则显示“Welcome to PHP”

```php
<?php
// router.php
if (preg_match('/\.(?:png|jpg|jpeg|gif)$/', $_SERVER["REQUEST_URI"]))
    return false;    // 直接返回请求的文件
else { 
    echo "<p>Welcome to PHP</p>";
}
?>
```
```regexp
php -S localhost:8000 router.php
```

*****************************

### ** 参考 **

[在 Ubuntu/Debian 下安装 PHP7.2](https://www.mf8.biz/debian-install-php7-2/)
[ubutun安装php7.2](https://blog.csdn.net/zhezhebie/article/details/79939843)
[You are seeing this message because you have apache2 package installed.](https://blog.csdn.net/zhezhebie/article/details/79940324)
[查看php已安装扩展命令](https://blog.csdn.net/qdujunjie/article/details/11559883)
[内置Web Server](http://php.net/manual/zh/features.commandline.webserver.php)
[什么是CGI、FastCGI、PHP-CGI、PHP-FPM](https://segmentfault.com/a/1190000009066688)
[FastCgi 与 PHP-FPM 之间的区别](https://segmentfault.com/q/1010000000256516)