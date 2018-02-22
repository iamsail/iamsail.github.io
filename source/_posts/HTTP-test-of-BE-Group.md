---
title: HTTP 测验
date: 2017-06-24 16:21:30
categories: 计算机网络(协议)
tags: HTTP(S)
---

今天是本学期后端组的最后一次值班,[明灿](http://blog.leanote.com/mclee)进行了HTTP 测验,<span class="under0">测试的参考是《图解HTTP》</span>

本文对部分测试内容做些记录

*****************************

### ** 使用代理服务器的理由 **

- 利用缓存技术减少网络带宽的流量
- 组织内部针对特定网站的访问控制
- 以获取访问日志为主要目的

### ** 代理的两种基准分类 **

- 是否使用缓存
- 是否会修改报文

#### ** <span class="under0">缓存代理</span> **

代理转发响应时,缓存代理(Caching Proxy)会预先将资源的副本(缓存)保存在代理服务器上

当代理再次接收到对相同资源的请求时,就可以不从源服务器那里获取资源,而是将之前缓存的资源作为响应返回

#### ** <span class="under2">透明代理</span> **

转发请求或响应时,不对报文做任何加工的代理类型被称为透明代理(Transparent Proxy)。反之,对报文内容进行加工的代理被称为非透明代理

### ** 虚拟主机用来解决什么问题？怎么解决的？ **

- 使用一台HTTP服务器搭建多个站点（比如为每位客户持有的域名运行各自不同的网站）

- 在相同的IP地址下,由于虚拟主机可以寄存多个不同主机名和域名的网站,因此在发送HTTP请求时,必须在Host首部内完整执行主机名或域名的URI

### ** 写出以下四行HTTP首部字段的分类标准,并说明各字段的作用 **

- Cache-control Connection Data Via
- Accept Host if-Modified-Since User-Agent
- Age Location Server
- Content-type Allow Last-Modified Expires

这个问题过段时间会给出答案

### ** HTTP协议有哪些不足 **

- 通信使用明文(不加密),内容可能会被窃听
- 不验证通信方的身份,因此有可能遭遇伪装
- 无法证明报文的完整性,所以有可能已遭篡改

### ** Cookie的作用及其工作原理 **

- 保留HTTP协议无状态这个特征的同时,解决无状态协议的痛点(管理、控制客户端状态)
- Cookie会根据从服务端发送的响应报文的一个叫做Set-Cookie的首部字段信息,通知客户端保存Cookie。当下次客户端再往该服务器发送请求时,客户端会自动在请求报文中加入Cookie值后发送出去

### ** Cookie共享 **

- [占坑](http://www.cnblogs.com/mxmbk/articles/5671233.html)

*******************************

### ** 写在最后 **

- 《图解HTTP》是我很久以前看的,当时限于自身水平以及应用开发经验有限,理解十分粗浅
- 近期准备重看

********************************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>


