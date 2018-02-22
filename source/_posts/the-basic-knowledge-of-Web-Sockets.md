---
title: Web sockets基础知识
date: 2017-06-19 16:59:59
categories: 计算机网络(协议)
tags: Websockets
---
<span class="under0">Web sockets的目标是在一个单独的持久连接上提供全双工、双向的通信(** 通信的双方可以同时发送和接受消息 **)</span>

Web sockets使用了自定义的协议。未加密的协议是ws://,加密的协议是wss://。

使用自定义协议而非HTTP协议的好处是,** 能够在客户端和服务器之间发送非常少量的数据,而不必担心HTTP那样字节级的开销 **。因此Web sockets非常适合移动应用

*********************

### ** Web Sockets API **

```
    var socket = new WebSocket("ws//www.example.com/server.php);
```

- 必须给WebSocket构造函数传入绝对URL。
- 同源策略对Web Sockets不适用,因此可以通过它打开任何站点的连接

实例了对象后,浏览器会尝试立马建立连接。有一个表示当前状态的readyState属性,该属性是只读的,属性值如下


|CONNECTING	|0|连接还没开启|
|---------|------|-----------|
|OPEN|1	|连接已开启并准备好进行通信|
|CLOSING|2|连接正在关闭的过程中|
|CLOSED|3|连接已经关闭，或者连接无法建立|


要关闭Web Sockets连接，可以在任何时候调用close()方法
```
socket.close();
```

*************************

### ** 发送和接收数据 **

建立连接后,调用send()方法,可以向服务器发送数据
```
socket.send("xxxxxxxxxx");
```
Web Sockets只能通过连接发送纯文本数据,所以对于复杂的数据结构,需要先将数据序列化为JSON字符串。

当服务器向客户端发送数据,WebSocket对象会触发message事件。返回的数据保存在event.data属性中。
```
socket.onmessage = function(event){
   var data = event.data;
};
```

*************************

### ** 其他事件 **
WebSockets还有三个其它事件,在连接生命周期的不同阶段触发

- open:在连接成功时建立
- error:在发生错误时触发,连接不能持续
- close:在连接关闭时触发

```
socket.onopen/onerror/onclose(){
    alert("xxxxxx");
};
```
*******************************
### ** 参考 **

- JavaScript高级程序设计
- [WebSocket](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket)

********************************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>