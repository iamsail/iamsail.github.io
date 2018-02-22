---
title: 移动端click事件的300ms延迟
date: 2017-07-25 19:40:17
categories: Javascript
tags: 移动web
---

### ** 背景 **

近期开发[killCube](https://github.com/iamsail/killCube),了解到移动端click事件有一个300ms延迟。本文做些记录。

***********

### ** 延迟由来 **

这要追溯至 2007 年初。苹果公司在发布首款 iPhone 前夕，遇到一个问题：当时的网站都是为大屏幕设备所设计的。于是苹果的工程师们做了一些约定，应对 iPhone 这种小屏幕浏览桌面端站点的问题。

这当中最出名的，当属双击缩放(double tap to zoom)，这也是会有上述 300 毫秒延迟的主要原因。双击缩放，顾名思义，即用手指在屏幕上快速点击两次，iOS 自带的 Safari 浏览器会将网页缩放至原始比例。

那么这和 300 毫秒延迟有什么联系呢？

假定这么一个场景。用户在 iOS Safari 里边点击了一个链接。由于用户可以进行双击缩放或者双击滚动的操作，当用户一次点击屏幕之后，浏览器并不能立刻判断用户是确实要打开这个链接，还是想要进行双击操作。因此，iOS Safari 就等待 300 毫秒，以判断用户是否再次点击了屏幕。

鉴于iPhone的成功，其他移动浏览器都复制了 iPhone Safari 浏览器的多数约定，包括双击缩放，几乎现在所有的移动端浏览器都有这个功能。之前人们刚刚接触移动端的页面，在欣喜的时候往往不会care这个300ms的延时问题，可是如今touch端界面如雨后春笋，用户对体验的要求也更高，这300ms带来的卡顿慢慢变得让人难以接受。

而touchstart事件虽然响应很快,但如果用户只是想下滑滚动屏幕也会触发。

**********

这里介绍两种方法

### ** 禁止缩放 **
```
<meta name="viewport" content="user-scalable=no, initial-scale=1.0, 
maximum-scale=1.0, minimum-scale=1.0">
```
表明这个页面是不可缩放的,双击缩放功能就没有意义,此时浏览器会禁用默认的双击缩放行为并且去掉300ms的延迟。

当然倘若想让页面能够缩放,那么这个方案就失效了

### ** 更改默认的适口宽度 **

通过标签设置适口宽度为设备宽度
```
<meta name="viewport" content="width=device-width">
```
如果能够识别出一个网站是响应式网站,那么移动端浏览器就可以自动禁掉默认的双击缩放行为并且去掉300ms的点击延迟。因此设置了上述标签,浏览器就可以认为改网站对移动端做过了适配和优化,无需双击缩放的操作了。


至于其它使用第三方库的方法我就不做介绍了

**********

### ** 参考 **

[移动端click事件延迟300ms到底是怎么回事，该如何解决？](http://www.cnblogs.com/shenjp/p/6433646.html)

***********

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>

