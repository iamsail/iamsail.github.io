---
title: zsh command not found pip
date: 2018-04-06 20:26:00
categories: Python
tags: [Shell]
---

### ** preface **
 
在zsh中执行`pip xxx`,出现错误`zsh: command not found: pip`。 当然我很确定自己是有安装pip的,应该是应该切换了shell,导致环境变量出了问题。
    
无奈百度谷歌到的办法都不适合我,最后bing解决了。如果你也折腾了很久,或许可以一试。

*******************

![1.png](/img/python/zsh-command-not-found-pip/1.png)

如图

先执行 `sudo apt-get install --reinstall python3-pip`  

查看是否安装成功 `pip3 -V`

再执行 `pip3 install --upgrade pip`

接着 `pip --version` 即可

********************

### ** 解释 **

之所以`reinstall`是因为虽然安装了,但是可能某些文件等之类的缘故,--reinstall 将会重写所有的文件覆盖这个包。

搞定pip3过后,再回头升级pip.

*******************

### ** 参考 **

[Use Python3-pip](https://github.com/pypa/pip/issues/3565)
[zsh command cannot found pip](https://stackoverflow.com/questions/42870537/zsh-command-cannot-found-pip)