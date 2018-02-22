---
title: 小谈盒子模型
date: 2017-03-12 23:16:17
categories: HTML&&CSS
---
最近通过某前端交流群，讨论的一个问题，发现** 对盒子模型的了解还很浅显。**

背景如下:
A君：为啥我设置的input的高度和实际显示的高度有0.8px的偏差。
![box-sizing.jpg](/img/htmlcss/box-sizing.jpg)

从图片上的开发者工具，我们可以看到 ** style中height为31px,border有1px*2,然后实际的高度却是32.6px。分明是少了0.4px。 **

最终A君解决了这个问题，解决办法是:** input元素的box-sizing默认是content-box，只需要改成border-box即可。**

*****************

次日晚上,我在w3school看了下[box-sizing](http://www.w3school.com.cn/cssref/pr_box-sizing.asp)

box-sizing 属性允许您以特定的方式定义匹配某个区域的特定元素。

    box-sizing: content-box|border-box|inherit;

- content-box

    - 这是由 CSS2.1 规定的宽度高度行为。
    - 宽度和高度分别应用到元素的内容框。
    - 在宽度和高度之外绘制元素的内边距和边框。

- border-box

    - 为元素设定的宽度和高度决定了元素的边框盒。
    - 就是说，为元素指定的任何内边距和边框都将在已设定的宽度和高度内进行绘制。
    - 通过从已设定的宽度和高度分别减去边框和内边距才能得到内容的宽度和高度。

- inherit

    - 规定应从父元素继承 box-sizing 属性的值。

****************

看到这儿，虽然我没能弄清楚为什么少了0.4px(毕竟图片提供的信息十分有限),但应该能够明白为什么设置 <code>box-sizing:border-box</code>能够解决问题了。因为这种情况下，width的高度已经包括了边框和内边距的高度和宽度了，当然还有内容的宽度和高度了。

说到box-sizing就避不开了盒子模型了。因为** box-sizing 是用来选择是标准(W3C)盒模型还是IE盒模型的 **

** 一个盒模型具备内容(content)、填充/内边距(padding)、边框(border)、边界/外边距(margin)。 **

我们一般所说的盒子模型都是指的标准盒模型。和标准(W3C)盒子模型不同的是:IE盒子模型的 content 部分包含了 border 和 pading。

也就是说标准盒子模型，width = content.width。IE盒模型 width = content.width + border.width +padding.width 【实际上并没有类似border.width这种写法】

可以看下这段代码和图片加以理解。

    <style>
            .one{
                box-sizing: content-box;
                background-color: deepskyblue;
                width: 150px;
                height: 150px;
                padding-left: 10px;
                border:1px solid green;
            }

            .tow{
                box-sizing: border-box;
                background-color: red;
                width: 150px;
                height: 150px;
                padding-left: 10px;
                border:1px solid green;
            }
    </style>

     <div class="one">1</div>
     <div class="tow">2</div>

************************

![tow-box-model.png](/img/htmlcss/tow-box-model.png)

class = "one"
![content-box.png](/img/htmlcss/content-box.png)

class = "tow"
![border-box.png](/img/htmlcss/border-box.png)


************************

当然最后还是有些困惑的————开篇提到的为什么少了0.4px。于是,又看了看BFC,依然没能解决。

参考资料:

- [BFC 神奇背后的原理](http://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html)
- [box-sizing](http://www.w3school.com.cn/cssref/pr_box-sizing.asp)

<div width="100%" align="center"><div name="dashmain" id="dash-main-id-87905c" class="dash-main-2 87905c-3"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>