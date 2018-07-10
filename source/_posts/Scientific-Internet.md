---
title: 不可描述
date: 2018-06-24 18:34:30
categories: 不可描述
password: Scientific,  
---
### ** Preface **

从昨天开始就ssh不上[vultr](https://www.vultr.com/)的服务器了,工作室同学也连接不上。估计是被封了。希望过段时间能够恢复吧,毕竟我充的钱还没用完23333。

然后我现在用回了学叔[提供的服务](https://fadsfasdfsdaf.darkerthanblack.org),他是用的DO(水滴)。

我的操作系统是`ubuntu16.04`,之前我用的是ssr,学叔这个是ss。恰恰今天折腾ss踩了坑,本文坐下记录。

******************
#### ** 安装ss **

首先是安装

```regexp
sudo apt-get install python-pip // 安装PIP，用它来安装ss
sudo pip install shadowsocks    // 安装ss
```

然后是进行配置

在`/etc/ss.json`

```regexp
{
    "server": "xxxxx",
    "server_port": xxxxx,
    "local_address": "127.0.0.1",
    "local_port": 1080,
    "password": "xxxxxx",
    "method": "aes-256-cfb",
    "remarks": "", 
    "timeout": 120 
}   
```

然后就是启动

```regexp
sslocal -c /etc/ss.json
```
or 

```regexp
nohup sslocal -c /etc/ss.json >/dev/null &
```
******************
### ** Bug解决　**

然后就是这里,遭遇了一个bug,心痛

** 解决`openssl`升级到`1.1.0`以上版本，导致启动报`undefined symbol: EVP_CIPHER_CTX_cleanup`错误。**

`error`如下

```regexp
AttributeError: /usr/local/ssl/lib/libcrypto.so.1.1: undefined symbol: EVP_CIPHER_CTX_cleanup
```
#### ** 解决如下 **

vim打开文件`openssl.py`

```regexp
# 路径不同根据报错路径而定
vim /usr/local/lib/python3.5/dist-packages/shadowsocks/crypto/openssl.py
```

修改`libcrypto.EVP_CIPHER_CTX_cleanup.argtypes`
```regexp
:%s/cleanup/reset/
:x
# 以上两条为VIM命令， 替换文中libcrypto.EVP_CIPHER_CTX_cleanup.argtypes 为libcrypto.EVP_CIPHER_CTX_reset.argtypes 共两处，并保存
```
运行Shadowsocks,即可

****************
### ** 原因：**
这个问题是由于在`openssl1.1.0`版本中，废弃了`EVP_CIPHER_CTX_cleanup`函数，如官网中所说：
```regexp
EVP_CIPHER_CTX was made opaque in OpenSSL 1.1.0. As a result, EVP_CIPHER_CTX_reset() appeared and EVP_CIPHER_CTX_cleanup() disappeared. EVP_CIPHER_CTX_init() remains as an alias for EVP_CIPHER_CTX_reset().

#EVP_CIPHER_CTX_reset函数替代了EVP_CIPHER_CTX_cleanup函数
```
EVP_CIPHER_CTX_reset函数说明：
```regexp
EVP_CIPHER_CTX_reset() clears all information from a cipher context and free up any allocated memory associate with it, except the ctx itself. This function should be called anytime ctx is to be reused for another EVP_CipherInit() / EVP_CipherUpdate() / EVP_CipherFinal() series of calls.
```

`EVP_CIPHER_CTX_cleanup`函数说明：
```regexp
EVP_CIPHER_CTX_cleanup() clears all information from a cipher context and free up any allocated memory associate with it. It should be called after all operations using a cipher are complete so sensitive information does not remain in memory.
```

** 可以看出，二者功能基本上相同，都是释放内存，只是应该调用的时机稍有不同，所以用`reset`代替`cleanup`问题不大。**



最后成功的时候启动应该如下的:

```regexp
{} ~ sslocal -c /etc/ss.json
INFO: loading config from /etc/ss.json
2018-06-24 18:46:43 INFO     loading libcrypto from libcrypto.so.1.1
2018-06-24 18:46:43 INFO     starting local at 127.0.0.1:1080

```
*******************
### ** vultr搭建 **

[vultr](https://www.vultr.com/)又恢复了,我对搭建的过程做个记录。学叔用的是水滴搭建的。

******************

### ** 安装SSR **

执行以下命令

`wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh`

*************

如提示

`wget :command not found`

*************

请执行

`yum install wget -y`

******************

### ** 破解版锐速安装 **
一键更换内核脚本（Vultr需先执行此脚本）

`wget -N --no-check-certificate https://freed.ga/kernel/ruisu.sh && bash ruisu.sh`

脚本执行过程中，请勿进行任何操作。待服务器重启后，重新连接安装锐速即可。

*************

锐速安装脚本

```
wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh
```

若提示：The name of network interface is not eth0, please retry after changing the name.请使用备用脚本

```
`wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh`
```
******************

### ** Linux配置 **

这是基于Ubuntu164.4系统版本教程，其他Linux系统亦可参考

配置环境，python-m2crypto libsodium18
```
sudo apt-get install git python-m2crypto libsodium18
```
如果你想将SSR安装到Download目录下，请执行（非必需步骤）

cd ~/Downloads
从Github上获取ShadowSocksR

````regexp
git clone -b manyuser  https://github.com/qcgzxw/ssr.git

````
编辑配置文件（没配置文件的请移步->https://www.qcgzxw.cn/1640.html）
```regexp
sudo vi /etc/shadowsocks.json

```
将`shadowsocks.json`文件编辑成这样（IP 端口 密码等等配置请填你自己的）
```
{
	"server":"12.34.56.78",
	"server_ipv6":"::",
	"server_port":8388,
	"local_address":"127.0.0.1",
	"local_port":1080,
	"password":"www.qcgzxw.cn",
	"timeout":300,
	"udp_timeout":60,
	"method": "chacha20",
	"protocol": "auth_sha1_v4",
	"protocol_param":"",
	"obfs":"tls1.2_ticket_auth",
	"obfs_param":"https://www.qcgzxw.cn/",
	"fast_open":false,
	"workers":1
}
```


重要信息说明：
```

server：SSR IP
server_port：SSR端口
password：SSR密码
method：SSR加密方法
protocol：SSR协议
obfs：SSR混淆方式
obfs_param：SSR混淆参数

```

按ESC键后，依次按: w q后回车，退出编辑器并保存配置文件
进入到ShadowSocksR根目录准备开始运行
```regexp
cd shadowsocksr/shadowsocks
```

启动SSR
```regexp
sudo python local.py -c /etc/shadowsocks.json -d start

```

******************
### ** 参考 **

[Ubuntu下搜狗拼音输入法打不出汉字的解决方法](https://www.cnblogs.com/xia-weiwen/p/6472372.html)
[ShadowSocks启动报错undefined symbol EVP_CIPHER_CTX_cleanup](https://kionf.com/2016/12/15/errornote-ss/)
[vim x和wq的区别](https://www.cnblogs.com/GODYCA/archive/2013/05/09/3068895.html)
[Linux中配置SS （非全局模式）](https://blog.csdn.net/qq_25978793/article/details/49870501)
[linux命令后台运行](https://www.cnblogs.com/lwm-1988/archive/2011/08/20/2147299.html)
[实战vultr搭建SSR+锐速——超速看youtube1080p](https://www.qcgzxw.cn/1640.html)
[ShadowsocksR客户端下载及操作步骤](https://www.qcgzxw.cn/301.html)