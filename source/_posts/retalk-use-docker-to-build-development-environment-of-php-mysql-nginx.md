---
title: 再谈docker搭建nginx+php+mysql开发环境
date: 2017-09-26 16:04:20
categories: Docker
---
## ** 写在前面 **

前几天我写了一篇博客[docker搭建nginx+php+mysql开发环境](http://www.sail.name/2017/09/23/use-docker-to-build-development-environment-of-php-mysql-nginx/)。当时主要是参考一片博文搭建记录的。

可是这样搭建出来是有一些问题的,具体的原因我还没找出。当然那篇文章还是有一些参考价值。

于是我又自己重新搭建了一个,踩了很多很多的坑,好在都解决了。

本文就是记录我的搭建过程,踩的坑,以及结合`thinkphp`项目存在的一些问题解决方案。

`docker`的好处我就不说了,和`git`一样,谁用谁知道。

本文参考的文章,会放在文末的参考。部分参考内容会在文中给出参考链接。

******************

## ** 搭建 **

### ** 环境介绍 **

操作系统
`Ubuntu 16.04 LTS`
docker版本
`Docker version 17.05.0-ce`

*******************

### ** 项目结构参考 **

这里先给出项目结构参考树形图,有的内容是在搭建中产生的,故仅供参考,与后文内容结合看。
```
sail@codeBetter:~$ tree www -L 1
www
├── default.conf   
├── Dockerfile
├── html
├── mysql
├── php.ini
└── www.conf

```

```
sail@codeBetter:~$ tree www -L 2
www
├── default.conf
├── Dockerfile
├── html
│   ├── coalball
│   ├── index.html
│   ├── index.php
│   └── mysql.php
├── mysql
│   ├── auto.cnf
│   ├── ca-key.pem
│   ├── ca.pem
│   ├── client-cert.pem
│   ├── client-key.pem
│   ├── coalball
│   ├── coalball.sql
│   ├── ib_buffer_pool
│   ├── ibdata1
│   ├── ib_logfile0
│   ├── ib_logfile1
│   ├── ibtmp1
│   ├── mysql
│   ├── performance_schema
│   ├── private_key.pem
│   ├── public_key.pem
│   ├── server-cert.pem
│   ├── server-key.pem
│   ├── sys
│   └── test_db
├── php.ini
└── www.conf

### 去掉一些无关内容

www
├── default.conf 
├── Dockerfile
├── html
│   ├── coalball
│   ├── index.html
│   ├── index.php
│   └── mysql.php
├── mysql
│   ├── coalball.sql
├── php.ini
└── www.conf

```
********************

### ** MySQL **

从 [Dockerhub](https://hub.docker.com/)拉取 `MySQL` 镜像：
```
$ docker pull mysql
```

实例容器,启动数据库
```
$ docker run -p 3306:3306 --name mysql -v ~/www/mysql/:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d --privileged=true mysql

### 命令说明：
-p 3306:3306：将容器的3306端口映射到主机的3306端口
-v ~/www/mysql/:/var/lib/mysql：将主机当前用户目录下的mysql文件夹挂载到容器的/var/lib/mysql 下，在mysql容器中产生的数据就会保存在本机mysql目录下
-e MYSQL_ROOT_PASSWORD=123456：初始化root用户的密码
-d 后台运行容器
--name 给容器指定别名
--privileged=true  可能会碰到权限问题，需要加参数
```
***************

### ** Nginx **

从 [Dockerhub](https://hub.docker.com/)拉取 `Nginx` 镜像：
```
$ docker pull nginx
```

实例容器,启动Nginx
```
$ docker run --name nginx -p 80:80 -d nginx


运行成功后，终端会返回容器的ID号，上面的命令中，

run：创建一个新的容器
--name：指定容器的名称（如果留空，docker会自动分配一个名称）
-p：导出容器端口到本地服务器，格式：-p <local-port>:<container-port>。在本例中，我们映射容器的80端口到本地服务器的80端口。
nginx：是 Dockerhub 上下载nginx镜像名称（如果本地没有可用的镜像，Docker会自动下载一个）
-d：后台启动。

```

通过浏览器浏览：`http://localhost` 就会看到`Nginx`欢迎界面。

几个命令介绍
```
$ docker ps -a                       # 查看正在运行的容器
$ docker ps                          # 查看容器
$ docker stop nginx                  # 停止正在运行的容器
$ docker start nginx                 # 启动一个已经停止的容器
$ docker start nginx                 # 重启一个容器
$ docker rm nginx                    # 删除容器

```

#### ** 映射HTML路径 **


默认情况下，`Docker nginx`服务器的`HTML`路径（网站根目录）在容器` /usr/share/nginx/html `目录下，现在需要把这个目录映射到本地服务器的` ~/www/html `目录。在上面命令的基础上加上-v参数，具体如下：
```
## 先删除之前的容器
$ docker rm nginx    

$ docker run --name nginx -p 80:80 -d -v ~/www/html:/usr/share/nginx/html nginx
```

 -v的参数格式为：`<local-volumes>:<container-volumes>`。

在`~/www/html`下创建一个` index.html `文件，内容随意

比如 `hello world`

在浏览器上访问 `http://localhost`，刷新一下就可以看到新的内容了。


#### ** 配置 Nginx **

`Nginx `的强大很大部分体现在配置文件上，对于一些高级的应用来说，自定义` Nginx `非常重要。所以，我们需要把` Nginx `的配置文件复制到本地服务器目录：

```
$ cd ~/www
$ docker cp nginx:/etc/nginx/conf.d/default.conf default.conf
```

再加一个-v参数，把本地的配置文件映射到容器上，在重启容器：
```
$ docker stop nginx

$ docker rm nginx

$ docker run --name nginx -p 80:80 -v ~/www/html:/usr/share/nginx/html -v ~/www/default.conf:/etc/nginx/conf.d/default.conf -d nginx
```
如果配置文件有修改，需要重启容器生效：
```
$ docker restart nginx
```
这样就可以直接在本地修改配置文件了。

***************

### ** PHP-FPM **

从 [Dockerhub](https://hub.docker.com/)拉取 `PHP-FPM` 镜像：

```
$ docker pull php:fpm
```
实例容器,启动`php:fpm`

```
$ docker run --name php-fpm -p 9000:9000 -d php:fpm
```
把配置文件复制到本地：

```
$ cd ~/www

$ docker cp php-fpm:/usr/local/etc/php-fpm.d/www.conf www.conf
$ docker cp php-fpm:/usr/src/php/php.ini-production php.ini
```
这里要特别注意一下,`php-fpm:/usr/src/php/php.ini-production`,在实例出的容器中,不一定是路径`src/php`,拉取的`php:fpm`版本镜像不同,`php.ini`路径不同。

可以这样查看`php.ini`路径


```
# 先进入容器
$ docker exec -it php-fpm bash

$ cd /usr/src/ && ls

# 有以下两个文件
php.tar.xz   php.tar.xz.asc

# 这里我们需要解压php.tar.xz文件,因为php.ini-production就在其中
//先解压xz
 xz -d php.tar.xz  
//再解压tar
# tar -xvf  php.tar
```

解压完毕后, `php.ini-production`便出现了，我当时的路径是`/usr/src/php-7.1.9/php.ini-production`。

```
即,前文中的

$ docker cp php-fpm:/usr/src/php/php.ini-production php.ini

改为

$ docker cp php-fpm:/usr/src/php-7.1.9/php.ini-production php.ini
```

在本地服务器修改 `php.ini` 的内容，设置`cgi.fix_pathinfo=1`（要先删除前面的;注释符）。

***************

前面关于php-fpm的一系列操作主要是为了获得配置文件,并没有挂载本地目录到容器中,所以接下来需要删除容器,重新实例一个容器出来

```
$ docker stop php-fpm
$ docker rm php-fpm

$ docker run --name php-fpm -p 9000:9000 --link mysql:mysql -v ~/www/html:/var/www/html -v ~/www/www.conf:/usr/local/etc/php-fpm.d/www.conf -v ~/www/php.ini:/usr/local/etc/php/php.ini -d php:fpm
```

### ** 配置Nginx **

修改`Nginx`的配置文件，也就是前面我们从容器中复制出的`default.conf`

```
server {
    listen       80;
    server_name  _;
    root /usr/share/nginx/html;
    index index.php index.html index.htm;

    #charset koi8-r;
    #access_log  /var/log/nginx/log/host.access.log  main;

    location / {
        #root   /usr/share/nginx/html;
        #index  index.php index.html index.htm;
	try_files $uri $uri/ =404;
    }

    error_page  404  /404.html;
    location = /40x.html {
        root    /user/share/nginx/html;
    }

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    location ~ \.php$ {
        root           /var/www/html/;
        fastcgi_pass   php-fpm:9000;
        fastcgi_index  index.php;
#        fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        include        fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

    }

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    location ~ /\.ht {
        deny  all;
    }
}
```

关于配置文件,有个需要注意的地方
```
    location ~ \.php$ {
        root           /var/www/html/;
        fastcgi_pass   php-fpm:9000;
        fastcgi_index  index.php;
#        fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        include        fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

    }
    
include        fastcgi_params;  
要放在
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
的前面    
```

删除刚才的nginx容器,重新生成一个

```
$ docker stop nginx
$ docker rm nginx

$ docker run --name nginx -p 80:80 --link php-fpm -v ~/www/html:/usr/share/nginx/html -v ~/www/default.conf:/etc/nginx/conf.d/default.conf -d nginx
```

在 `~/www/html` 下创建 `index.php`
```
<?php
    phpinfo();
```

浏览器访问`http://localhost`


![phpinfo](/img/docker/phpNgxinMysql/phpinfo.png)

***************

上面的讲述基本描述了如何搭建一个基本的`php+nginx+mysql`的开发环境。

然而在实际开发中,还是有问题的,比如php需要安装的一系列的扩展,比如`pdo_mysql`，我们可以通过编写`Dockerfile`的方式来定制镜像

## ** 编写Dockerfile **

这里我们再看一下前面展示的项目结构

```
www
├── default.conf 
├── Dockerfile
├── html
│   ├── coalball
│   ├── index.html
│   ├── index.php
│   └── mysql.php
├── mysql
│   ├── coalball.sql
├── php.ini
└── www.conf
```

`Dockerfile`如下

```
FROM php:5.6-fpm

ADD www.conf   /usr/local/etc/php-fpm.d/www.conf
ADD php.ini    /usr/src/php/php.ini

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql

EXPOSE 9000
```
依旧先删除之前的`php-fpm`容器

```
$ docker stop php-fpm
$ docker rm php-fpm

# 构建 运行
# 进入项目的目录,比如我的www文件夹就是建在/home/username下的

$ cd ~/www
$ docker build -t php-fpm:v1 ./
$ docker run --name php-fpm -p 9000:9000 --link mysql:mysql -v ~/www/html:/var/www/html -v ~/www/www.conf:/usr/local/etc/php-fpm.d/www.conf -v ~/www/php.ini:/usr/local/etc/php/php.ini -d php:fpm

即可
```

当然具体需要哪些扩展还是根据自己的需求来编写`Dockerfile`。

***************

###  ** 结合thinkphp **

前面的内容就基本搭建好了开发环境,这里我仅仅谈跑tp项目遇到一些坑(包括一些容器内的坑),做些记录与分享

** <span class="under0">因为这部分踩的坑比较多,或许记得不太清楚,仅作参考,文末会留下一些参考链接</span> **

#### ** How to install the locate command? **

如果**<span class="under0"> 在容器中 </span>**下载东西失败,且提示没有`locate`命令

```
$ apt-get update
$ apt-get install mlocate
```
然而此时执行`locate`寻找一些文件还会有些问题

#### ** locate: can not stat () `/var/lib/mlocate/mlocate.db': No such file or directory **

更新下数据库

```
$ updatedb

# 一次不行的话，多执行几次该命令
```
**********

#### ** Undefined class constant 'MYSQL_ATTR_INIT_COMMAND' **

修改配置文件`php.ini`

把以下这几项配置都开启,如果你的配置文件(php.ini)中没有,自行添加
```
extension=php_mysqli.dll
extension=php_pdo.dll
extension=php_pdo_mysql.dll
extension=pdo.so
extension=pdo_mysql.so

# 如果pdo_mysql扩展安装失败 
可以执行 
docker-php-ext-install pdo_mysql
```


#### ** No such file or directory **
如果访问站点,出现这个错误,可以看看你的phpinfo页面,是否

![pdo](/img/docker/phpNgxinMysql/pdo.png)

`pdo_mysql.default_socket`是否有`Ｌocal Value` 和 `Ｍaster Value`

没有的话,先进入mysql容器中的mysql

```
$ docker exec -it mysql bash
$ mysql -u root -p
# enter your password
```

执行
`mysql> STATUS;`

![mysql](/img/docker/phpNgxinMysql/mysql.png)

记录下`UNIX socket`的值

在你的`php.ini`文件将以下的几项配置为`UNIX socket`的值,没有自行添加
```
pdo_mysql.default_socket
mysql.default_socket
mysqli.default_socket

## 示范
mysqli.default_socket = /var/run/mysqld/mysqld.sock
```

倘若还有问题,可以参考下[stackoverflow上的这个问题](https://stackoverflow.com/questions/22188026/sqlstatehy000-2002-no-such-file-or-directory)

```
### 这里可以跳过,个人记录
creating a symbolic link in: /var/mysql (create the directory if it does not exist)
cd /var/mysql && sudo ln -s /Applications/MAMP/tmp/mysql/mysql.sock

This fixed it for me. I'm not using MAMP though, so it was cd /var/mysql && sudo ln -s /tmp/mysql.sock
```
***************
### ** SQLSTATE[HY000]: General error **
### ** SQLSTATE[HY000] [2002] **
### ** SQLSTATE[HY000] [2002] Connection refused **

最后如果项目出现了这类问题,还需要修改项目配置文件的有关数据的配置

`'DB_HOST'=>'xxx',//数据服务器地址`

** <span class="under0">如果用的是虚拟主机,容器的话，'DB_HOST' => '',这一项应该填数据库的主机地址，而不是本机地址的localhost或者127.0.0.1 </span>**

```
执行
docker inspect --format='{{.NetworkSettings.IPAddress}}' $CONTAINER_ID

即可获得容器IP

但是容器的ip每次启动都会改变，知道容器ip没什么意义！ 
但是容器的ip每次启动都会改变，知道容器ip没什么意义！ 
但是容器的ip每次启动都会改变，知道容器ip没什么意义！ 
```
这样配置即可,前提是你的容器命名为mysql
```
 'DB_HOST'=>'mysql',//数据服务器地址
```
***************

### ** 写在最后 **

以上就是搭建的大致记录。

当然可以自己写一份`docker-compose.yml`使整个搭建过程自动化起来,只需要敲击几个命令即可,必行每次写shell也挺麻烦的。因为时间原因,这儿我就没写了。

也可以发布成镜像,这样就可以一次搭建环境,永久使用了,下次重装了系统,拉取下即可。
**************

[Docker部署LNMP完整教程](https://www.awaimai.com/728.html)
[Docker在PHP项目开发环境中的应用](http://avnpc.com/pages/build-php-develop-env-by-docker)
[tar.xz如何解压:linux和windows下tar.xz解压命令介绍](http://www.169it.com/article/9024845268002546255.html)
[locate: can not stat () `/var/lib/mlocate/mlocate.db': No such file or directory](http://blog.csdn.net/w13770269691/article/details/6987384)
[Mac下PHP连接MySQL报错＂No such file or directory＂的解决办法](http://www.linuxidc.com/Linux/2012-12/76150.htm)
[SQLSTATE[HY000] [2002] No such file or directory [duplicate]](https://stackoverflow.com/questions/22188026/sqlstatehy000-2002-no-such-file-or-directory)
[宿主机上如何获得 docker container 容器的 ip 地址？](https://segmentfault.com/q/1010000001637726)
[如何获取 docker 容器(container)的 ip 地址](https://mozillazg.github.io/2016/01/docker-get-containers-ip-address.html)
