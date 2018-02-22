---
title: 《JavaScript语言精粹》读书笔记(一)
date: 2017-08-14 17:40:00
categories: Javascript
---

### ** 前言 **

本文是对《JavaScript语言精粹》的一些整理

***********

### ** 内容 **

#### ** 级联形式继承 **

```javascript
var Mammal = function (name) {
    this.name = name;
};

Mammal.prototype.get_name = function () {
    return this.name;
};;

Mammal.prototype.says = function () {
    return this.saying || '';
}

Function.prototype.method = function (name,func) {
    if(!this.prototype[name]){
        this.prototype[name] = func;
        return this;
    }
}

Function.method('inherits',function (Parent) {
        this.prototype = new Parent();
        return this;
});

var Cat = function (name) {
    this.name = name;
    this.saying = 'meow';
}
.inherits(Mammal)
.method('apple',function () {
    console.log("apple");
})

var car = new Cat("sail");
car.apple();
```
这种方式隐藏了无所谓的`prototype`细节。

使用构造器函数存在一个严重的危害。如果在调用构造函数时忘记了在前面加new 前缀,那么this将不会被绑定到一个新对象。悲剧的是,this将被绑定到全局对象。不但没有扩充新对象,反而破坏了全局环境变量。

***********

#### ** 移除字符串首尾空白 **

如今的标准已经有了`String.prototype.trim()`

trim() 方法会从一个字符串的两端删除空白字符。trim() 方法并不影响原字符串本身，它返回的是一个新的字符串。

以前没有这个方法,可以这样实现

```javascript
Function.prototype.method = function (name,func) {
    if(!this.prototype[name]){
        this.prototype[name] = func;
        return this;
    }
}

String.method('trim', function () {
    return this.replace(/^\s+|\s+$/g,'');
})

console.log('"' + "    neat    ".trim() + '"');
```
***********

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
