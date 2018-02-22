---
title: CSS中的层叠优先级
date: 2017-05-18 0:00:00
categories: HTML&&CSS
---

#### ** 以前我对CSS中的样式优先级别理解是这样的 **

** 从高到低 **

- 属性后跟!important的样式
- 作为style属性写在元素标签的内联样式
- id选择器
- 类选择器
- 伪类选择器
- 属性选择器
- 标签选择器
- 通配符选择器
- 浏览器自定义

*******************

最近看绿皮书,书中这样写到

** 层叠采用以下重要次序 **

- 标有!important的用户样式
- 标有!important的作者样式
- 作者样式
- 用户样式
- 浏览器/用户代理应用的样式

*********************

作者样式既是开发者编写的。

这个用户样式,就是用户自己写的样式文件,导入浏览器。在chrome中叫做<code>custom.css</code>

** 不过自从33版本后,chrome便取消了对<code>custom.css</code>文件的支持 **

时代变迁呀,Web也在不断发展233333


***********************

#### ** 参考 **

- [CSS样式表来源以及“！important”规则](http://blog.csdn.net/ruoyiqing/article/details/38959045)
- [添加浏览器的用户样式表](http://www.cnblogs.com/xesam/archive/2011/12/08/2280707.html)


**********************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>