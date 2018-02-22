---
title: 如何通过文件打开Vue中的index.html
date: 2017-06-10 10:25:02
categories: Vue
---

### ** 通过Vue构建项目有两种方式 **

** 一种是直接引入vue.js文件 **

```
<script src="https://unpkg.com/vue/dist/vue.js"></script>
```

*************************

** 一种是通过vue-cli **

Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。该工具提供开箱即用的构建工具配置，带来现代化的前端开发流程

CLI 工具假定用户对 Node.js 和相关构建工具有一定程度的了解

```
$ npm install vue

# 全局安装 vue-cli
$ npm install --global vue-cli
# 创建一个基于 webpack 模板的新项目
$ vue init webpack my-project
# 安装依赖，走你
$ cd my-project
$ npm install
$ npm run dev

```

执行

```
$ npm run build
```

会对项目进行打包,并在根目录下生成一个dist文件

同时会给出提示

Tip: built files are meant to be served over an HTTP server.
Opening index.html over file:// won't work.


它提示提示：建立文件是放在一个HTTP服务器。打开index.html文件：/ /不工作。当直接使用浏览器打开文件时，浏览器控制台会报错

** 因为vue-cli的默认配置中, publishPath是用绝对目录 **

********************************

那如何执行在dist文件夹下执行打开index.html

```
修改config\index.js中的build的对象

assetsPublicPath: '/',

改为

assetsPublicPath: './',

即可
```

这样dist目录就可以随意移动了
******************************
当然也可以在

执行以下命令

```
cd dist
npm install -g http-server
hs
```

*******************

### ** 参考 **

- [关于 vue-cli 的疑惑](https://segmentfault.com/q/1010000006868255)


******************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>