---
title: dependencies与devDependencies
date: 2017-07-24 10:37:30
categories: npm&&yarn 
---

在项目的`package.json`中有两个相似的键值对,分别是`dependencies`与`devDependencies`

在使用npm安装node模块或者插件时,有两种命令参数将其信息写入`package.json`文件

```
-- save dev
-- save
```

其中`-- save dev`安装的插件,依赖包名字被添加到`devDependencies`键下面,该键下面的模块依赖用于开发环境,不用于生产环境
`-- save dev`安装的插件,依赖包名字被添加到`dependencies`键下面,该键下面的模块依赖于用于开发环境

****************

执行
```
npm install 
```
默认安装两种依赖

**************

如果只是单纯的使用这个包而不需要进行一些改动测试之类的,只安装dependencies而不安装devDependencies。
执行
```
npm install --production

```
**************

执行
```
npm install packagename
```

只安装dependencies

****************

如需安装devDependencies
执行

```
npm install packagename
```

****************

### ** 参考 **


[devDependencies和dependencies的区别](http://www.cnblogs.com/ayseeing/p/4128612.html)
[dependencies与devDependencies的区别](http://www.cnblogs.com/fewenjing/p/5892377.html)




********************************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>