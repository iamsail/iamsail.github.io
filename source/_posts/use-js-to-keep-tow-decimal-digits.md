---
title: JS保留两位小数
date: 2018-01-27 17:04:27
categories: Javascript
---

### ** Preface ** ###

本文是对JS保留两位小数的方法的记录。

****************
测试数据
```javascript
var numObj = 12345.6789;
var numObj = 12345.6;
var numObj = 12345;
```

### ** 方法一 ** ##

`numObj.toFixed(2)`

*****************

`toFixed()` 方法使用定点表示法来格式化一个数。

#### ** 语法 ** ####
`numObj.toFixed(digits)`

#### ** 参数 ** ####
`digits`
小数点后数字的个数；介于 0 到 20 （包括）之间，实现环境可能支持更大范围。<span class="under0">如果忽略该参数，则默认为 0</span>。

#### ** 返回值 ** ####
所给数值的定点数表示法的** 字符串形式 **。

****************
### ** 方法二 ** ##
```javascript
function returnFloat(value){
 var value = Math.round(parseFloat(value)*100)/100;
 var xsd   = value.toString().split(".");
 if (xsd.length == 1) {
    value=value.toString() + ".00";
    return value;
 }
 
 if (xsd.length > 1) {
     if (xsd[1].length < 2) {
        value = value.toString() + "0";
     }
     return value;
 }
}
 var num = 3.1;
 console.log(returnFloat(num));
```
#### ** 解释 **

`var value=Math.round(parseFloat(value)*100)/100`

`parseFloat(value)`将参数转换为浮点数，因为参数有可能是字符串，乘以100是因为要保留两位小数，先将小数点向右移动两个位数，然后再利用Math.round()方法实行四舍五入计算，最后除以100，这样就实现了保留两位小数，并且还具有四舍五入效果。

** 但是这个并不完美，如果参数数字本身的小数位数大于等于2是可以的，如3.1415，但是如3或者3.0这样的还是没有完美的实现。**

`var xsd   = value.toString().split(".");`

所以此句后面的代码,以小数点为分界拆成数组,对数组的长度以及倘若数组长度为2,对数组的第二个元素(即小数点后面的数字位数进行了判断处理)


****************
### **　参考 ** ##
[Number.prototype.toFixed()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed)
[javascript实现保留两位小数的多种方法](http://www.jb51.net/article/76584.htm)

