---
title: Zsh-command-not-found-jupyter 
date: 2018-06-09 13:02:00
categories: Python
---
今天安装jupyter后,在终端执行`jupyter notebook`使用提示

`Zsh: command not found: jupyter`

后来找到了一个解决办法

先执行`pip3 show jupyter`

再执行`ipython notebook`即可

*******************

Python安装pip包的时候权限出现问题

sudo解决了权限问题，但是pip安装有个本地缓存目录，如果是用sudo，这个目录会写到root用户的home目录下（一般是/root），不用sudo，就写到当前用户home目录下（一般是/home/username）

sudo也提供了选项 -h ，表示用sudo的权限，但又是用当前用户的home目录，所以最佳方式是：

```
sudo -h pip install -U Pillow
```
*******************

### ** 参考 **

[Zsh: command not found: jupyter ](https://github.com/jupyter/help/issues/317)
[pip install 执行过程中遇到的各种问题](https://www.cnblogs.com/feixiablog/p/8320602.html)