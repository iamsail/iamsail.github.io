---
title: 修改github仓库的语言类型
date: 2017-03-25 18:28:31
categories: github
---
有个问题困惑了不久,github所有repo的语言类型都是html

可一些仓库明明css，js，php的代码更多...

今天查了下,发现** github是使用 [Linguist](https://github.com/github/linguist) 来detect所使用的语言,会根据项目里文件数目最多的文件类型,识别项目类型。**

******
- 解决办法

项目根目录添加 .gitattributes 文件

    *.languageA linguist-language=languageB

作用就是把项目里的 languageA 文件, 识别成 languageB 语言。
可以修改多个语言，也就是

    *.languageA linguist-language=languageB

    *.languageC linguist-language=languageD

******************

- windows系统中并不好直接创建名为 .gitattributes 的文件
- 会提示 必须键入文件名
- 通过命令创建文件

    <code>touch .gitattributes</code>

- 如果对命令不熟悉,可以看下我的[Ubuntu中的拼音问题](http://www.sail.name/2017/02/28/about-the-pin-ying-in-linux/)

*********************
** 参考 **
- [请教如何修改github上仓库的项目语言?](https://www.zhihu.com/question/47249333/answer/129215637)
- [修改GitHub上项目语言显示的问题](http://www.tuicool.com/articles/bI7f6rE)

