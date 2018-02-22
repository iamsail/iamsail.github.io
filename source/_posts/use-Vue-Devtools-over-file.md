---
title: 通过文件网址使用vue-devtools
date: 2017-06-11 11:00:02
categories: Vue
---

### ** vue-devtools **

[vue-devtools](https://github.com/vuejs/vue-devtools)是chrome浏览器的一个扩展程序用于调试Vue.js应用程序

***********

vue-devtools默认是只有通过http/https打开文件才能检测,开发者工具才会出现VUE窗格
<span class="under0">** 如果要使通过file://协议打开的网页正常工作,需要在扩展程序中勾选允许访问文件网址才可以 **</span>

***********

此外,如果页面使用Vue.js的生产/最小化构建，默认情况下将禁用devtools检查，因此Vue窗格将不会显示。

#### ** 如何在生产版本开启vue-devtools **

修改全局配置Vue.config,是一个对象，包含 Vue 的全局配置

```
#devtools

#类型： boolean
#默认值： true (生产版为 false)

#用法：
#务必在加载 Vue 之后，立即同步设置以下内容
Vue.config.devtools = true
#配置是否允许 vue-devtools 检查代码。开发版本默认为 true，生产版本默认为 false。
#生产版本设为 true 可以启用检查。
```
************************

### ** 下载地址 **


[vue-devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?utm_source=chrome-app-launcher-info-dialog)





******************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>