---
title: 'Invalid Host header'
date: 2019-04-13 13:15:30
categories: webpack
---

### ** Preface **

最近在部署一个前端用vue开发的项目的时候,访问的时候页面出现了如下错误`'Invalid Host header'`

********************

**<span class="under0"> 这是因为新版的webpack-dev-server出于安全考虑，默认检查hostname，如果hostname不是配置内的，将中断访问。</span>**

如果有webpack配置文件，那么在`package.json`的脚本里添加参数即可

```javascript
"webpack-dev-server --disableHostCheck=true"
```

如果是通过vue-cli来创建的项目,在根目录下创建文件`vue.config.js`, 然后填入如下内容

```javascript
module.exports = {
    devServer: {
        host: '0.0.0.0',
        hot: true,
        disableHostCheck: true,
    },
}
```
********************

### ** 参考链接 **

[关于webpack 'Invalid Host header' 错误 - 简书](https://www.jianshu.com/p/111806476add)
[解决vue-cli脚手架访问出现“Invalid Host header” | 浅殇博客](https://www.trojansun.com/solve-vue-cli-invalid-host-header.html)
[配置参考 | Vue CLI](https://cli.vuejs.org/zh/config/#%E5%85%A8%E5%B1%80-cli-%E9%85%8D%E7%BD%AE)