---
title: HTMLElement
date: 2017-11-08 13:21:00
categories: Javascript
---

## ** Preface **

`HTMLElement `接口表示所有的 HTML 元素。一些HTML元素直接实现了`HTMLElement`接口，还有一些间接实现`HTMLElement`接口.

所有的DOM元素都继承于 `HTMLElement` 构造器。通过访问`HTMLElement`的原型,浏览器可以为我们提供任意扩展HTML节点的能力。


***********

## ** demo **

[戳这儿](http://www.sail.name/CSS_Demo/js/HTMLElement.html)

```javascript
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, " +
           "maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>DOM 原型</title>
    <style>
        div{
            background: red;
        }
    </style>
</head>
<body>
<div id="a">a</div>
<script>
    HTMLElement.prototype.remove = function(){
      if(this.parentNode){
          this.parentNode.removeChild(this);
      }
    };

    var a = document.querySelector("#a");
    a.onclick = function () {
        a.remove();
    }

</script>
</body>
</html>
```

在以上代码中,我们在`HTMLElement`原型上增加了`remove()`方法,使得元素本身调用该方法将自己从DOM中删除。


***********

## ** 注意 **

但是需要注意的是,HTML元素是不可以直接通过其构造器进行实例化的,也就是

`var elem = new HTMLElement()`

是无效的。

尽管浏览器暴露了基构造器和原型,它们选择性地禁用了通过构造器创建元素的能力。

***********

## ** 参考 **

《JavaScript 忍者秘籍》
[HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)

