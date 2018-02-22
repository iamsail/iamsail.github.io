---
title: 给后端新同学第一次任务的讲解
date: 2017-10-31 18:32:00
categories: Python
tags: 翔工作室
---

## ** preface **

这届后端组大一的新生一共六名同学,三个来自计算机学院,另外三个非计算机学院。

给他们的第一次任务,是55道程序设计题目,少部分题目,涉及到一些算法。计算机学院的同学使用C++写,非计算机学院的同学使用的python。

本来是我和[健勋](http://www.wuya00.top/),负责带非计算机学院的三个学弟。由于健勋就读于国际学院,明年就要出国了,需要准备托福,我就负责了三个学弟。

代码均放在了工作室[github](https://github.com/cumtflyingstudio/novice-task-of-BE-17),有关第一次任务存在的一些问题陆续更新在本文

****************

## ** 问题讲解 **

### ** 输入输出问题 **
```
Example(基础)输入两个数,求出它们的和并输出。样例输入:1 2

样例输入:3
```

学弟们大致都是这样写的

```python
a=input()
b=input()
a=int(a)
b=int(b)
d=a+b
print(d)
```

但是这样的输入是与题目要求不符合的,题目中的输入是在同一行输入两个数,而他们的写法只能在一行输入一个数字

推荐这样写

```python
a,b= map(float, raw_input().split())
```

<span class="under0">** `raw_input()` 将所有输入作为字符串看待，返回字符串类型。 **</span>

注意：`input()` 和 `raw_input()` 这两个函数均能接收 字符串 ，但 `raw_input()` 直接读取控制台的输入（任何类型的输入它都可以接收）。而对于 input() ，它希望能够读取一个合法的 python 表达式，即你输入字符串的时候必须使用引号将它括起来，否则它会引发一个 SyntaxError 。
除非对 `input()` 有特别需要，否则一般情况下我们都是推荐使用 `raw_input()` 来与用户交互。

注意：python3 里 input() 默认接收到的事 str 类型。

以下是参考链接

[raw_input](http://www.runoob.com/python/python-func-raw_input.html)
[split](http://www.runoob.com/python/att-string-split.html)
[map](http://www.runoob.com/python/python-func-map.html)

***************

## ** 循环问题 **

有的同学在上大学前有过一些C语言的基础,然而Python中的for循环有一些不同

在C,C++,或者类C的一些语言中for循环大概如下

```python
for(int i = 0 ; i < n; i++)
    cout << a[i];
```

而在python中设若有如下一个list

```python
a = [100,200,300,400,500]

for x in a
    print x 
```

像这样是没有下标的。而在一些程序设计题当中,有时候是需要控制输出格式的,这样就不太方便

这里有一个解决方案

<span class="under0">** Python内置的`enumerate`函数可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代索引和元素本身: **</span>
```
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C
```

此外listName.index(element)可以得到列表某个元素的下标,len(listName)可以得到某个列表的长度,这样结合起来也可以相互判断

以下是参考链接

[迭代](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014317793224211f408912d9c04f2eac4d2af0d5d3d7b2000)

****************

### ** 持续更新中... **

****************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>