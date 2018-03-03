---
title: Anaconda
date: 2017-08-11 16:07:00
categories: Python
---

### ** 前言 ** 

因为开始接触机器学习,重拾了Python。
<span class="under0"> ** 这次我选择了`Anaconda`,因为看重了其内置了常用的科学计算包。** </span>

********

### ** Anaconda **

[Anaconda](https://www.continuum.io/downloads)是一个用于科学计算的Python发行版，支持 Linux, Mac, Windows系统，提供了包管理与环境管理的功能，可以很方便地解决多版本python并存、切换以及各种第三方包安装问题。

Anaconda利用工具/命令conda来进行package和environment的管理，并且已经包含了Python和相关的配套工具。

### ** Conda **

conda 是 Anaconda 下用于包管理和环境管理的工具，功能上类似 pip 和 vitualenv 的组合。安装成功后 conda 会默认加入到环境变量中，因此可直接在命令行窗口运行命令 conda。

#### ** 多版本python **

```
# 查看帮助
conda -h 

# 基于python3.6版本创建一个名字为python36的环境
conda create --name python36 python=3.6 

****** 如果创建新的python环境，比如3.4，运行conda create -n python36 python=3.6之后，
conda仅安装python 3.6相关的必须项，如python, pip等，如果希望该环境像默认环境那样，安装anaconda集合包

# 在当前环境下安装anaconda包集合
conda install anaconda
 
# 结合创建环境的命令，以上操作可以合并为
conda create -n python36 python=3.4 anaconda
# 也可以不用全部安装，根据需求安装自己需要的package即可

******

# 激活此环境
activate python36   # for Windows
source activate python36 # linux/mac

# 再来检查python版本，显示是 3.6
python -V  

# 退出当前环境
deactivate python36 
source deactivate python36 # for Linux & Mac

# 删除该环境
conda remove -n python36 --all

# 或者 
conda env remove  -n python36

# 查看所有安装的环境
conda info -e
python36              *  D:\Programs\Anaconda3\envs\python36
root                     D:\Programs\Anaconda3

```

#### ** 包管理 **

```
# 安装scipy
conda install scipy
# conda会从从远程搜索scipy的相关信息和依赖项目，对于python 3.6，conda会同时安装numpy和mkl（运算加速的库）
 
# 查看已经安装的packages
conda list
# 最新版的conda是从site-packages文件夹中搜索已经安装的包，不依赖于pip，因此可以显示出通过各种方式安装的包

# 查看当前环境下已安装的包
conda list
 
# 查看某个指定环境的已安装包
conda list -n python36
 
# 查找package信息
conda search numpy
 
# 安装package
conda install -n python36 numpy
# 如果不用-n指定环境名称，则被安装在当前活跃环境
# 也可以通过-c指定通过某个channel安装
 
# 更新package
conda update -n python36 numpy
 
# 删除package
conda remove -n python36 numpy

```
conda将conda、python等都视为package，因此，完全可以使用conda来管理conda和python的版本，例如

```
# 更新conda，保持conda最新
conda update conda
 
# 更新anaconda
conda update anaconda
 
# 更新python
conda update python
# 假设当前环境是python 3.6, conda会将python升级为3.6.x系列的当前最新版本
```
#### ** 设置镜像 **

```
# 添加Anaconda的TUNA镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
# TUNA的help中镜像地址加有引号，需要去掉
 
# 设置搜索时显示通道地址
conda config --set show_channel_urls yes
```
### ** 踩坑 **

在跑我的第一个机器学习程序的时候,出现了以下的错误

![1.png](/img/python/Anaconda/1.png)


在网上看了些解决方案,都不太靠谱

我的解决方案是

<span class="under0"> ** 删除了自己在系统里安装的python,使用Anaconda中的python。当然我使用的Pycharm中的`Project Interpreter`也是Anaconda中的python. **</span>

********
### ** 参考 **

[Anaconda使用总结](http://python.jobbole.com/86236/)
[Anaconda 入门安装教程](https://foofish.net/anaconda-install.html)
[初学python者自学anaconda的正确姿势是什么？？](https://www.zhihu.com/question/58033789)

