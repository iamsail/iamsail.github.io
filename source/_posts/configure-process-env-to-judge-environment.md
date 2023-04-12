---
title: 配置process.env判断代码运行环境
date: 2019-04-13 13:56:01
categories: Vue
tags: [node]
---
### ** Preface **

在开发一个项目的时候，会涉及到许多环境,比如dev、test、stage、product等,不同的环境需要加载不同的配置,因为后端接口的域名是不同的。

*********************

### ** process.env **

我们可以通过`process.env`来配置`NODE_ENV`来区分开发环境。

`process `对象是一个全局变量，它提供有关当前` Node.js `进程的信息并对其进行控制。 作为一个全局变量，它始终可供` Node.js `应用程序使用，无需使用` require()`。`process.env `属性返回包含用户环境的对象。

在`package.json`中进行配置
```javascript
"scripts": {
    "start": "node ./bin/www",
    "dev": "NODE_ENV=development pm2 --no-daemon start ./bin/www --watch ",
    "stage": "NODE_ENV=stage pm2 --no-daemon start ./bin/www --watch "
}
```


如果是windows环境,执行`npm install cross-env`
```javascript
// 因为mac和windows设置命令环境变量的命令不一致, 所以用cross-env来做兼容
"scripts": {
    "start": "node ./bin/www",
    "dev": "cross-env NODE_ENV=development pm2 --no-daemon start ./bin/www --watch ",
    "stage": "cross-env NODE_ENV=stage pm2 --no-daemon start ./bin/www --watch "
}
```

在代码中,我们就可以通过`process.env.NODE_ENV`来判断环境

```javascript
    let host = null;
    if (process.env.NODE_ENV === "development") {
        // pass
    } else if (process.env.NODE_ENV === "stage") {
        // pass
    }
```
********************

### ** vue-cli创建的项目 **

如果我们是[vue-cli脚手架来创建的项目](https://cli.vuejs.org/zh/guide/mode-and-env.html#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E5%92%8C%E6%A8%A1%E5%BC%8F):

模式是 Vue CLI 项目中一个重要的概念。默认情况下，一个 Vue CLI 项目有三个模式：

- `development` 模式用于 `vue-cli-service serve`
- `production` 模式用于 `vue-cli-service build 和 vue-cli-service test:e2e`
- test 模式用于 vue-cli-service test:unit
注意模式不同于 NODE_ENV，一个模式可以包含多个环境变量。也就是说，每个模式都会将 NODE_ENV 的值设置为模式的名称——比如在 development 模式下 NODE_ENV 的值会被设置为 "development"。

** 你可以通过为 .env 文件增加后缀来设置某个模式下特有的环境变量。比如，如果你在项目根目录创建一个名为 .env.development 的文件，那么在这个文件里声明过的变量就只会在 development 模式下被载入。**

你可以通过传递 --mode 选项参数为命令行覆写默认的模式。例如，如果你想要在构建命令中使用开发环境变量，请在你的 package.json 脚本中加入：

```
"dev-build": "vue-cli-service build --mode development",
```


*********************
### ** 参考 **

[process | Node.js API 文档](http://nodejs.cn/api/process.html#process_process_env)
[Node环境变量 process.env 的那些事儿 - JS那些事儿 - SegmentFault 思否](https://segmentfault.com/a/1190000011683741)
[环境变量和模式 | Vue CLI](https://cli.vuejs.org/zh/guide/mode-and-env.html#%E6%A8%A1%E5%BC%8F)
[业务代码如何判断生产/开发环境 - 我不懂前端 - SegmentFault 思否](https://segmentfault.com/a/1190000016194069)
[React系列---Webpack环境搭建（二）不同环境不同配置 - 朱哥的全栈历险记 - SegmentFault 思否](https://segmentfault.com/a/1190000009952845)