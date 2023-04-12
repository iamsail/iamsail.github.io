---
title: 五分钟跳转回登录页面
date: 2019-09-07 18:09:45
categories: Javascript
---

### ** Preface **

最近业务中有一个小需求是, 用户五分钟没有操作, 跳转回登录页面。

**********************

代码实现如下: 

```javascript
// 页面最外层的dom节点
let income = this.$refs.income; 

let timer;
// 函数防抖
function startTimer(){
    clearTimeout(timer);
    timer = setTimeout(function(){
        // todo: 清空cookie 和 token
        window.location.href="/login.html"; 
    },  5 * 60 * 1000);
}

income.onmousemove = income.onmousedown = income.onclick = income.ontouchstart = income.ontouchmove = income.ontouchend = startTimer;

// 进入页面, 触发一下事件
income.onclick();
```



