---
title: Uglifyjs失效?
date: 2017-08-04 21:14:30
categories: webpack
---

在昨天我发布了[killCube v2.0.0](https://github.com/iamsail/killCube)

v2.0.0与v1.0.0相比

主要是用ES6重写,并为游戏增加了音效

******************

第一次打包完的`bundle.js`大概有2.8MB大小。首次加载简直是一个噩梦，半分钟也不一定能够加载出来。

于是今天开始做优化相关的工作,更多详细的优化在彻底完成或许会写博文记录

通过关闭`devtool`,将`bundle.js`减小到了1.2MB左右

** 这里记录下使用`Uglifyjs`遇见的问题 **

*******************

![1.png](/img/webpack/is-Uglifyjs-cannot-work/1.png)
![2.png](/img/webpack/is-Uglifyjs-cannot-work/2.png)
![3.png](/img/webpack/is-Uglifyjs-cannot-work/3.png)

<span class="under0">** 从上面的图片可以看出,引入`Uglifyjs`插件后,是1.21MB大小。问题在于引入插件前,终端显示也是1.21MB. **</span>

于是我认为这个插件没有生效,百之谷之,都没有解决我的问题。翻看完官方文档依旧没有结果。

这一折腾就是五六个小时,最后意外的发现了原因。

![4.png](/img/webpack/is-Uglifyjs-cannot-work/4.png)
![5.png](/img/webpack/is-Uglifyjs-cannot-work/5.png)


************

原来插件是生效的,但是整个文件只优化了4kb,相对1.21MB是忽略不计的,所以在终端上没有显示出来。

<span class="under0">** 给我一种插件没有生效的错觉。**</span>

这里要解释下,`Uglifyjs`的压缩效果还是很强大的,可为什么这里只优化了4KB呢？

<span class="under0">** 我将44个时长为0.5的音频通过node脚本转码成了一个base64的数组。base64数组里面的内容本身间隙很小,几乎没有多余的空格,也就是没有压缩的空间了。**</span>

有群友提到,可以使用mid格式进行优化。可以尝试下。
********************************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>