---
title: 判断是PC还是移动端
date: 2019-10-13 20:57:45
categories: Javascript
---

### ** Preface **

最近上班真的很累，很多东西都没有时间来整理出来。最近写了一些h5,本文是对判断用户是PC还是移动端的记录。

********************

```javascript
isPc() {
  const userAgentInfo = navigator.userAgent;
  const Agents = ["Android", "iPhone", "SymbianOS", "Windows Phone", "iPad", "iPod"];  
  const filtrArrLenthg = Agents.filter(item => userAgentInfo.indexOf(item) > 0).length;
  return filtrArrLenthg === 0 ?  true : false;
},
```

上面代码片段，所做的工作就是拿到用户的`userAgentInfo`,判断这个字符串中是否有移动端的信息,如果有,则是移动端,反之就是PC。

比如我在chrome浏览器中`navigator.userAgent`的值就是
```
"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Safari/537.36"
```
不能命中`Agents`的任何一个元素, 所以就是PC。
******************

### ** 参考 **

- [判断客户端是PC还是移动端的问题？](https://segmentfault.com/q/1010000013079292)
- [js判断客户端是pc端还是移动端](https://blog.csdn.net/kongjiea/article/details/17612899)
