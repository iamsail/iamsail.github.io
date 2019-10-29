---
title: JS函数前面的一元运算符
date: 2019-10-13 21:36:45
categories: Javascript
---

### ** Preface **

在改祖传代码的时候，我发现代码中有的地方，在函数表达式前面加了一个`!`。其实这个`!`就是让这个函数变成了自执行函数表达式，从函数声明转换成了函数表达式。

**********************

比如我们有这样一个函数

```javascript
function() {console.log('1111');}
```

这是一个函数声明,函数是不能执行的。除非将该函数赋值为一个表达式,函数表达式是可以执行的。

```javascript
let a = function() {console.log('1111');}
a();
```

除了上面那样执行，我们还可以写成如下这样的自执行函数表达式

```javascript
(function() {console.log('1111')}());
(function() {console.log('1111')})();
```

其实`!`或者前函数前面加一个一元运算符，也是讲一个函数声明转为成一个函数表达式

```javascript
!function() {console.log('1111');}
-function() {console.log('1111');}
+function() {console.log('1111');}
# 甚至可以写成如下
true && function() {console.log('1111');}
0 , function() {console.log('1111');}
```

回到文章开头提到的问题，我看到的祖传代码如下

```javascript
+function() {console.log('1111');}()
```
`function() {console.log('1111');}` 是一个函数声明,前面加上`+`,就成了一个表达式。后面再加上一个`()`,就成了立即执行函数。

**********************

### ** 参考 **

- [function与感叹号](https://swordair.com/function-and-exclamation-mark/)
- [javascript 函数前面有加号，叹号的意思](https://blog.csdn.net/ForMyQianDuan/article/details/51888965)

