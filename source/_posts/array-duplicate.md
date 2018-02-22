---
title: JS数组去重
date: 2017-04-6 17:32:12
categories: Javascript
---

**数组去重,有很多实现的方法。最近学习ES6，发现一种十分简单的办法。**

先看一下比较常规的解决方法。

一、** 遍历数组,建立新数组，利用indexOf判断是否存在于新数组中,不存在则push进新数组。**
```
    let dedupe = (arr) =>{
        let ret = [];
        for(let i = 0, j = arr.length; i < j; i++){
            if(ret.indexOf(arr[i]) === -1){
                ret.push(arr[i]);
            }
        }
    }
```
二、** 遍历数组,利用object对象保存数组值,判断数组值是否存在object中,未保存则push到新数组。**
```
    let dedupe = (arr) => {
        let  j = arr.length,
             i = 0,
           tmp = {},
           ret = [];

        for(; i < j; i++){
            if(!tmp[arr[i]]){
                tmp[arr[i]] = 1;
                ret.push(arr[i]);
            }
        }
    }
```
三、** 遍历数组，通过indexOf返回值判断与当前索引是否相当。相等则push入新数组。**
```
    let dedupe = (arr) => {
        let ret = [];
        arr.forEach(function(item, index ,array){
            if(arr.indexOf(item) === index){
                ret.push(item);
            }
        });
    }
```
四、** 用到了一点桶排序的思想。以待去重数组的最大值+1为长度,新建数组,用来标记各个值出现的次数。遍历待去重数组,如果只出现一次,则push进入新数组。**
```
    let dedupe = (arr) => {
        let i = 0,
            maxLength = Math.max.apply(null,arr) + 1,
            //ES6,利用扩展运算符
            // maxLength = Math.max(...arr) + 1,
            ret = new Array(maxLength).fill(0),
            ret2 = [];

        for(;i < arr.length; i++){
                ret[arr[i]]++;
                if(ret[arr[i]] == 1){
                    ret2.push(arr[i]);
                }
        }
    }
```
************************************

现在看一下,更简单的方法
```
    function dedupe(array){
        return Array.from(new Set(array));
    }
```
用到了两个知识点

- ES6中新的数据结构Set。** 它类似于数组,只不过其成员值都是唯一的,没有重复值。**

- Array.from()用于将两类对象转换成真正的数组:类似数组的对象(array-like object) 和可遍历(iterable)的对象,其中包括ES6新增的Set和Map结构

**********************************

** 参考 **

- 《ECMAScript6 入门》

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>