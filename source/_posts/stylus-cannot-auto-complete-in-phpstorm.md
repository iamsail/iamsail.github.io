---
title: stylus在phpstorm中不能自动补全
date: 2017-07-09 19:54:30
categories: Developer Tools
tags: CSS预处理器
---

### ** 问题 **

今天在phpstorm中开发VUE应用,发现一个问题

在开发单页面组件时,style部分

```
<style  scoped>

</style>
```

写原生的CSS会有代码提示和自动补全

可如果使用预处理器stylus

```
<style lang="stylus" scoped>

</style>
```

不会有代码提示和自动补全

至于less和sass我是没有测试的

*********************

###  ** 解决 ** 

** 原来是phpstorm没有升级到最新(目前最新是2017.1),在最新版中已经修复了这个bug **

当然前提是要装上VUE和stylus插件,否则哪怕是最新版也无能为力

********************
### ** 福利 **

** jetbrains旗下的产品学生是可以免费使用的 **

这里我给出参考链接

<span class="under0">[学生授权申请方式 ](https://sales.jetbrains.com/hc/zh-cn/articles/207154369-%E5%AD%A6%E7%94%9F%E6%8E%88%E6%9D%83%E7%94%B3%E8%AF%B7%E6%96%B9%E5%BC%8F)</span>



*********************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>