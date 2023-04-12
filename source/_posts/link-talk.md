---
title: 链接样式
date: 2017-07-08 14:06:29
categories: HTML&&CSS
---

链接是万维网的基础,使得网页可以互相连接。

HTML中使用`<a>`标签定义超链接

本文谈谈`<a>`标签的样式

**************************

在《精通CSS高级Web标准解决方案》一书中,是这样总结的

使用以下次序应用链接样式

```
a:link a:visited a:hover a:focus a:active


:link伪类选择器是作用于没有访问过的链接

:visited伪类选择器是作用于已访问的链接

:hover伪类选择器是作用于鼠标悬浮状态

:focus伪类选择器是作用于获得焦点时(比如通过键盘移动到该链接时)

:active伪类选择器是作用于被激活的元素

```

<span class="under0">也就是LVHFA</span>

*********************************

或许是因为Web在不断变化,我实践的时候有一些发现,做点记录

### ** demo-1 **

<span class="under0">** 代码如下: **</span>

```
## style

a{
    display: block;
    margin-top: 12px;
}

a:link{
    color: red;
}

a:visited{
    color: gold;
}

a:hover{
    color: #00bcd7;
}

a:focus{
    color: seagreen;
}

a:active{
    color: black;
}

## html

<a href="https://github.com/bayi27">1111111</a>
<a href="#">2222222</a>
<a href="#">3333333</a>
<a href="#">4444444</a>
<a href="http://www.sail.name/">5555555</a>
<a href="http://www.sail.name/">6666666</a>

```

<span class="under0">** 渲染如下: **</span>

![link-talk-0.png](/img/htmlcss/link-talk-0.png)

可以看出

1、5、6指向外部的链接,`:link`伪类选择器的样式没有生效
2、3、4指向内部的链接,`:visited`伪类选择器的样式生效

** 虽然这些链接都没有访问过 **


*********************************

### ** demo-2 **

<span class="under0">** 代码如下: **</span>
```
## style

a{
    display: block;
    margin-top: 12px;
}

a{
    color: gold;
}

a:link{
    color: black;
}

#a:visited{
#    color: green;
#}


## html

<a href="http://www.sail.name/">aaaaaa</a>
<a href="#">bbbbbb</a>

```
<span class="under0">** 渲染如下: **</span>

![link-talk-1.png](/img/htmlcss/link-talk-1.png)

指向外部的链接,生效的样式是`<a>`标签的样式
指向内部的链接,生效的样式是`:link`伪类选择器的样式

** 同样这些链接也没有访问过 **

若取消注释,渲染如下

![link-talk-2.png](/img/htmlcss/link-talk-2.png)

这是因为当两个规则具有相同的特殊性时,后定义的规则优先

********************************

### ** 总结 **

** 指向内部的链接,`:link`选择器生效;指向外部的链接,`:link`选择器没有起作用 **

PS:这个指向外部的链接,域名必须是已经解析的,否则与指向内部的链接是同等的效果。读者可以自行尝试验证。

