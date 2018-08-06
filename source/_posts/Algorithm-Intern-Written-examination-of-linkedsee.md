---
title: 灵犀联云算法实习生笔试
date: 2018-06-24 21:04:30
tags: 笔试
password: 0Algorithm6,
---
### ** Preface **

昨天中午收到了[灵犀联云](https://www.linkedsee.com/)hr的电话,聊了快十分钟。hr很专业也很nice.

还是蛮激动的,毕竟投了3天算法的简历,总算有一家有反馈的了。

有意思的是这家公司的创始团队全是从百度运维那边出来的,这家公司业务就是做智能运维的,今年还拿到了百度的投资。

电话结束过后,hr给我发了笔试邮件,今天上午做了。本文记录下。为了防止泄题,所以我加密了。

其实还是蛮想去的,不过我太菜了,应该是凉了。

*********************

### ** 第一题　**

> 返回第二大的元素,不可以调用sort

本题快排就可以解决

*********************

### ** 第二题　**

> 判断两颗二叉树是否相等(结构和值)

```regexp

```
*********************

### ** 第三题　**

> 非负整数，数字加和到只有一位数，打印值

```regexp

```
这题我是递归解决的,后面补下代码

*********************

### ** 第四题　**
> 两个人，石头，每次只能拿一到三块，我先拿，最后一个有石头拿的人为赢？两个人足够聪明，设计算法，根据石头数量，是否能赢

```regexp

```
*********************
### ** 第五题　**

>股票，每天只能交易一次，k天，有一个数组，股票每天的价格，交易前必须卖完？求最大利润

```regexp

```

*********************

### ** 秋招前端面试更新　**

关于算法的面经我都更新到了[图鸭信息科技算法实习生面试](http://www.sail.name/2018/06/26/algorithm-intern-interview-of-tucodec/),那前端就更新在这篇博客吧,所有的面经等我最终工作搞定后再解封。

这里我多说一句吧,算是对我自己的提醒,在最终工作敲定前,都不要松懈

********************

### ** 老虎证券　**

#### ** 一面　**

老虎证券是8月6号下午面的,从1点56面到接近3点,几乎一个小时吧。3点10收到了hr的电话,说面试官对我特别满意。接下来就是终面了,终面必须现场面,我去北京或者他们安排人过来。希望能够拿下第一个offer。

>1.自我介绍

>盒子模型　　具体怎么设置的　查下

`content-box`
默认值，标准盒子模型。 width 与 height 只包括内容的宽和高， 不包括边框（border），内边距（padding），外边距（margin）。注意: 内边距, 边框 & 外边距 都在这个盒子的外部。 比如. 如果 .box {width: 350px}; 而且 {border: 10px solid black;} 那么在浏览器中的渲染的实际宽度将是370px;
尺寸计算公式：width = 内容的宽度，height = 内容的高度。宽度和高度都不包含内容的边框（border）和内边距（padding）。

`border-box`
width 和 height 属性包括内容，内边距和边框，但不包括外边距。这是当文档处于 Quirks模式 时Internet Explorer使用的盒模型。注意，填充和边框将在盒子内 , 例如, .box {width: 350px; border: 10px solid black;} 导致在浏览器中呈现的宽度为350px的盒子。内容框不能为负，并且被分配到0，使得不可能使用border-box使元素消失

>flex

[Flex基础](http://www.sail.name/2017/07/09/the-base-of-flex/)
[flex垂直居中](http://www.sail.name/2017/07/22/vertical-center-by-flex/)

>position　　sticky

[position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)

>闭包

>js GC机制

>cookie localstorage sessionstorage

>cookie安全问题,加密篡改啥的
待更新

>对数据可视化的了解

>2.反转字符串　　具体了解下有哪些方法

```javascript
function reverse_string(str) {
    let temp = [];
    for(let i = 0;i < str.length; i++) {
       temp.push(str[i]); 
    }
    
    let final_str = [];
    
     for(let i = temp.length;i >=0 ; i--) {
       final_str.push(temp.pop()); 
    }
    
    return string(final_str);
}
```

这里第一次写的时候我忘记了对返回值要做个处理string(),不然返回的是字符串


> 如何把数组转为字符串
  join方法

>3.数组哪些方法是会改变数组本身的
    
[js数组方法 改变原数组和不改变原数组的方法整理](https://blog.csdn.net/love07070707/article/details/79888566)
[js中那些方法不改变原来的数组对象](https://blog.csdn.net/liangklfang/article/details/49300417)
[细说JS数组](https://segmentfault.com/a/1190000008211717)

> 还问题了webpack
　我应该了解一下了,一些常用的loader,以及当初用到的一些性能优化的插件
    
    
>es6 常用的有哪些
    深入下异步和class部分

>4.vue的虚拟dom算法
    对vue的原理部分,和全家桶这两天要了解下
    待更新

>对职业的发展

>对code review怎么看
    
>实习项目有什么特别难忘的bug之类的吗

>有什么想问的
































