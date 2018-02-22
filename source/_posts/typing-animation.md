---
title: 打字机动画
date: 2017-08-03 21:09:00
categories: HTML&&CSS
tags: CSS揭秘
---

### ** 前言 **

本文是对《CSS揭秘》中的打字机动画的记录,没有教程意义。

<iframe src="http://www.sail.name/CSS_Demo/typing.html" style="width:500px;height:100px;">
</iframe>

**********

### ** 相关 **

在[工作室首页](http://flyingstudio.online/)也有一个打字机的效果。该效果是由[肖高阳](https://blog.xgy666.cn/)编码实现的。

通过审查元素可以发现是通过JS脚本动态的写入字符实现的。

在secret一书中的方法只需要借助CSS就可以实现。

************

### ** 先行知识 **

#### ** ch **

ch是CSS中和字符相关的相对单位。

与ch相关的字符是0,也就是1ch便是1个0的宽度。该单位必须与等宽字体一起使用才有用。

等宽字体有`Consolas`,`Monaco`, `monospace`等等

#### ** steps() **

请看我的博文[animation-timing-function:steps](http://www.sail.name/2017/04/21/steps-in-animation-timing-function/)

***********

### ** 实现 **

HTML

```HTML
<h1 id="h1">hello world66</h1>
```
CSS

```CSS
    @keyframes typing {
            from{width : 0}
        }
        
        @keyframes caret {
            50%{border-color: transparent;}
        }
        h1{
            font-family: "Consolas";
            width:11ch;
            white-space: nowrap;
            overflow: hidden;
            border-right: .5em solid;
            animation: typing 6s steps(11),
                       caret 1s  steps(1) infinite;
        }
```

如果需要动态适配文字内容,加上以下脚本即可

```javascript
 var h1 = document.getElementById("h1");
    function typing(target) {
        var len = target.textContent.length,
            s  = target.style;
        s.width = len + "ch";
        s.animationTimingFunction = "steps(" + len + "),steps(1)"
    }
    typing(h1);
```

****************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>