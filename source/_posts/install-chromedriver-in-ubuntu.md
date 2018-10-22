---
title: ubuntu安装chromedriver
date: 2018-10-04 20:36:00
categories: 爬虫
---

###  ** Preface **

本文是对Ubuntu安装chromedriver的记录

***********************

### ** 安装 **

chromedriver有很多版本和浏览器版本需要一一对应，否则无法使用

|chromedriver版本|支持的Chrome版本|
| :---: | :---: |
|v2.40|v66-68|
|v2.39|v66-68|
|v2.38|v65-67|
|v2.37|v64-66|
|v2.36|v63-65|
|v2.35|v62-64|
|v2.34|v61-63|
|v2.33|v60-62|
|v2.32|v59-61|
|v2.31|v58-60|

选择与浏览器版本匹配的chromedriver下载,[chromedriver下载地址](http://chromedriver.storage.googleapis.com/index.html)

然后执行以下命令:
```javascript
#解压，加上执行权限，移动到/usr/bin/文件夹下。(复制则将mv改为cp)
unzip chromedriver_linux64.zip
chmod +x chromedriver
sudo mv chromedriver /usr/bin/
```
************************

### ** 测试代码 **

```js
#!usr/bin/python
# -*- coding:utf-8 -*-
from selenium import webdriver

browser = webdriver.Chrome()
browser.get('http://www.baidu.com/')
```

***********************
###  ** 参考 **

[Python 爬虫相关环境 - 掘金](https://juejin.im/post/5b607624e51d4576b8286f02)
[ubuntu下安装selenium以及chromedriver、geckodriver和phantomjs等驱动 - 明月清風 - CSDN博客](https://blog.csdn.net/qq_23926575/article/details/77268924)
[[Linux] Ubuntu安装ChromeDriver - YasinQiu的博客 - CSDN博客](https://blog.csdn.net/pangtouyu_qy/article/details/80282795)
[python爬虫积累（一）--------selenium+python+PhantomJS的使用 - 今孝 - 博客园](https://www.cnblogs.com/jinxiao-pu/p/6677782.html)
[Python爬虫利器四之PhantomJS的用法](https://cuiqingcai.com/2577.html)