---
title: macOS安装labelImg踩坑汇总
date: 2020-03-15 23:00:01
categories: 深度学习
tags: [前端智能化, 数据集]
---
### ** Preface **

最近有一个涉及到计算机视觉相关的项目，网上没有合适的数据集，需要自己整理一个数据集出来。
`LabelImg`作为图片标注工具，是在进行图片识别和视频分类等机器学习任务的训练集准备，不可少的工具。这里我也使用了`LabelImg`来做数据的标注。

*******************

### ** 如何安装labelImg **
这里推荐看github官方文档，根据自己所使用的操作系统，进行安装。
因为我的系统是Mac OS X，所以执行如下命令
```
brew install python3
pip3 install pipenv
pipenv run pip install pyqt5==5.13.2 lxml
pipenv run make qt5py3
python3 labelImg.py
[Optional] rm -rf build dist; python setup.py py2app -A;mv "dist/labelImg.app" /Applications
```

但是在上面的命令执行过程中，可能会遇到一些问题，导致安装失败。我将整个安装过程所踩的坑整理在下方。

*************************

### ** 问题汇总 **

### ** 需要先将labelImg的代码仓库克隆到本地 **

上面提到的安装命令有一个是`python3 labelImg.py`,所以需要先有这个文件。

执行命令
```git
git clone git@github.com:tzutalin/labelImg.git
cd /labelImg-master
```

*******************

### ** 指定镜像源 **
没有指定镜像源，使用官方的镜像源，可能网速会很慢。这里推荐使用清华的镜像源，示例
```git
pip3 install lxml -i https://pypi.tuna.tsinghua.edu.cn/simple
```

*******************

### ** 安装pyQt5 **
安装pyQt5,会报错。最终发现是因为python安装没有带openssl这个库。
`macOS High Sierra: ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib? `

解决办法
```
执行如下命令

brew uninstall openssl && brew install openssl && CFLAGS="-I$(brew --prefix openssl)/include" LDFLAGS="-L$(brew --prefix openssl)/lib" pyenv install 3.7.0

或者

brew uninstall --ignore-dependencies openssl && brew install openssl && CFLAGS="-I$(brew --prefix openssl)/include" LDFLAGS="-L$(brew --prefix openssl)/lib" pyenv install 3.7.0

# 然后再安装 PyQt5
pip3 install PyQt5 --default-timeout=1000 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

*******************
### ** RFE: pyenv update should regenerate shims unconditionally **

执行如下命令
```
pyenv rehash
```
*******************
### ** ReadTimeoutError **
下载python库的时候，由于国内网络原因，python包的下载速度非常慢。会因为抛出错误`ReadTimeoutError`,而报错。

解决办法添加参数`--default-timeout=1000`即可，示例如下

```
pip3 install PyQt5 --default-timeout=1000
```

*******************

### ** xcrun: error: active developer path (“/Applications/Xcode.app/Contents/Developer”) does not exist **

如果报了这个错，执行如下命令

```
sudo xcode-select --reset
```
*******************

### ** 如果某一个包，安装过后，还是提示没有 **

上面的安装命令中，有的使用`pipenv`进行安装的。如果安装过后执行命令还是提示找不到的话，可以使用pip/pip3再安装一次。

*******************

### ** 参考资料 **

- [tzutalin/labelImg](https://github.com/tzutalin/labelImg)
- [macOS High Sierra: ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib? #993](https://github.com/pyenv/pyenv/issues/993)
- [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)
- [更改pip源至国内镜像，显著提升下载速度](https://blog.csdn.net/lambert310/article/details/52412059)
- [解决pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.](https://yq.aliyun.com/articles/619208)
- [使用 pyenv 管理 Python 版本](http://einverne.github.io/post/2017/04/pyenv.html)
- [https://stackoverflow.com/questions/35009531/xcrun-error-active-developer-path-applications-xcode-app-contents-developer/35009644](xcrun: error: active developer path (“/Applications/Xcode.app/Contents/Developer”does not exist
Ask)
- [如何用Paython制作自己的图片数据集
](https://imyong.top/2018/05/25/%E5%A6%82%E4%BD%95%E7%94%A8Paython%E5%88%B6%E4%BD%9C%E8%87%AA%E5%B7%B1%E7%9A%84%E5%9B%BE%E7%89%87%E6%95%B0%E6%8D%AE%E9%9B%86/)
- [You are using pip version 19.0.3, however version 20.0.2 is available.You should consider upgrading via the 'pip install --upgrade pip' command. 的解决办法](https://blog.csdn.net/mbytes/article/details/104102814)
- [RFE: pyenv update should regenerate shims unconditionally](https://github.com/pyenv/pyenv/issues/1068)
