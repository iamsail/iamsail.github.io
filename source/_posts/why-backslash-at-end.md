---
title: 为什么行末是\
date: 2017-02-19 19:14:56
categories: 代码人生
---

假期初学VUE，写todolist的时候，发现字符串换行的时候，末尾有\。

![backslash-1.jpg](/img/codelife/backslash-1.jpg)
![backslash-2.jpg](/img/codelife/backslash-2.jpg)

别人给我的解释是，** 表示字符串还没结束。**
这个说法是不太准确的。

********

今天看python基础指南(第二版)明白了。
- 普通字符串(py中还有长字符串,用三个引号代替普通引号)可以跨行，如果一行之中最后一个字符是反斜线，那么，换行符本身就"转义"了，也就是被忽略了。

所以字符串换行的时候，末尾有\，是因为，转义掉行末的换行符。
<hr />
    <p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
    </p>
