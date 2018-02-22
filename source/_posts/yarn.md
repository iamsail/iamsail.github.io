---
title: yarn
date: 2017-07-31 0:22:30
categories: npm&&yarn 
---

### ** 前言 **

今天从老家回来后,开始着手重构[killCube](https://github.com/iamsail/killCube)。

主要是准备用ES6重写,并在之前基础上,为游戏增加音效。

在这次重构中,我也从npm转移到了[yarn](https://github.com/yarnpkg/yarn)。

本文做些相关介绍和记录。

****************
### ** 什么是yarn **

Fast, reliable, and secure dependency management.

Yarn是一个新的 JS 包管理工具,由Facebook、Google、Exponent 和 Tilde 联合推出。

在这之前已经有了npm。而yarn就是对npm存在的一些缺陷进行了完善,这也是我从npm转向yarn的原因。大概如下

#### ** 更快 **

无论 npm 还是 Yarn 在执行包的安装时，都会执行一系列任务。npm 是按照队列执行每个 package，也就是说必须要等到当前 package 成功安装之后，才能继续后面的安装。而 Yarn 是同步执行所有任务，提高了性能。

yarn 缓存了每次你下载的模块，所以同样模块同样的版本不会发送第二次下载请求，对于没有缓存的模块， yarn 也可以通过并行的网络请求最大限度利用网络资源。

#### ** yarn.lock **

npm 和 Yarn 都是通过 package.json 记录项目需要拉取的依赖模块，不过在使用时，往往 package.json 中模块的版本号不太会写得非常确切，通常是定个版本范围。这样你就能自行选择使用模块的大版本或者小版本，也允许 npm 拉取模块最新的修复了 bug 的版本。

在理想的语义化版本世界中，新版是不会有颠覆旧版本的改变，然而现实并非如此。这就导致了使用 npm 拉取依赖时，即使用的是相同的 package.json，在不同的设备上拉到的 packages 版本不一，这就可能为项目引入 bug。

为了防止拉取到不同的版本，Yarn 有一个锁定文件 (lock file) 记录了被确切安装上的模块的版本号。每次只要新增了一个模块，Yarn 就会创建（或更新）yarn.lock 这个文件。这么做就保证了，每一次拉取同一个项目依赖时，使用的都是一样的模块版本。

#### ** 安全 **

yarn 在开始安装一个包之前会先用 checksums 来验证，你不用担心本地的缓存的包被破坏了导致安装失败。

#### ** 依旧是npm库 **

Yarn 没想要完全替代 npm，它只是一个新的 CLI 工具，拉取的 packages 依然来自 npm 仓库。仓库本身不会变，所以获取或者发布模块的时候和原来一样

**********
###  ** 常见命令 **
 
开始新项目

```javascript
yarn init
```
添加依赖包

```
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
```

分别添加到 devDependencies、peerDependencies 和 optionalDependencies
```
yarn add [package] --dev
yarn add [package] --peer 
yarn add [package] --optional

```

升级依赖包
```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```
移除依赖包
```
yarn remove [package]
```

安装项目的全部依赖
```
yarn
## 或者
yarn install
```
安装依赖项
```
yarn install 
```
安装选项
```
安装所有依赖：yarn 或 yarn install
安装一个包的单一版本：yarn install --flat
强制重新下载所有包：yarn install --force
只安装生产环境依赖：yarn install --production
```
*********
### ** 更换镜像 **

查看下载源
```
yarn config get registry
```
更换为淘宝源
```
yarn config set registry https://registry.npm.taobao.org

## 默认镜像源
https://registry.yarnpkg.com

```
***********

### ** 其他 **

这里我顺便记录下,今天重构发现的问题

```javascript
// 让黑块动起来
function move(){
    var con = $('con');
    var top = parseInt(window.getComputedStyle(con, null)['top']);

    if(speed + top > 0){
        top = 0;
    }else{
        top += speed;
    }
    con.style.top = top + 'px';

    if(top === 0){
        createrow();
        con.style.top = '-100px';
        delrow();
    }else if(top === (-100 + speed)){
        var rows = con.childNodes;
        if((rows.length === 5) && (rows[rows.length-1].pass !== 1) ){
            fail();
        }
    }
}

function init(){
    // 定时器 每30毫秒调用一次move()
    // clock = window.setInterval("move()", 30);
    clock = window.setInterval(function () {
        move();
    }, 30);
}

```

在上面这段代码中,init()函数,关于setInterval,提供了两种写法。

分别是注释的,记作A,非注释的,记作B。

这里我直接给结论,两种写法都是对的,但B更好。

<span class="under0">** A中用字符串作为第一个参数,十分低效。从系统的角度来说,当用字符串的时候,它会被传进构造函数,并且重新调用另一个函数。这样会拖慢程序的进度。**</span>

**********
### ** 参考 **

[Yarn vs npm：你需要知道的一切](https://zhuanlan.zhihu.com/p/23493436)
[yarn, 不是又一个 npm 第三方客户端](https://zhuanlan.zhihu.com/p/22892675)
[yarnpkg](https://yarnpkg.com/zh-Hans/)
[npm和yarn更改为淘宝镜像](http://www.bubuko.com/infodetail-1919297.html)
****************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>