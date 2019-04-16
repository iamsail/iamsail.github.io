---
title: 在centos7安装python3.x
date: 2018-12-22 23:39:00
categories: Python
tags: [环境搭建]
---

### ** Preface **

本文是在centos7.1安装python3.x的记录。踩了不少坑，记录下。心酸,docker化势在必行！！！！！！

*******************
### ** 安装python3.x **
** 先安装安装几个必须的包，以方便后续的操作 **
```bash
# wget 用于下载源码包
# gcc 和 make 用于编译
yum -y install wget gcc make  zlib-devel readline-devel  bzip2-devel ncurses-devel sqlite-devel gdbm-devel xz-devel
```

<div style="height:12px"></div>


** 上[Python的官网](https://www.python.org/) 下载源码包 **
```bash
wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tar.xz
```
<div style="height:12px"></div>


** 解包，解压缩 **
```bash
xz -d Python-3.6.1.tar.xz
tar -xvf Python-3.6.1.tar
```
<div style="height:12px"></div>

** 编译 **
```bash
cd Python-3.6.1
./configure --prefix=/usr/local/python3.6 --enable-optimizations
```
先解释下上面的参数，`--prefix `是预期安装目录，`--enable-optimizations `是优化选项（LTO，PGO 等）加上这个 flag 编译后，性能有 10% 左右的优化，但是这会明显的增加编译时间。不过关于 LTO 和 PGO 其实不在今天文章的讨论范围内，感兴趣的可以看看 GCC 中 LTO 的具体实现([GNU Compiler Collection (GCC) Internals: LTO Overview](https://gcc.gnu.org/onlinedocs/gccint/LTO-Overview.html))。
<div style="height:12px"></div>


** 接下来 **
```bash
make && make install
```
<div style="height:12px"></div>

 
** 编译安装完成后，执行 **
```bash
➜  /usr/local/python3.6/bin/python3 --version
Python 3.6.1
```
Python 3 也就安装成功了。
<div style="height:12px"></div>


** 为了避免每次都输入一大串路径，加个链接 **
```bash
➜ ln -s /usr/local/python3.6/bin/python3 /usr/bin/python3
```

*******************
以上的命令整理为如下的shell

```bash
#!/bin/bash
# author: TaoBeier

yum -y install wget gcc make  zlib-devel readline-devel  bzip2-devel ncurses-devel sqlite-devel gdbm-devel xz-devel tk-devel openssl-devel
wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tar.xz
xz -d Python-3.6.1.tar.xz
tar -xvf Python-3.6.1.tar
cd Python-3.6.1
./configure --prefix=/usr/local/python3.6 --enable-optimizations
make
make install
ln -s /usr/local/python3.6/bin/python3 /usr/bin/python3
```
*******************
### ** 安装pip3.x  **


#### ** 安装pip2.x **
```bash
# 首先安装 epel 扩展源
$ sudo yum -y install epel-release

# 安装 python-pip
$ sudo yum -y install python-pip

# 清除 cache
$ sudo yum clean all
通过这种方式貌似只能安装 pip2，想要安装 Python 3 的 pip，可以通过以下的源代码安装方式。
```

#### ** 源码安装pip3.x **
```bash
# 下载源代码
$ wget --no-check-certificate https://github.com/pypa/pip/archive/9.0.1.tar.gz

$ tar -zvxf 9.0.1.tar.gz

$ cd pip-9.0.1

# 使用 Python 3 安装
$ python3 setup.py install
```

#### ** 创建链接 **
```bash
$ sudo ln -s /usr/local/python3.6/bin/pip /usr/bin/pip3
```

#### ** 升级 pip **
```bash
$ pip install --upgrade pip
```

以上的命令整理为如下的shell
```
#!/bin/bash
# author: Sail

yum -y install epel-release python-pip
yum clean all

wget --no-check-certificate https://github.com/pypa/pip/archive/9.0.1.tar.gz
tar -zvxf 9.0.1.tar.gz
cd pip-9.0.1
python3 setup.py install
ln -s /usr/local/python3.6/bin/pip /usr/bin/pip3
```
<div style="height:12px"></div>
*******************

### ** 参考 **

[在 CentOS 7 上安装并配置 Python 3.6 环境](https://segmentfault.com/a/1190000009922582)
[CentOS 7 安装Python3、pip3](https://ehlxr.me/2017/01/07/CentOS-7-%E5%AE%89%E8%A3%85-Python3%E3%80%81pip3/)
[python3中pip3安装出错，找不到SSL](https://blog.csdn.net/jeryjeryjery/article/details/77880227)
[no acceptable C compiler found in $PATH](https://www.jianshu.com/p/5fbbe1435db2)
