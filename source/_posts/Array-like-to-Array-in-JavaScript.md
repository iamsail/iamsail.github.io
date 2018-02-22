---
title: JS类数组转数组
date: 2017-05-15 18:39:17
categories: Javascript
---

#### ** JS类数组转数组 **

这个问题短短5天内,我已经遇见两次了。

第二次是,今天在一个交流群看见别人问。

第一次是,本月12号在上海面试阅文集团前端实习生。

二面面试官问** 如何将arguments转为数组。**

我给了Array.from()方法

面试官说不用ES6呢

那就遍历,push进一个新数组。

这个效率有点低,有没有更高效的方法。

......

之所以还没写面试相关的博客,是因为在阅文只面试了一、二技术面。

还剩下hr面没面。据二面说hr面大概在一周后。

** 等面完hr面,最终面试结果出来,会对本次面试做些整理。**

*************************************

#### ** 首先要明确,什么是类数组(ArrayLike) **

- 拥有length属性，其它属性（索引）为非负整数(对象中的索引会被当做字符串来处理，这里你可以当做是个非负整数串来理解)

- 不具有数组所具有的方法

#### ** 解决 **

** 方法一 **

```
    function list() {
        return Array.from(arguments);
    }
```

*********************

** 方法二 **

```
    let a = {'0':'I','1':'am','2':'Sail','length':3};
    let c = {'1':'I','2':'am','4':'Sail','length':3};

    let arrayLikeToArray = arrLike =>{

        let newArray = [];

        for(let i=0 ;i < arrLike.length; i++){
            newArray.push(arrLike[i]);
        }

        return newArray;
    };

    arrayLikeToArray(a);
```

关于这个函数,** 如果传入的类数组的属性是从0到某个整数n依次递增的,是一切ok的。如果不是,会和预先的结果有区别。**

上面特意给出了两组测试数据,以便加深理解。

** 另外要特别强调的是,上面这段代码,是不适用于处理arguments的。(没错,我是故意这样写的)**

这里需要提下箭头函数几个需要注意的点

- 函数体内的this对象,绑定定义时所在的对象,而不是使用时所在的对象

- 不可以当作构造函数,也就是说,不可以使用new命令,否则抛出一个错误

- 不可以使用arguments对象,该对象在函数体内不存在。

- 由于this在箭头函数中被绑定,所以不能使用call()、apply()、bind()这些方法去改变this的指向

**********************

** 方法三 **

```
    function list() {
      return Array.prototype.slice.call(arguments);
    }

    var list1 = list(1, 2, 3); // [1, 2, 3]
```

********************************

** 方法四 **

```
    var unboundSlice = Array.prototype.slice;
    var slice = Function.prototype.call.bind(unboundSlice);

    function list() {
      return slice(arguments);
    }

    var list1 = list(1, 2, 3); // [1, 2, 3]
```

*********************************

#### ** 参考 **

- [js类数组转数组的方法](http://www.jianshu.com/p/f8466e83cef0)
- [Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice?v=example)
- [js类数组转数组的方法（ArrayLike）](http://www.cnblogs.com/guorange/p/6668440.html)
- [js将类数组转成数组](http://blog.csdn.net/liaozhongping/article/details/51075343)
- [Array.prototype.slice应用和原理探析](http://blog.csdn.net/warhin/article/details/50922314)

********************************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>