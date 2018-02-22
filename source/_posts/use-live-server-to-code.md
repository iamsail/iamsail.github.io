---
title: 使用live-server开发web应用
date: 2017-06-15 16:55:00
categories: Developer Tools
---
在我的另一篇博文[如何通过文件打开Vue中的index.html](http://www.sail.name/2017/06/10/how-to-open-index-html-of-vue-over-file/)提到了http-server

本文介绍的是[live-server](https://github.com/tapio/live-server)。

<span class="under0">这是一个具有实时重新加载功能的小型开发服务器。是的,相比http-server来说,这个具备了实时刷新的功能。</span>

当然使用http-server,我们也可以通过其它组件配合达到这个效果,比如supervisor。

*****************************

### ** live-server **

```
# 全局安装
npm install -g live-server

# 修改package.json中的script
"scripts": {
  "server": "live-server ./ --port=8080"
}

# 启动

npm run server

```

*************************
### ** devserver **

当然devserver也可以构建本地服务器,且实时监听修改。

|devserver配置选项 | 功能描述 |
| ------------- |-------------|
| contentBase| 默认webpack-dev-server会为根文件夹提供本地服务器，如果想为另外一个目录下的文件提供本地服务器，应该在这里设置其所在目录（本例设置到“public"目录）|
| port|设置默认监听端口，如果省略，默认为”8080“|
|inline | 设置为true，当源文件改变时会自动刷新页面 |
|colors | 设置为true，使终端输出的文件为彩色的|
|historyApiFallback | 在开发单页应用时非常有用，它依赖于HTML5 history API，如果设置为true，所有的跳转将指向index.html|

```
# 修改webpack配置文件
  devServer: {
    contentBase: "./public",//本地服务器所加载的页面所在的目录
    colors: true,//终端中输出结果为彩色
    historyApiFallback: true,//不跳转
    inline: true//实时刷新
  }
```

更多可以参考我的另一篇博文[webpack加载不了样式](http://www.sail.name/2017/05/17/can-not-load-css-in-webpack/)

*************************

### ** 参考 **

- [Markdown 语法手册 （完整整理版）](http://blog.csdn.net/witnessai1/article/details/52551362)
- [live-server 快速搭建服务](https://juejin.im/post/5940dc1961ff4b006cb82c3d)

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>