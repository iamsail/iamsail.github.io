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
******************
### ** 参考 **

[Ubuntu下搜狗拼音输入法打不出汉字的解决方法](https://www.cnblogs.com/xia-weiwen/p/6472372.html)
[ShadowSocks启动报错undefined symbol EVP_CIPHER_CTX_cleanup](https://kionf.com/2016/12/15/errornote-ss/)
[vim x和wq的区别](https://www.cnblogs.com/GODYCA/archive/2013/05/09/3068895.html)
[Linux中配置SS （非全局模式）](https://blog.csdn.net/qq_25978793/article/details/49870501)
[linux命令后台运行](https://www.cnblogs.com/lwm-1988/archive/2011/08/20/2147299.html)