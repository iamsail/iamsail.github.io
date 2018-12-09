---
title: BeautifulSoup4 UserWarning
date: 2018-09-23 10:30:00
categories: 爬虫
---

### ** Preface **

写爬虫的时候遇到了这样一个警告

代码如下:

```python
from urllib.request import urlopen
from urllib.error import HTTPError
from bs4 import BeautifulSoup

def download(url):
    print('Downloading:',url)
    try:
        html = urlopen(url)
    except HTTPError as e:
        print('Download error:',e)
        html = None
    return html

html = download('https://www.sail.name/')
bsObj = BeautifulSoup(html.read())
print(bsObj)

```


```
UserWarning: No parser was explicitly specified, so I'm using the best available HTML parser for this system ("lxml"). This usually isn't a problem, but if you run this code on another system, or in a different virtual environment, it may use a different parser and behave differently.

The code that caused this warning is on line 16 of the file one.py. To get rid of this warning, change code that looks like this:

 BeautifulSoup(YOUR_MARKUP})

to this:

 BeautifulSoup(YOUR_MARKUP, "lxml")

  markup_type=markup_type))
```

根据提示信息,是因为没有指定解析器

以下是主要的解析器,以及它们的优缺点:

|解析器|   使用方法   |优势|劣势|
| :------: | :------------------------:  | :------: | :------: |
|Python标准库| `BeautifulSoup(markup, "html.parser")` | `1.Python的内置标准库 2.执行速度适中 3.文档容错能力强 `| Python 2.7.3 or 3.2.2)前 的版本中文档容错能力差 |
|`lxml HTML` 解析器| `BeautifulSoup(markup, "lxml")` | `1.速度快 2.文档容错能力强 `| 需要安装C语言库 |
|`lxml XML` 解析器| `BeautifulSoup(markup, "lxml")` | `1.速度快 2.文档容错能力强 `| 需要安装C语言库 |
|html5lib| `BeautifulSoup(markup, "html5lib")` | `1.最好的容错性 2.以浏览器的方式解析文档 3.生成HTML5格式的文档`| 1.速度慢 2.不依赖外部扩展 |


![1.png](/img/爬虫/BeautifulSoup4-UserWarning/1.png)

**<span class="under0"> 推荐使用lxml作为解析器,因为效率更高. 在Python2.7.3之前的版本和Python3中3.2.2之前的版本,必须安装lxml或html5lib, 因为那些Python版本的标准库中内置的HTML解析方法不够稳定. </span>**

增加解析器即可:

```python
from urllib.request import urlopen
from urllib.error import HTTPError
from bs4 import BeautifulSoup

def download(url):
    print('Downloading:',url)
    try:
        html = urlopen(url)
    except HTTPError as e:
        print('Download error:',e)
        html = None
    return html

html = download('https://www.sail.name/',"lxml")
bsObj = BeautifulSoup(html.read())
print(bsObj)

```

********************** 

### ** 参考 **
[Beautiful Soup 4.2.0 文档](https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html)
[BeautifulSoup4 UserWarning](https://blog.csdn.net/ace_fei/article/details/50466584)
[Markdown插入表格语法](https://www.jianshu.com/p/2df05f279331)
[表情符](https://www.kancloud.cn/thinkphp/github-tips/37887)
[用emoji表情提交代码指南](https://github.com/muwenzi/Program-Blog/issues/71)
[程序员提交代码的 emoji 指南——原来表情文字不能乱用](https://www.h5jun.com/post/gitmoji.html)
[gitmoji的使用](https://www.wenjunjiang.win/2016/11/22/gitmoji%E7%9A%84%E4%BD%BF%E7%94%A8/)
