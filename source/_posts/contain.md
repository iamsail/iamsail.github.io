---
title: contain
date: 2017-08-10 15:27:00
categories: HTML&&CSS
tags: 性能优化
---

### ** 前言 **

本文是对`contain`属性的介绍。

2017年8月8日，W3C的CSS工作组发布了 CSS包含模块（CSS Containment Module Level 1）的候选推荐标准（Candidate Recommendation）。该模块定义了 ‘contain’ 属性，用于指出该元素的子树将独立于页面的其他部分。该规范可用于用户代理（如浏览器等）的重度优化（heavy optimizations）。

contain 属性允许开发者声明当前元素和它的内容尽可能的独立于其他部分的 Dom 树。这会让浏览器在重新计算布局、样式、绘图或它们的组合的时候，仅仅在有限的 Dom 区域中，并不是整个页面。这个属性常用在包含大量独立的 widgets 小部件的页面，这个 contain 属性可以防止某个小部件的 CSS 规则改变页面上的其他东西。

先看看兼容性

![1.png](/img/性能优化/contain/1.png)

可以看出contain的兼容性,没错还相当糟糕。

****************

### ** API **

`
none
`
声明元素正常渲染，没有包含的应用。

`
strict
`
声明所有的包含规则应用于这个元素。这样写等价于 contain: size layout style paint。


`
content
`
声明这个元素上除了 size 的所有包含规则。等价于 contain: layout style paint。



`
size
`
声明这个元素可以被变换尺寸，不需要去检查它依赖尺寸变化。


`
layout
`
声明没有外部元素可以影响它内部的布局，反之亦然。


`
style
`
声明那些同时会影响这个元素和其子孙元素的属性，不会超出这个元素的包含范围。

`
paint
`
声明这个元素的子孙节点不会在它边缘外显示。如果一个元素在视窗外或其他原因不可见，则同样保证它的子孙节点不会被显示。


****************

### ** 参考 **

[W3C 发布 CSS 包含模块（CSS Containment Module Level 1）的候选推荐标准 征集参考实现及审阅意见](http://www.chinaw3c.org/archives/1926/)
[CSS性能优化新属性 contain 的语法、作用及使用场景](http://ms.csdn.net/geek/197519)


****************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>