---
title: p标签不能嵌套块级元素
date: 2017-03-2 23:16:27
categories: HTML&&CSS
---
今天周玥问了我一个问题。
问题解决的关键在于** P标签不能嵌套其他块级元素。**

这个之前遇见过，却渐渐忘却了，今天记录下来。
*************
比如有这样一段代码

 ![p-qiantao1.png](/img/htmlcss/p-qiantao-one.png)

在浏览器中却会被渲染成

 ![p-qiantao2.png](/img/htmlcss/p-qiantao-tow.png)
*************
在对p写的样式中,和文本有关的样式都没有了作用的对象。
p标签不能嵌套其他的块级元素，导致解析出来的html与原本的有出入。

************
- 参考
- [常见的块状元素与内联元素](http://blog.csdn.net/dynadotwebb/article/details/17787355)
- [对p标签嵌套块级元素的思考](http://wuxy720.iteye.com/blog/2325985)
