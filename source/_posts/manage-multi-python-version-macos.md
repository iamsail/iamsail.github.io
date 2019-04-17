---
title: macOS pyenv管理多个版本的python
date: 2019-04-17 14:26:00
categories: Python
---
### ** Preface **
本文是在macOS,使用`pyenv`管理多个版本的`python`的记录
******************

<span class="under0"> ** Pyenv只会管理通过Pyenv安装的Python版本，你自己在Python官网上下载的直接安装的Pyenv并不能被管理！！！同样除了系统自带的python包外,其他直接安装的python包是识别不出来的,即使使用的brew安装的也识别不出来. **</span>

******************
### ** 安装 **

#### ** 安装homebrew **
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew -v
```

#### ** 安装pyenv **
```
$ brew update
$ brew install pyenv
$ pyenv -v
```
<div style="height:12px"></div>

*******************

#### ** 修改配置 **
在profile文件里面添加一句,编辑`.bash_profile`(bash)或者`.zshrc`(zsh),如果shell是bash,则编辑`.bash_profile`。是zsh,则编`.zshrc`。
若不存在`.bash_profile`，则输入如下命令，创建文件
```
touch .bash_profile
```
添加
```
eval "$(pyenv init -)" 
```
刷新之前配置的文件.
```
source .bash_profile
# or
source .zshrc
```
<div style="height:12px"></div>

******************
### ** 使用 **
```
# 查看pyenv支持哪些Python版本
pyenv install --list

# 查看当前使用的python版本
pyenv version

# 安装一个python版本如3.5.6
pyenv install 3.5.6

# 安装完成之后需要对数据库进行更新：
pyenv rehash

# 卸载一个python版本如3.5.6
pyenv uninstall  3.5.6

# 设置全局python版本如3.5.6
pyenv global 3.5.6
//很多人不推荐这么做,说是mac操作系统的文件也会调用原生的2.7的python版本
//这种说法感觉有点:恐惧来自未知的感觉.持保留意见

# 设置目录级python版本如3.5.6
pyenv local 3.5.6


# 为当前shell会话设置python版本如3.5.6
pyenv shell 3.5.6
```


```
pyenv常用的命令说明：

使用方式: pyenv <命令> [<参数>]

命令:
  commands    查看所有命令
  local       设置或显示本地的Python版本
  global      设置或显示全局Python版本
  shell       设置或显示shell指定的Python版本
  install     安装指定Python版本
  uninstall   卸载指定Python版本)
  version     显示当前的Python版本及其本地路径
  versions    查看所有已经安装的版本
  which       显示安装路径
```

******************
### ** 参考链接 **
[macOS 安装和管理多个Python版本 - 掘金](https://juejin.im/post/5b42cbb15188251abf413ee6)
[mac下利用pyenv管理多个版本的python - 掘金](https://juejin.im/post/5c389b4b6fb9a049e2323a8a)