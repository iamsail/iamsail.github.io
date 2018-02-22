---
title: docker搭建nginx+php+mysql开发环境
date: 2017-09-23 16:43:20
categories: Docker
---

### ** 写在前面 **

本文是对`docker`搭建`nginx+php+mysql`开发环境的记录。

主要都是参考了[这篇文章](http://www.tanhui.bid/docker/2016/10/19/%E4%BD%BF%E7%94%A8Docker-docker-compose-%E6%90%AD%E5%BB%BAnginx+php+mysql-%E7%8E%AF%E5%A2%83)。

因为这篇博客写得特别好,特意搬迁到自己的博客,当然在原文基础上增加了一些内容。
*********

主要使用了两种方式搭建环境。分别是自己写`shell`和利用`docker-compose`。

### ** 第一种 **

#### ** MySQL **

获取MySQL 直接使用官方镜像,输入以下命令
```
docker pull mysql:5.6
```
运行MySQL
```
docker run -p 3306:3306 --name test_mysql -v $PWD/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d --privileged=true mysql:5.6



### 命令说明：

-p 3306:3306：将容器的3306端口映射到主机的3306端口
-v PWD/mysql/data:/var/lib/mysql：将主机当前目录下的mysql/data文件夹挂载到容器的/var/lib/mysql 下，在mysql容器中产生的数据就会保存在本机mysql/data目录下
-e MYSQL_ROOT_PASSWORD=123456：初始化root用户的密码
-d 后台运行容器
--name 给容器指定别名
--privileged=true  可能会碰到权限问题，需要加参数
```

执行以下命令进入mysql 运行环境

```
docker exec -it test_mysql bash

这样就进入mysql容器了，可以查看mysql 命令
mysql －u root -p
输入密码就可以操作数据库
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.07 sec)
mysql> create database if not exists test_db;
Query OK, 1 row affected, 1 warning (0.00 sec)

mysql> use test_db
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> create table people (name varchar(10), age int);
Query OK, 0 rows affected (0.13 sec)

mysql> insert into people values('liming',10);
Query OK, 1 row affected (0.03 sec)
```

#### ** PHP **


PHP 同样使用官方的php镜像，不过需要支持mysql扩展。所以我们这次用Dockerfile 来构建一个镜像，以下是Dockerfile
````
 FROM  php:5.6-fpm
 RUN apt-get update && apt-get install -y \
 libfreetype6-dev \
 libjpeg62-turbo-dev \
 libpng12-dev \
 vim \
 && docker-php-ext-install pdo_mysql \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && docker-php-ext-install gd \
```

我们在原本的php5.6上安装了一些工具以及扩展。

build 我们新建的镜像
```
docker build -t="php-fpm5.6/v2" .
```
然后用这个镜像跑一个php环境的容器
```
docker run -d -p 9000:9000 -v /home/sail/codelife/code/be/php/:/var/www/html/ --name php-with-mysql --link test_mysql:mysql  --volumes-from test_mysql --privileged=true php-fpm5.6/v2

### 参数解析

－v 将本地磁盘上的php代码挂载到docker 环境中，对应docker的目录是 /var/www/html/
--name 新建的容器名称 php-with-mysql
--link 链接的容器，链接的容器名称：在该容器中的别名，运行这个容器是，docker中会自动添加一个host识别被链接的容器ip
--privileged=true 权限问题

```


进入容器
```
docker exec -it php-with-mysql bash
cd /var/www/html && ls
```

这里就会看到你本地磁盘下所挂载的文件,在该目录下可以添加一个 `mysql.php` 文件，如下
```
try {
    $dbh = new PDO('mysql:host=mysql;dbname=test_db', 'root','12
3456');
    foreach($dbh->query('SELECT * from people') as $row) {
        print_r($row);
    }
    $dbh = null;
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}

```
退出编辑
```
root@f5c9b982690a:/var/www/html# php mysql.php
Array
(
    [name] => liming
    [0] => liming
    [age] => 10
    [1] => 10
)
```

输出结果如上，这样我们php链接mysql就成功了。

#### ** Nginx **

安装Nginx镜像

```
$ docker pull nginx
```

本地编辑nginx配置文件 default.conf 绝对路径为（/home/tanhui/composeTest/nginx/conf/default.conf） 文件内容如下

```
server {
    listen       80;
    server_name  localhost;

    location / {
        root   /var/www/html;
        index  index.html index.htm index.php; # 增加index.php
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /var/www/html;
    }
    location ~ \.php$ {
        root           /var/www/html; # 代码目录
        fastcgi_pass   phpfpm:9000;    # 修改为phpfpm容器
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name; # 修改为$document_root
        include        fastcgi_params;
    }
}

```
### 运行容器
```
docker run -d --link php-with-mysql:phpfpm --volumes-from php-with-mysql -p 81:80 -v /home/sail/codelife/code/be/nginx/conf/default.conf:/etc/nginx/conf.d/default.conf --name nginx-php --privileged=true

### 参数解析
--link php-with-mysql:phpfpm 将php容器链接到nginx容器里来，phpfpm是nginx容器里的别名。
--volumes-from php-with-mysql 将php-with-mysql 容器挂载的文件也同样挂载到nginx容器中
-v /home/sail/codelife/code/be/nginx/conf/default.conf:/etc/nginx/conf.d/default.conf  将nginx 的配置文件替换，挂载本地编写的配置文件

docker exec -it nginx-php bash
root@32de01dbee49:/# cd /var/www/html/&&ls
  mysql.php
```

我们可以看到挂载在php－mysql容器里的文件夹同样也被挂载在nginx容器里，这时在本机方案127.0.0.1：81/mysql.php,数据库中的数据就在浏览器上输出了。 这样 nginx＋php＋mysql 的连接就基本完成了。

*********

### ** 方法二 **

上面介绍了用纯docker 命令启动容器，链接容器，但是每次启动容器时都要填写一堆参数，难免容易出错，出错了之后还要删除该容器才能重新跑。接下来就介绍一下 `docker-compose.`

### ** Docker Compose **

`Docker Compose 是 Docker 官方编排（Orchestration）项目之一，负责快速在集群中部署分布式应用。

`Compose` 定位是 “定义和运行多个 Docker 容器的应用`（Defining and running multi-container Docker applications）`”，其前身是开源项目 Fig，目前仍然兼容 Fig 格式的模板文件。

在日常工作中，经常会碰到需要多个容器相互配合来完成某项任务的情况。例如要实现一个 Web 项目，除了 Web 服务容器本身，往往还需要再加上后端的数据库服务容器，甚至还包括负载均衡容器等。

`Compose` 恰好满足了这样的需求。它允许用户通过一个单独的 `docker-compose.yml` 模板文件（YAML 格式）来定义一组相关联的应用容器为一个项目`（project）`。

`Compose` 中有两个重要的概念：

`服务（service）`：一个应用的容器，实际上可以包括若干运行相同镜像的容器实例。
项目(project)：由一组关联的应用容器组成的一个完整业务单元，在 `docker-compose.yml` 文件中定义。
`Compose` 的默认管理对象是项目，通过子命令对项目中的一组容器进行便捷地生命周期管理。

`Compose` 项目由 `Python` 编写，实现上调用了 Docker 服务提供的 API 来对容器进行管理。因此，只要所操作的平台支持` Docker API`，就可以在其上利用 Compose 来进行编排管理。

#### ** 安装 **

```
$ sudo pip install -U docker-compose
```

可以看到类似如下输出，说明安装成功

```
Collecting docker-compose
  Downloading docker-compose-1.8.0.tar.gz (149kB): 149kB downloaded
...
Successfully installed docker-compose cached-property requests texttable websocket-client docker-py dockerpty six enum34 backports.ssl-match-hostname ipaddress
```

安装成功后，可以查看 `docker-compose` 命令的用法
```
$ docker-compose -h
Define and run multi-container applications with Docker.

Usage:
  docker-compose [-f=<arg>...] [options] [COMMAND] [ARGS...]
  docker-compose -h|--help

Options:
  -f, --file FILE           Specify an alternate compose file (default: docker-compose.yml)
  -p, --project-name NAME   Specify an alternate project name (default: directory name)
  --x-networking            (EXPERIMENTAL) Use new Docker networking functionality.
                            Requires Docker 1.9 or later.
  --x-network-driver DRIVER (EXPERIMENTAL) Specify a network driver (default: "bridge").
                            Requires Docker 1.9 or later.
  --verbose                 Show more output
  -v, --version             Print version and exit

Commands:
  build              Build or rebuild services
  help               Get help on a command
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pulls service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  unpause            Unpause services
  up                 Create and start containers
  migrate-to-labels  Recreate containers to add labels
  version            Show the Docker-Compose version information
```
`Compose`的默认配置文件是`docker-compose.yml`。让我们看看下面这个文件：

```
nginx:
  build: ./nginx
  ports:
    - "81:80"
  links:
    - "phpfpm"
  volumes:
    - /home/sail/codelife/code/be/php:/var/www/html/
    - /home/sail/codelife/code/be/nginx/conf/default.conf:/etc/nginx/conf.d/default.conf
phpfpm:
  build: ./phpfpm
  ports:
    - "9000:9000"
  volumes:
    - ./code/:/var/www/html/
  links:
    - "mysql"
mysql:
  build: ./mysql
  ports:
    - "3306:3306"
  volumes:
    - /home/sail/mysql/data/:/var/lib/mysql/
  environment:
    MYSQL_ROOT_PASSWORD : 123456

```

以上的配置文件路径有绝对路径,有相对路径,`build `参数代表该路径下的`Dockerfile `先看一下大概的目录结构

```
$ tree composeTest
composeTest
├── code
│   ├── index.php
│   ├── mysql.php
│   └── testmysql.php
│
├── docker-compose.yml
├── index.php
├── mysql
│   ├── data
│   │   ├── auto.cnf
│   │   ├── ibdata1
│   │   ├── ib_logfile0
│   │   ├── ib_logfile1
│   │   ├── mysql [error opening dir]
│   │   ├── performance_schema [error opening dir]
│   │   └── test_db [error opening dir]
│   └── Dockerfile
├── nginx
│   ├── conf
│   │   └── default.conf
│   └── Dockerfile
└── phpfpm
    └── Dockerfile

10 directories, 23 files

// Dockerfile 如下
$ cat composeTest/mysql/Dockerfile
FROM mysql:5.6

# tanhui @ localhost in ~ [20:57:51]
$ cat composeTest/phpfpm/Dockerfile
 FROM  php:5.6-fpm
 RUN apt-get update && apt-get install -y \
 libfreetype6-dev \
 libjpeg62-turbo-dev \
 libpng12-dev \
 vim \
 && docker-php-ext-install pdo_mysql \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && docker-php-ext-install gd \

# tanhui @ localhost in ~ [20:58:19]
$ cat composeTest/nginx/Dockerfile
FROM nginx:latest
RUN apt-get update && apt-get install -y vim

```
现在运行这三个容器只要使用命令 `docker-compose up -d`




*********

### ** 参考 **

[Docker Compose 配置文件详解](http://www.jianshu.com/p/2217cfed29d7)
[Docker docker-compose 配置Nginx+Php+Mysql开发环境](http://www.tanhui.bid/docker/2016/10/19/%E4%BD%BF%E7%94%A8Docker-docker-compose-%E6%90%AD%E5%BB%BAnginx+php+mysql-%E7%8E%AF%E5%A2%83)
[Docker —— 从入门到实践](https://www.gitbook.com/book/yeasy/docker_practice/details)
**********


<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
