---
title: vim插件配置(ubuntu)
date: 2018-06-22 12:53:30
categories: Vim 
---

### ** Preface **

本文是我配置`vim`插件的记录。操作系统是`ubuntu16.04`

************************

### ** 安装Vundle **

Vundle是Vim的一个插件管理器，基于git，通过Vundle可以方便的安装github上的Vim插件。

首先需要确保vim的版本大于等于7.3:

```
> vim -v
```

如果版本不满足,执行以下命令自动升级

```shell
sudo apt-get update 
sudo apt-get upgrade vim 
```

确认版本满足后开始安装

克隆项目到本地
```shell
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim 
```

配置`vimrc`文件 

`vim ~/.vimrc `

```regexp
set nocompatible               " be iMproved
filetype off                   " required!
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()
" let Vundle manage Vundle
" required! 
Bundle 'gmarik/vundle'
" My Bundles here:
filetype plugin indent on     " required!
"
" Brief help
" :BundleList          - list configured bundles  列出所有已配置的插件
" :BundleInstall(!)    - install(update) bundles　 
" :BundleSearch(!) foo - search(or refresh cache first) for foo
" :BundleClean(!)      - confirm(or auto-approve) removal of unused bundles
" :PluginList       - 列出所有已配置的插件
" :PluginInstall     - 安装插件,追加 `!` 用以更新或使用 :PluginUpdate
" :PluginSearch foo - 搜索 foo ; 追加 `!` 清除本地缓存
" :PluginClean      - 清除未使用插件,需要确认; 追加 `!` 自动批准移除未使用插件
" see :h vundle for more details or wiki for FAQ
" NOTE: comments after Bundle command are not allowed..
```

*********************

### ** 安装NERDTree **

** nerdtree，用来浏览文档树 **


在`.vimrc`中加入

`Bundle 'scrooloose/nerdtree' " 加入NERDTree`

保存退出，并重新进入vim，执行`:PluginInstall`，等待安装，安装完成会有`Done`状态提示，这样NERDTree插件就安装上了，执行`:NERDTree`命令，侧栏文件树形目录就出来了。可以映射快捷键调出NERDTree，在`.vimrc`中加入`:map <C-f> :NERDTree<CR>`，这样就可以使用`Ctrl+f`来调出侧边栏。

最后`.vimrc`如下

```regexp
set nocompatible               " be iMproved
filetype off                   " required!
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()
" let Vundle manage Vundle
" required! 
Bundle 'gmarik/vundle'
Bundle 'scrooloose/nerdtree' 
" My Bundles here:
filetype plugin indent on     " required!
:map <C-f> :NERDTree<CR>
"
" Brief help
" :BundleList          - list configured bundles
" :BundleInstall(!)    - install(update) bundles
" :BundleSearch(!) foo - search(or refresh cache first) for foo
" :BundleClean(!)      - confirm(or auto-approve) removal of unused bundles
"
" see :h vundle for more details or wiki for FAQ
" NOTE: comments after Bundle command are not allowed..

```

快捷键
```regexp
ctrl + w + h    光标 focus 左侧树形目录
ctrl + w + l    光标 focus 右侧文件显示窗口
ctrl + w + w    光标自动在左右侧窗口切换
ctrl + w + r    移动当前窗口的布局位置
o       在已有窗口中打开文件、目录或书签，并跳到该窗口
go      在已有窗口 中打开文件、目录或书签，但不跳到该窗口
t       在新 Tab 中打开选中文件/书签，并跳到新 Tab
T       在新 Tab 中打开选中文件/书签，但不跳到新 Tab
i       split 一个新窗口打开选中文件，并跳到该窗口
gi      split 一个新窗口打开选中文件，但不跳到该窗口
s       vsplit 一个新窗口打开选中文件，并跳到该窗口
gs      vsplit 一个新 窗口打开选中文件，但不跳到该窗口
!       执行当前文件
O       递归打开选中 结点下的所有目录
x       合拢选中结点的父目录
X       递归 合拢选中结点下的所有目录
e       Edit the current dif
双击    相当于 NERDTree-o
中键    对文件相当于 NERDTree-i，对目录相当于 NERDTree-e
D       删除当前书签
P       跳到根结点
p       跳到父结点
K       跳到当前目录下同级的第一个结点
J       跳到当前目录下同级的最后一个结点
k       跳到当前目录下同级的前一个结点
j       跳到当前目录下同级的后一个结点
C       将选中目录或选中文件的父目录设为根结点
u       将当前根结点的父目录设为根目录，并变成合拢原根结点
U       将当前根结点的父目录设为根目录，但保持展开原根结点
r       递归刷新选中目录
R       递归刷新根结点
m       显示文件系统菜单
cd      将 CWD 设为选中目录
I       切换是否显示隐藏文件
f       切换是否使用文件过滤器
F       切换是否显示文件
B       切换是否显示书签
q       关闭 NerdTree 窗口
?       切换是否显示 Quick Help

# 切换标签页
:tabnew [++opt选项] ［＋cmd］ 文件	建立对指定文件新的tab
:tabc   关闭当前的 tab
:tabo   关闭所有其他的 tab
:tabs   查看所有打开的 tab
:tabp   前一个 tab
:tabn   后一个 tab

标准模式下： gt , gT 可以直接在tab之间切换。
```
**********************
其他不错的插件我用一段时间过后再来本文补充～

**********************
### ** 参考 **

[Ubuntu 16.04 安装Vundle](https://blog.csdn.net/wr132/article/details/54019046)
[使用Vundle管理vim的插件](https://www.cnblogs.com/davidhhuan/archive/2013/01/06/2846982.html)
[vim插件管理器：Vundle的介绍及安装（很全）](https://blog.csdn.net/zhangpower1993/article/details/52184581)
[有哪些好用到爆的vim插件？](https://www.zhihu.com/question/23590572)
[Vim: 使用Vundle安装NERDTree](https://www.cnblogs.com/davidhhuan/archive/2013/01/06/2846982.html)
[NERDTree快捷键](http://mufool.com/2016/07/08/vim-nerdtree/)
[使用map自定义快捷键](https://blog.csdn.net/jasonding1354/article/details/45372007)
[vim插件goyo与limelight](https://blog.csdn.net/Demorngel/article/details/70474496)
[vim显示行号、语法高亮、自动缩进的设置](https://blog.csdn.net/chuanj1985/article/details/6873830)
[把vim配置成顺手的python轻量级IDE（一）](https://www.jianshu.com/p/f0513d18742a)
[YouCompleteMe](https://github.com/Valloric/YouCompleteMe#javascript-semantic-completion)
[vim进阶 | 使用插件打造实用vim工作环境](https://juejin.im/post/5a38c37f6fb9a0450909a151)
