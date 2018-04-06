---
title: border-radius
date: 2017-05-01 22:21:17
categories: HTML&&CSS
---

虽然写了很久的border-radius,但也是近期才知道,** border-radius每个值可以有两个长度,分别是椭圆的水平半径和垂直半径。**

有兴趣看demo,[戳这儿](http://www.sail.name/CSS_Demo/border-radius.html)

*********************

 border-radius 用来设置边框圆角

** 当使用一个半径时确定一个圆形；当使用两个半径时确定一个椭圆，这个(椭)圆与边框的交集形成圆角效果 **

![border-radius-2.png](/img/htmlcss/border-radius-2.png)

![border-radius-1.png](/img/htmlcss/border-radius-1.png)

************************

### ** 语法 ** ###

<code>border-radius: 1-4 length|% / 1-4 length|%;</code>

按此顺序设置每个 radii 的四个值。如果省略 bottom-left，则与 top-right 相同。如果省略 bottom-right，则与 top-left 相同。如果省略 top-right，则与 top-left 相同。

** 这里的顺序是指: 左上 右上 右下 左下 **

** length **

定义圆形半径或椭圆的半长轴，半短轴。不能用负值。

** percentage **

使用百分数定义圆形半径或椭圆的半长轴，半短轴。水平半轴相对于盒模型的宽度；垂直半轴相对于盒模型的高度。不能用负值。


** 半径的第一个语法取值可取1~4个值: **
```
    border-radius: radius

    border-radius: top-left-and-bottom-right top-right-and-bottom-left

    border-radius: top-left top-right-and-bottom-left bottom-right

    border-radius: top-left top-right bottom-right bottom-left
```
** 半径的第二个语法取值也可取1~4个值 **
```
    border-radius: (first radius values) / radius

    border-radius: (first radius values) / top-left-and-bottom-right top-right-and-bottom-left

    border-radius: (first radius values) / top-left top-right-and-bottom-left bottom-right

    border-radius: (first radius values) / top-left top-right bottom-right bottom-left

    border-radius: inherit
```
**************************

### ** 参考 ** ###

- [border-radius-MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius)
- [border-radius-W3school](http://www.w3school.com.cn/cssref/pr_border-radius.asp)
- [border-radius-W3C](https://www.w3.org/TR/2005/WD-css3-background-20050216/#the-border-radius)

