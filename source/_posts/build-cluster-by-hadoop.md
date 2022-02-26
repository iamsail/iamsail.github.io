---
title: hadoop2.6搭建集群(伪分布式)
date: 2018-07-12 18:58:30
categories: 大数据
tags: [hadoop]
---
### ** Preface **

一直想学学hadoop,不过因为比较忙,一直没开起头。刚好昨天去图书馆还书了,在书架看到了《Hadoop大数据实战权威指南》,就借了下来。也初步搭建了一个集群,后面可以进一步的学习,本文做些记录。

本文不是详细的记录安装细节,主要是为了以后若再次搭建,可以更快些。所以你只看我这篇文章,是比较难搭出来的,具体细节推荐看书或者文档。

![书展示](/img/大数据/build-cluster-by-hadoop/1.jpeg)

*******************
### ** 我的系统环境 **

这本书中介绍的搭建环境是在windows下通过安装linux(centos)虚拟机搭建集群。因为我的开发系统就是`Ubuntu16.04`,所以我就是在`Ubuntu`下搭建的虚拟机(依旧是Ubuntu16),搭的集群。

说来好笑,一开始还在担心是不是linux也是可以安装虚拟机。其实linux也是可以安装虚拟机,比如VMware,VirtualBox。我选用的是VMware14。直接去[官网](https://www.vmware.com/)下载安装就好了

怎么安装虚拟机什么的就不记录了。

******************

### ** 虚拟机克隆安装 **

集群肯定是有多个机器的,对于hadoop,我们最少得有三个机器。如果重复装三次ubuntu肯定是很蠢的,我们安装好第一个(Ubuntu-One)后,就可以通过克隆安装。这里有两种方法

比如我有三个机器,这里我每个虚拟机分配的是4G内存,35

```regexp
Ubuntu-One
Slave0
Slave1
```
#### ** 方法一 **

在VMvare的目录下,复制对应系统的整个目录(Ubuntu-One),然后粘贴,将目录改个名Slave0。然后在VMvare的主页选择Slave0这个目录进行一系列操作就好了。

#### ** 方法二 **

在VMvare主页界面,右键点击`Ubuntu-One`,管理->克隆(Manage->Clone),一系列操作即可。

******************

### ** 集群配置 **

#### ** 修改主机名 **

[ubuntu永久修改主机名](https://blog.csdn.net/ruglcc/article/details/7802077)

这里我三个机器分别命名为

```regexp
master
slave0
slave1
```

如果是centos系统，执行`gedit /etc/sysconfig/network`
输入以下代码
```
NETWORKING=yes
HOSTNAME=master
```

如果是ubuntu系统,执行`gedit /etc/hostname`

输入

```
master
```
master是用户自己取的主机名,可以根据需要任意命名。
  
修改完成后,保存文件。在终端执行`hostname master`,确认修改生效。关闭终端,再打开一个新的终端,执行`hostname`，进行确认是否生效。重复以上方法,修改另外两个虚拟机为`slave0`,`slave1`.
*****************

#### ** 网络设置 **

在终端输入`ifconfig`命令,`inet`后面跟的数字就是IP地址。根据IP地址,可以虚拟机之间互相ping,有返回值则说明机器是连通的。

上面这个只是简单的采用了系统安装时配置的网络IP,实际上，上述地址一般都是DHCP类型的。由于我们目前网络里并没有DHCP服务器,因此,需要将动态主机IP地址修改为静态地址。在虚拟机的设置中找到网络设置,然后将网络状态的ON切换为OFF。注意,修改网络地址需要事先断掉网络连接。

然后选择IPV4,接着选择Manual,然后增加静态地址信息。这里,设置的地址是192.168.1.100，子网掩码是255.255.255.0，网关地址是192.168.1.1。slave0,1的地址分别是192.168.1.101,192.168.1.102.子网掩码和网关地址相同。

这样我们就完成了整个集群的网络配置。可以使用ping进行测试。然而,为了用计算机名进行网络访问，我们还需要修改hosts文件中的主机名和IP地址对照裂变。注意,需要在root用户下操作。
`gedit /etc/hosts`

然后输入如下代码
```
192.168.1.101 master
192.168.1.102 slave0
192.168.1.101 slave1
```

以上操作需要在所有主机上进行。然后就可以用主机名代替IP地址了,比如`ping slave0`
******************

#### ** 关闭防火墙 **

大数据应用系统通常部署在linux集群上,一般属于内部网络平台,且计算机之间关系紧密,通信频繁,所以不需要开启防火墙。

如果是centos系统,防火墙相关操作如下

```
# 查看当前防火墙状态
systemctl status firewalld.service

# 关闭防火墙
systemctl stop firewalld.service

# 一般在关闭防火墙过后,还可以执行如下命令,该命令使防火墙在下次启动计算机时取消防火墙服务
systemctl status firewalld.service
```
如果是ubuntu系统,防火墙相关操作,看这篇文章[ubuntu 默认防火墙安装、启用、查看状态](https://www.cnblogs.com/OnlyDreams/p/7210914.html)

******************

#### ** 安装JDK **

hadoop是基于JAVA环境的,所以必须安装JDK.这里我使用的是jdk-7u71-linux-x64.gz压缩包.

我们在`/usr`目录下创建java目录,即`/usr/java`.然后在该目录下进行解压

```
tar -zxvf jdk-7u71-linux-x64.gz
```

接着开始配置环境变量,`gedit /home/sail/.profile`,新增代码如下

```
# set PATH so it includes user's private bin directories
PATH="$HOME/bin:$HOME/.local/bin:$PATH"

# 以下是新增的代码
export JAVA_HOME=/usr/java/jdk1.7.0_71/
export PATH=$JAVA_HOME/bin:$PATH

```
这里的`/usr/java/jdk1.7.0_71/`就是java安装文件夹。接着执行`source .profile`使其生效,`java -version`进行检查。

这里罗嗦下,`source .profile`执行后,关闭终端后重新打开,检查版本就是找不到的,要重启计算机才生效。在ubuntu下还有个`.bashrc`文件，如果是修改这个文件而不是profile,应该不会这种情况。不过我没有测试过。如果是`centos`系统的话,则应该修改`~/.bash_profile`文件。

这里其他两个虚拟机也需要执行以上操作。当然如果是老司机,应该清楚,我们可以配置好一台机器,然后其他机器直接复制就可以了。
******************

#### ** 免密钥登录配置 **
免密钥登录是指两台linux机器之间ssh连接时不需要用户名和密码。下面的配置分为在master和所有slave节点操作。同时是以普通用户,非root进行操作的.

##### ** Master节点的配置 **
在终端`~/`目录下,执行命令`ssh-keygen -t rsa`,一路回车即可。

`ssh-keygen`是用来生成private和public的密钥对,将public密钥拷贝到远程机器后,就可以使用ssh到另外一台机器不用密码了。`-t`是指定加密算法,这里是rsa。生成的密钥在.ssh目录下

接下来执行 `cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys`，这是一个复制操作。复制过后是为了便于修改文件权限,接下来执行`chmod 600 ~/.ssh/authorized_keys`,然后将这个文件复制到所有的slave节点。

```
scp ~/.ssh/authorized_keys sail@slave0:~/

scp ~/.ssh/authorized_keys sail@slave1:~/
```
然后输入yes,就完成了在master节点的配置
**********************

##### ** Slave节点的配置 **
在`~/`目录下执行`ssh-keygen -t rsa`,一路回车

接着将从master复制过来的authorized_keys复制到.ssh目录,`mv authorized_keys ~/.ssh`

然后修改权限,`chmod 600 ~/.ssh/authorized_keys`。以上操作要在两个slave节点均做.至此,配置完毕。

在master执行`ssh slave0`，若登录成功，且不需要输入密码,即证明配置成功。`exit`,回到本地计算机。

*******************
### ** Hadoop HDFS安装与配置 **

#### ** 解压 **
这里我用的是`hadoop-2.6.0.tar.gz`。先解压到用户目录,`tar -zxvf ~/hadoop-2.6.0.tar.gz`

******************
#### ** 配置hadoop环境变量 **
`gedit ~/hadoop-2.6.0/etc/hadoop/hadoop-env.sh`,修改为如下

```
# The java implementation to use.
export JAVA_HOME=/usr/java/jdk1.7.0_71/
```
********************

#### ** 配置yarn环境变量 **
`gedit ~/hadoop-2.6.0/etc/hadoop/yarn-env.sh`,修改为如下

```
# some Java parameters
# export JAVA_HOME=/home/y/libexec/jdk1.6.0/
export JAVA_HOME=/usr/java/jdk1.7.0_71/
```
*********************
#### ** 配置核心组件文件 **
`gedit ~/hadoop-2.6.0/etc/hadoop/core-site.xml`,修改为如下

```
<configuration>
 <property>
     <name>fs.defaultFS</name>
     <value>hdfs://master:9000</value>
 </property>
 <property>
	 <name>hadoop.tmp.dir</name>
	 <value>/home/sail/hadoopdata</value>
 </property>
</configuration>
```
******************

#### ** 配置文件系统 **
`gedit ~/hadoop-2.6.0/etc/hadoop/hdfs-site.xml`,修改为如下

```
<configuration>
 <property>
    <name>dfs.replication</name>
	<value>1</value>
 </property>
</configuration>
```
******************

#### ** yarn-site.xml **
`gedit ~/hadoop-2.6.0/etc/hadoop/yarn-site.xml`,修改为如下

```regexp
<configuration>
    <property>
	    <name>yarn.nodemanager.aux-services</name>
		<value>mapreduce_shuffle</value>
	</property>
	<property>
		<name>yarn.resourcemanager.address</name>
		<value>master:18040</value>
	</property>
	<property>
	    <name>yarn.resourcemanager.scheduler.address</name>
	    <value>master:18030</value>
	</property>
	<property>
	    <name>yarn.resourcemanager.resource-tracker.address</name>
		<value>master:18025</value>
	</property>
	<property>
	    <name>yarn.resourcemanager.admin.address</name>
		<value>master:18141</value>
	</property>
	<property>
	    <name>yarn.resourcemanager.webapp.address</name>
		<value>master:18088</value>
	</property>
    <!-- Site specific YARN configuration properties -->
</configuration>
```
******************
#### ** 配置MapReduce 计算框架文件 **

先执行如下两行
```
cd ~/hadoop-2.6.0/etc/hadoop/
cp mapred-site.xml.template mapred-site.xml`
```

然后,`gedit mapred-site.xml`。修改如下

```regexp
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```
******************
#### ** 配置Master的slaves文件 **

slaves文件给出集群的slave节点。启动hadoop时,根据该文件启动集群,不在列表的slave节点不会被视为计算节点

`gedit ~/hadoop-2.6.0/etc/hadoop/slaves`,修改为如下

```regexp
slave0
slave1
```

******************
#### ** 复制Master上的hadoop到salve节点 **

```regexp
scp -r /home/sail/hadoop-2.6.0 sail@slave0:~/
scp -r /home/sail/hadoop-2.6.0 sail@slave1:~/
```
至此,我们就完成了hadoop集群的安装与配置

*****************

### ** Hadoop集群的启动 **

#### ** 配置操作系统环境变量 **

由于是在Linux集群上安装的hadoop集群,所以自然需要配置Linux系统平台的环境变量。注意,这里的配置需要在集群所有计算机上进行。

```regexp
cd ~
vim .profifle

#增加如下代码到文件尾部
export HADOOP_HOME=/home/sail/hadoop-2.6.0
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH
```
执行`source .profile`,使上述配置生效。没有生效的话重启下计算机就能生效了。

******************
#### ** 创建hadoop数据目录 **

在用户目录下(~),创建数据目录,`mkdir /home/sail/hadoopdata`

这里的数据目录名`hadoopdata`，与前面的hadoop核心组件`core-site.xml`中的配置
```
<property>
	 <name>hadoop.tmp.dir</name>
	 <value>/home/sail/hadoopdata</value>
</property>
```
是一致的

******************
#### ** 格式化文件系统 **

该操作只需要在master节点进行,在用户目录下(~)执行即可

```
hdfs namenode -format
```
******************
#### ** 启动和关闭hadoop **
到此,就可以启动hadoop了,进入hadoop的安装目录,执行`sbin/start-all.sh`即可以启动。如果要关闭,则执行`stop-all.sh`命令即可

`This script is Deprecated. Instead use start-dfs.sh and start-yarn.sh`

会提示`start-all.sh`这个命令已经被抛弃了,推荐使用`start-dfs.sh`和`start-yarn.sh`

******************
#### ** 验证hadoop是否启动成功 **

在master节点,执行`jps`命令,如果显示以下四个进程，则表示主节点(Master)启动成功

```
3202 SecondaryNameNode
3001 NameNode
3344 ResourceManager
3600 Jps

```
在从节点(slavex),执行`jps`,若显示以下三个进程,则表示启动成功

```
2374 Jps
2102 DataNode
2237 NodeManager
```


******************
### ** 参考 **

[Ubuntu 16.04 安装 VMware Workstation(虚拟机)](http://blog.topspeedsnail.com/archives/6649)
[VMware Workstation 14永久激活密钥](https://blog.csdn.net/qq_26954773/article/details/78128662)
[linux下VMware安装出现的问题解决](https://www.cnblogs.com/oloroso/p/4612935.html)
[Ubuntu 16.04 安装 qBittorrent－BT下载](http://blog.topspeedsnail.com/archives/6650)
[How do you get BitTorrent on Ubuntu?](https://askubuntu.com/questions/861023/how-do-you-get-bittorrent-on-ubuntu)
[ubuntu永久修改主机名](https://blog.csdn.net/ruglcc/article/details/7802077)
[从VMware虚拟机安装到hadoop集群环境配置详细说明](https://blog.csdn.net/whaoXYSH/article/details/17755555)
[子网掩码,如255.255.255.0\24， 24代表什么?](https://blog.csdn.net/Qiuzhongweiwei/article/details/80172270)
[Ubuntu16.04 配置环境变量的三种方法](https://blog.csdn.net/Bleachswh/article/details/51334661)
[ubuntu 默认防火墙安装、启用、查看状态](https://www.cnblogs.com/OnlyDreams/p/7210914.html)
[关于ssh: connect to host master port 22: Connection timed out问题的总结](https://blog.csdn.net/u010842515/article/details/52484404)
[ssh: connect to host slave2 port 22: Connection refused](https://blog.csdn.net/s646575997/article/details/51227976)
[ubuntu 环境变量 失效的解决办法](https://blog.csdn.net/u012146107/article/details/11766797)
[Ubuntu修改环境变量关掉终端就没了，问题解决办法](https://blog.csdn.net/zdw_zoro/article/details/78052600)
