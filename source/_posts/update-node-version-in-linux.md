---
title: linux升级node版本
date: 2017-10-22 20:06:00
categories: Javascript
tags: node
---

## ** preface **

本文是对`nodejs`版本升级的记录。因为使用的`zsh`有点不同,做点记录。

`nodejs` 升级一般使用nvm/n,本文是对n的介绍。

***********

## ** 流程 **

安装

```
$ npm install -g n
```
查看当前已经安装的node版本以及正在使用的版本（前面有一个o），你可以通过移动上下方向键来选择要使用的版本，最后按回车生效。

```
$ n
```

安装最新的版本
```
$ n latest
```

安装稳定版本
```
$ n stable
```
删除某个版本

```
$ n rm 0.10.1
```
以指定的版本来执行脚本
```
$ n use 0.10.21 some.js
```

***********

## ** 问题 **

我本机使用的shell是zsh,需要在sudo权限下才能正确切换。

退出sudo后,node版本没有切换成功。

`vim ~/.zshrc `

启动编辑，在最后面添加：
```
# auto check node version
 autoload -U add-zsh-hook
 load-nvmrc() {
 if [[ -f .nvmrc && -r .nvmrc  ]]; then
     nvm use
 fi
 }
 add-zsh-hook chpwd load-nvmrc
 load-nvmrc    
```

再执行

`source ~/.zshrc`

即可
***********

## ** 参考 **

[t](https://github.com/tj/n)
[利用n和nvm管理Node的版本](http://weizhifeng.net/node-version-management-via-n-and-nvm.html)
[自动切换项目的node版本](http://www.voidcn.com/article/p-bjkxzbsh-c.html)
