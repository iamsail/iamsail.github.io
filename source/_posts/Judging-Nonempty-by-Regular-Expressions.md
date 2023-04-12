---
title: 正则表达式判断非空
date: 2019-04-14 08:37:30
categories: 正则表达式
---

用来判断 textarea 是否全为空（不可全为空格和换行，允许字符前面和后面为空）
```javascript
/^[\s\S]*.*[^\s][\s\S]*$/
```
![1.png](/img/正则表达式/Judging-Nonempty-by-Regular-Expressions/1.png)
### ** 参考链接 **

[正则表达式 ---判断非空 - 鱿太人cccccciel___ - CSDN博客](https://blog.csdn.net/qq_31808899/article/details/77966273)