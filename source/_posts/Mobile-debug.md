---
title: 移动端真机调试
date: 2017-07-09 14:21:30
categories: Developer Tools
---

移动应用开发初期可以使用chrome模拟器进行调试,<span class="under0"> ** 但模拟器毕竟是模拟器,与真机依旧有较大差距 ** </span>

*******************************

### ** 运行环境 **

Chrome 手机版
Chrome PC版
Android 版本>4.0

******************************

### ** 调试 **

1.手机通过USB数据线与电脑相连
2.进入开发者模式,开发者选项中勾选USB调试

这里以我使用的OPPO R7 Plus讲解(其它手机应该大致相同)

初次: 设置 -> 关于手机 -> 多次点击开发者模式 -> 返回上一级 -> 更多 ->开发者选项 -> USB调试
非初次: 设置 -> 关于手机 -> 更多 ->开发者选项 -> USB调试

3.电脑在chrome浏览器地址栏输入 `chrome://inspect/#devices` 并勾选 `Discover USB devices` 选项

![Mobile-debug-0](/img/Developer-Tools/Mobile-debug-0.png)

4.点击需要调试页面的 `inspect` 按钮即可进行调试

PS:使用 Chrome Inspect 查看页面时，Chrome 需要从 https://chrome-devtools-frontend.appspot.com 加载资源，** 如果你得到的调试界面是一片空白，那你可能需要科学上网。 **

![Mobile-debug-1](/img/Developer-Tools/Mobile-debug-1.png)

![Mobile-debug-2](/img/Developer-Tools/Mobile-debug-2.png)

*********************

### ** 参考 **

- [移动端真机调试指南](https://aotu.io/notes/2017/02/24/Mobile-debug/)


*********************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>