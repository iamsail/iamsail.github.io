---
title: kill不掉mysqld
date: 2018-5-19 23:57:45
categories: 数据库
tags: [MySQL]
---

### ** Preface **

以前想停止mysql服务,都是执行类似如此的命令`service mysql stop`。前阵子某次操作我试图kill -9 掉mysqld,但是`mysqld`始终都是存在的。

经过一番搜索,在[这儿](https://askubuntu.com/questions/529302/how-to-stop-mysqld-process)找到了答案:


The mysql Upstart configuration has the respawn option:


```
grep respawn /etc/init/mysql.conf

respawn
respawn limit 2 5
        elif echo $statusnow | grep -q 'respawn/' ; then
```
 
The respawn option tells Upstart to restart the process if it exits or is killed. The limit is 2, so you can try killing of the processes twice, which will tell Upstart not to start them again, or use: `sudo service mysql stop`


respawn会告诉upstart重启mysqld进程当它退出或者被kill掉。这个限制是2,所以可以通过连续的两次kill或者使用`sudo service mysql stop`

不过我连续两次的kill或者更多次,是没有kill掉mysqld的。

另外在[这个帖子](https://serverfault.com/questions/526554/mysql-process-wont-die)看到了另一个回答,贴下

The mysql server runs with 2 processes, mysqld and mysqld_safe. If you kill mysqld with the SIGKILL signal (9), mysqld_safe will respawn mysqld. If you stop mysqld in the standard way, or kill it with the sigint(15) signal, mysqld_safe notices it and ends. If there is an emergency, remember always to kill -9 mysqld_safe first.

In this case, it seems that mysqld_safe is restarting just after shutdown. How are you exactly killing mysql?


`mysql`服务运行的时候有两个进程分别是`mysqld`和`mysqld_safe`。当你9杀的时候,`mysqld_safe`会重启`mysqld`.如果你以一种标准的方式来停止`mysqld`,或者以信号量15(SIGTERM)来kill,mysqld_safe将会退出。紧急情况下,记得要先9杀掉`mysqld_safe`。

*********************
### ** Linux信号 **

#### ** 信号本质 **
软中断信号（signal，又简称为信号）用来通知进程发生了异步事件。在软件层次上是对中断机制的一种模拟，在原理上，一个进程收到一个信号与处理器收到一个中断请求可以说是一样的。信号是进程间通信机制中唯一的异步通信机制，一个进程不必通过任何操作来等待信号的到达，事实上，进程也不知道信号到底什么时候到达。进程之间可以互相通过系统调用kill发送软中断信号。内核也可以因为内部事件而给进程发送信号，通知进程发生了某个事件。信号机制除了基本通知功能外，还可以传递附加信息。

每种信号用一个整型常量宏表示，以`SIG`开头，比如`SIGCHLD`、`SIGINT`等，它们在系统头文件中定义。

*********************

通过`kill -l`命令可以查看系统支持的所有信号：
```
> kill -l

HUP INT QUIT ILL TRAP ABRT BUS FPE KILL USR1 SEGV USR2 PIPE ALRM TERM STKFLT CHLD CONT STOP TSTP TTIN TTOU URG XCPU XFSZ VTALRM PROF WINCH POLL PWR SYS
```

`SIGTERM`(15)和`SIGKILL`(9)。 `SIGTERM`比较友好，进程能捕捉这个信号， 根据您的需要来关闭程序。在关闭程序之前，您可以结束打开的记录文件和完成正在做的任务。 在某些情况下， 假如进程正在进行作业而且不能中断，那么进程可以忽略这个`SIGTERM`信号。

对于`SIGKILL`信号，进程是不能忽略的。 这是一个 '“我不管您在做什么,立刻停止”'的信号。

更多可以看下这篇文章[SIGTERM vs. SIGKILL](https://major.io/2010/03/18/sigterm-vs-sigkill/)

*********************

### ** 守护进程 **


守护进程一般在系统启动时开始运行，除非强行终止，否则直到系统关机都保持运行。守护进程经常以超级用户（root）权限运行，因为它们要使用特殊的端口（1-1024）或访问某些特殊的资源。

一个守护进程的父进程是init进程，因为它真正的父进程在fork出子进程后就先于子进程exit退出了，所以它是一个由init继承的孤儿进程。守护进程是非交互式程序，没有控制终端，所以任何输出，无论是向标准输出设备stdout还是标准出错设备stderr的输出都需要特殊处理。

守护进程的程序命名通常在最后加一个 “d”。 BIND 是伯克利互联网域名服务 (而实际执行的程序名称则是 named)， Apache web系统的程序就叫 httpd， 在行式打印机上的打印守护进程就是 lpd。 这只是一种惯例，不是标准或硬性规定。 例如，为Sendmail而应用的主要mail守护进程就叫sendmail， 却不叫maild，这和您推测的一样。

查看守护进程
```
ps -eo ppid,pid,sid,stat,tty,comm  | awk '{ if ($2 == $3 && $5 == "?") {print $0}; }'
```


*********************
### ** mysqld_safe **

`cat /usr/bin/mysqld_safe` 

Script to start the MySQL daemon and restart it if it dies unexpectedly

`mysqld_safe` 是mysqld 启动脚本,当`mysqld`不正常死亡,重启它 。

***********************
### ** MySQL 的四种启动方式 **

这部分主要参考了以下几篇文章,贴在这里

[MySQL 数据库的启动与关闭](https://blog.csdn.net/leshami/article/details/40749935)
[MySql在Linux的启动方式](https://blog.csdn.net/alexdamiao/article/details/51498684)

在Linux系统下，MySQL服务器通常有四种启动方式：mysqld守护进程启动，mysqld_safe启动，mysql.server启动，mysqld_multi多实例启动。

#### ** mysqld守护进程启动 **

mysqld是mysql的守护进程，这种方式启动的时候会读取my.cnf文件中的[mysqld]和[server]组中的配置参数。一般的，我们通过这种方式手动的调用mysqld，如果不是出去调试的目的，我们一般都不这样做。这种方式如果启动失败的话，错误信息只会从终端输出，而不是记录在错误日志文件中，这样，如果mysql崩溃的话我们也不知道原因，所以这种启动方式一般不用在生产环境中，而一般在调试（debug）系统的时候用到。
启动方法：

```
./mysqld
```

************************

#### ** mysqld_safe启动 **
这种方式启动的时候会读取my.cnf文件中的[mysqld],[server]和[mysqld_safe]组的配置文件,为了兼容，也会读取[safe_mysqld]这个组内的配置文件。
mysqld_safe是一个启动脚本，该脚本会调用mysqld启动，如果启动出错，会将错误信息记录到错误日志中，mysqld_safe启动mysqld和monitor mysqld两个进程，这样如果出现mysqld进程异常终止的情况，mysqld_safe会重启mysqld进程。
启动方法：

```
./mysqld_safe
```
************************

#### ** mysql.server启动 **
mysql.server同样是一个启动脚本，调用mysqld_safe脚本。它的执行文件在$MYSQL_BASE/share/mysql/mysql.server 和 support-files/mysql.server。

************************

#### ** mysqld_multi多实例启动 **
[mysql dba系统学习（4）mysql的多实例multi启动停止](http://blog.51cto.com/wolfword/1241304)

************************

### ** 其他 **

#查看mysqld启动配置文件的优先级
```
mysqld --verbose --help |grep -A 1 "Default options" 
```
*************************

当MySQL实例启动时，会将自己的进程ID写入一个文件中——该文件即为pid文件。该文件可由参数pid_file控制，默认位于数据库目录下，文件名为主机名.pid：

mysql> show variables like 'pid_file'\G;

************************
### ** 参考 **

[Linux信号（signal) 机制分析](https://www.cnblogs.com/hoys/archive/2012/08/19/2646377.html)
[Linux kill -9 和 kill -15 的区别](http://www.cnblogs.com/yucongblog/p/6568374.html)
[Linux信号机制与信号处理](https://www.jianshu.com/p/9c9b74f6a222)
[MySQL使用kill杀不死](https://blog.csdn.net/hlf1203/article/details/52789685)
[Mysql Process wont die](https://serverfault.com/questions/526554/mysql-process-wont-die)
[MySQL 数据库的启动与关闭](https://blog.csdn.net/leshami/article/details/40749935)
[进程ID](https://zh.wikipedia.org/wiki/%E8%BF%9B%E7%A8%8BID)
[怎样查看mysql pid文件路径 文件位置](https://blog.csdn.net/u010098331/article/details/50786269)
[Linux查找所有正在运行的守护进程（daemon）](https://my.oschina.net/u/158589/blog/351890)
[守护进程daemon的创建和使用](https://my.oschina.net/u/556678/blog/183780)
[Linux 守护进程](https://my.oschina.net/shou1156226/blog/802931)
[UNIX中后台进程与守护进程](https://blog.csdn.net/dlutbrucezhang/article/details/8656680)
[mysqld_safe](https://www.jianshu.com/p/2f4ef40020aa)
[进程kill 失败](https://blog.csdn.net/liukun321/article/details/6918233)
[linux：nohup 命令实现守护进程（屏蔽 SIGHUP 信号）](https://my.oschina.net/sallency/blog/827737)
[SIGKILL](https://zh.wikipedia.org/wiki/SIGKILL)
[How to stop mysqld process?](https://askubuntu.com/questions/529302/how-to-stop-mysqld-process)
[4.8. 守护进程，信号和杀死进程](https://www.freebsd.org/doc/zh_CN/books/handbook/basics-daemons.html)