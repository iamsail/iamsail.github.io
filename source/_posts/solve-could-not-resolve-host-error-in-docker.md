---
title: 解决docker容器中” Could not resolve host”
date: 2017-09-23 11:16:20
categories: Docker
---

## ** 写在前面 **

在docke容器中执行`apt-get update`出现了一些系列错误,


## 解决


```
$ docker run busybox nslookup google.com
```

如果出现了如下内容
```
nslookup: can't resolve 'google.com'   
(Server:    8.8.8.8
Address 1: 8.8.8.8)
```

那么我们遇到的问题应该是相同的。

*********

执行
```
$ nmcli dev show | grep 'IP4.DNS'
```

出现
```
IP4.DNS[1]:              x.x.x.x
IP4.DNS[2]:              x.x.x.x
```

在`/etc/docker`目录下创建文件`daemon.json`

```
sudo vi daemon.json

## 此处的dns是填写你前面查询出来的
## 有几个写几个

{                                                                          
    "dns": ["x.x.x.x", "x.x.x.x"]                                                                           
}

```
重启docker
```
sudo service docker restart
```

最后,检验一下

```
$ docker run busybox nslookup google.com
Server:    x.x.x.x
Address 1: x.x.x.x
Name:      google.com
Address 1: 2a00:1450:4009:811::200e lhr26s02-in-x200e.1e100.net
Address 2: 216.58.198.174 lhr25s10-in-f14.1e100.net
```
大致出现如上信息,即可。


**********

## ** 参考 **

[Docker build “Could not resolve 'archive.ubuntu.com'” apt-get fails to install anything](https://stackoverflow.com/questions/24991136/docker-build-could-not-resolve-archive-ubuntu-com-apt-get-fails-to-install-a)



**********

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>