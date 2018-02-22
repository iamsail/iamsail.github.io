---
title: 妙用switch
date: 2017-07-21 9:25:17
categories: Javascript
tags: 奇技淫巧
---

在某个交流群看到这样一个问题

** 给定变量X,判断X值落在哪个区间[0,10],[10,50],[50,100],[100,+++],只能使用switch **


********************

一般我们写switch都是这样写的

```JavaScript
switch (foo){
    case 0:
    case 1:
        console.log('hehe');
        break;
    case 2:
        console.log('xixi');
        break;
    default:
        console.log('momo');
}        
```

其实像还可以这样

```JavaScript
switch (true){
    case foo > 0 && foo <=3:
        console.log('HTML');
        break;

    case foo > 3 && foo <=100:
        console.log('CSS');
        break;
    default:
        console.log("JavaScript");
}
```

*******************

开篇的问题就很容易解决了

********************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>

