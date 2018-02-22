---
title: 一个div在页面下的布局
date: 2017-05-19 7:45:30
categories: HTML&&CSS
---

#### ** 关于一个div在页面下的布局问题,已经困扰我很久很久了。** ####

当然此处换成span,section之类同样适用。

最近有了些新理解,在此做些记录。

*****************************

** 在开始阅读本文前,强烈建议读读garychang的[js获得浏览器宽高、屏幕宽高](http://garychang.cn/2016/08/16/widthheight/)。**

讲得十分清楚,以下做些摘录

#### ** 关于高度 **

```
//浏览器窗口高度
window.outerHeight
//浏览器可视区域高（包括滚动条）
window.innerHeight
//ps：在部分版本QQ浏览器上innerHeight和outerHeight值相同
//浏览器可视区域高（不包括滚动条）
document.documentElement.clientHeight
//网页总高度
document.body.clientHeight
//显示器可视高度
window.screen.height
//显示器可用高度（例如去除底部任务栏）
window.screen.availHeight

```

#### ** 关于宽度 **

```

//浏览器窗口宽度
window.outerWidth
//浏览器可视区域宽度（包括滚动条）
window.innerWidth
//浏览器可视区域宽度（不包括滚动条）
document.documentElement.clientWidth
//网页总宽度
document.body.clientWidth
//显示器可视宽度
window.screen.width
//显示器可用宽度（例如去除侧边任务栏）
window.screen.availWidth
```
***********************

哪怕只有一个div,布局也是涉及很多知识。对CSS没有一定的研究是很难讲清楚的。

限于自身水平,从

- position值为relative(主要讲这个)
- position值为absolute
- 页面有滚动条

这三方面进行讲解

***************************

#### ** 相关环境 **


- 屏幕分辨率 1920 * 960
- 测试环境 chrome 浏览器
- 如果未特殊说明,浏览器是窗口最大化的


*************************
#### ** position值为relative **

```
    html
    <div>one</div>

    css
     div{
         position: relative;
         width: 200px;
         height: 200px;
         top: 10%;
         left: 10%;
         /*top: 100px;*/
         /*left: 100px;*/
         text-align: center;
         line-height:200px;
         border: 2px solid salmon;
     }
```

##### ** 当top,left的值为100px时 **,会相对正常的位置在水平和垂直方向移动100px。如下

![oneDivLayout-0.png](/img/htmlcss/oneDivLayout-0.png)
![oneDivLayout-1.png](/img/htmlcss/oneDivLayout-1.png)

##### ** 当top,left的值为10%时 **
![oneDivLayout-2.png](/img/htmlcss/oneDivLayout-2.png)
![oneDivLayout-3.png](/img/htmlcss/oneDivLayout-3.png)

chrome浏览器下默认margin为8px等,这些细枝末节抛开不讲。

这里有一个有意思的问题

** 第二个盒子模型中,top方向的值为20.391px,可实际页面上盒子在top方面并没有移动(那一个小空白是body的margin值) **

** <code>left = (1920 - 8 * 2) x 0.1 ~ 190.391</code> **
** <code>top  = (200 + 2 * 2 ) x 0.1 ~ 20.391</code> **

用明白为什么20.391px的计算值为什么在页面没有效果,需要对CSS有一定了解。

就不慢慢科普了,直接上我的结论

** div的盒子在body盒子内部,此处的div的百分比依据body的值来计算的。**
** div的盒子在body盒子内部,此处的div的百分比依据body的值来计算的。**
** div的盒子在body盒子内部,此处的div的百分比依据body的值来计算的。**

**移动的参考点也是body形成的盒子的左上方第一个点来进行移动的 **

** body的样式这里使用的是user agent stylesheet(这里可以参考我的另一篇博文[CSS中的层叠优先级](http://www.sail.name/2017/05/18/the-cascade-priority-in-style-sheet/))。也就是display取值为block。 **

** 所以这里body形成的是block级别的盒子,宽度为document.body.clientWidth,而高度为div撑起来的高度也就是div盒子的高度 **

** 这儿就很明白了。**

**body本身是没有高度,有宽度的 **
**body本身是没有高度,有宽度的 **
**body本身是没有高度,有宽度的 **

** 0 x 0.1 = 0 **

如果想进一步体会,可以把div去掉或者top值改为px单位,仔细观察下。

**********************

#### ** position值为absolute **

这种情况,盒子脱离文档流。

百分比情况下,是相对于html定位的。因为body是static。

html宽度值为document.documentElement.clientWidth

**************************

#### ** 页面有滚动条 **

这里又可以细分为水平方向,垂直方向的滚动条了

我粗暴的总结下

** 此时html的宽度就是document.documentElement.clientHeight。所有值的计算要先减去滚动条宽度再进行计算 **

**********************

#### ** 写在最后 **

一直困扰我的就是position值为relative的情况。

网上也没查到相关资料。

好在通过这段时间的学习,搞定了。

*************************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>