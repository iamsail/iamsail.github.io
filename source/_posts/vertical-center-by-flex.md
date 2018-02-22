---
title: flex垂直居中
date: 2017-07-22 10:15:22
categories: HTML&&CSS
---

以前我们实现水平垂直居中,可以通过如下的代码段实现

```CSS
 position: absolute;
 top:50%;
 left:50%;
 transform: translateX(-50%) translateY(-50%);
```

实现文本垂直居中也可以借助以下代码段实现

```CSS
display: table-cell;
vertical-align: middle;

```
*********************

而使用flex可以更加简单的实现

若对flex不了解,可以看看我的博文[Flex基础](http://www.sail.name/2017/07/09/the-base-of-flex/)

这里介绍两种方式

### ** HTML结构 **

```HTML
  <div>
     <p>
         1111111 
     </p>
  </div>
```

### ** 方法一 **

CSS

```CSS
    div{
        display: flex;
        width: 200px;
        height: 200px;
        border: 10px solid red;
       }

    p{
        margin: auto;
    }
```

*********************

### ** 方法二 **

CSS
```CSS
  div{
      display: flex;
      width: 200px;
      height: 200px;
      background: red;
      justify-content: center;
      align-items: center;
  }
```
方法二可以去掉p标签



******************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>


