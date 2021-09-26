---
title: JS中字符和ASCII码相互转换
date: 2021-09-25 09:35:01
categories: Javascript
---

最近碰到了一个需要把数组和字母相互转换的场景。

在JS中可以通过`charCodeAt`把字母转换成`ASCII码`，也可以通过`fromCharCode`把数字转换成字母

```javascript
'A'.charCodeAt()
# 65

'Z'.charCodeAt()
# 90

'a'.charCodeAt()
# 97

'z'.charCodeAt()
# 122

String.fromCharCode(65)
# 'A'
```

*****************

### ** charCodeAt **

`charCodeAt()` 方法返回 0 到 65535 之间的整数，表示给定索引处的 UTF-16 代码单元
- 语法: `str.charCodeAt(index)`
- 参数`index`: 一个大于等于 0，小于字符串长度的整数。如果不是一个数值，则默认为 0。
- 返回值: 指定 `index` 处字符的 `UTF-16` 代码单元值的一个数字；如果 `index` 超出范围，`charCodeAt()` 返回 `NaN`。

举个例子
```javascript
'今天你吃了吗'.charCodeAt(1) 返回'天'的UTF-16 代码单元
# 22825

String.fromCharCode(22825)
# '天'
```

### ** charAt **
`charAt`方法则是返回一个字符串指定位置的字符

```javascript
'一个字符串中返回指定的字符'.charAt(3)
# '符'
```

### ** fromCharCode **

静态 `String.fromCharCode()` 方法返回由指定的 `UTF-16` 代码单元序列创建的字符串
这个`fromCharCode`方法可以传入多个参数
```javascript
String.fromCharCode(65, 66)
# 'AB'
```






*****************

### ** 参考链接 **

- [String.fromCodePoint()](https://es6.ruanyifeng.com/#docs/string-methods#String-fromCodePoint)
- [charCodeAt](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt)