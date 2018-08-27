---
title: Singleton(单例)模式
date: 2017-08-06 15:01:00
categories: 设计模式
---

### ** 概述 **

Singleton(单例)模式,限制了类的实例化次数只能一次。

在该实例不存在的情况下,可以通过一个方法创建一个类来实现创建类的实例;如果实例已经存在,它会简单返回该对象的引用。

**************

### ** 具体实现 **

#### ** ES5 **

```javascript
var mySingleton = (function () {
    var instance;
    function init() {
        function privateMethod() {
            console.log("I am private");
        }
        var privateVariable = "Im also private";
        var privateRandomNumber = Math.random();
        return {
            publicMethod : function () {
                console.log("The public can see me!");
            },
            publicProperty : "I am also public",
            getRandomNumber : function () {
                return privateRandomNumber;
            }
        };
    };

    return {
        getInstance : function () {
            if (!instance) {
                instance = init();
            }
            return instance;
        }
    };
})();

var singleA = mySingleton.getInstance();
var singleB = mySingleton.getInstance();
console.log(singleA === singleB);

```

#### ** ES6 **

```javascript
class Leader {
    constructor () {
        if (!Leader.single) {
            this.level = 'supreme';
            Leader.single = this;
        }
        return Leader.single;
    }
    toString() {
        console.log('I am a leader.');
    }
}


const leader  = new Leader();
const leader1 = new Leader();
console.log(Object.is(leader, leader1));    // true
```
**************

### ** 18年8月21更新 **

***************

#### ** 单例模式实践　**

```javascript
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>单例模式</title>
</head>
<body>
<h1>单例模式</h1>
<button id="loginBtn">登录</button>
<script>
    var createLoginLayer = (function () {
        var div;
        return function () {
            if(!div) {
                div = document.createElement('div');
                div.innerHTML = '我是登录悬浮窗';
                div.style.display = 'none';
                document.body.appendChild(div);
            }
            return div;
        }
    })();

    document.getElementById('loginBtn').onclick = function () {
        console.log('inner');
        var loginLayer = createLoginLayer();
        loginLayer.style.display = 'block';
    };
</script>
</body>
</html>
```
**************
** 优化=>把创建实例对象的职责和管理单例的职责分别放置在两个方法里 **

```javascript
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>单例模式</title>
</head>
<body>
<h1>单例模式</h1>
<button id="loginBtn">登录</button>
<script>
    var getSingle = function (fn) {
       var result;
       return function () {
           return result || (result = fn.apply(this, arguments));
       }
    };

    var createLoginLayer = function () {
        var div = document.createElement('div');
        div.innerHTML = '我是登录悬浮窗';
        div.style.display = 'none';
        document.body.appendChild(div);
        return div;
    };

    var createSingleLoginLayer = getSingle(createLoginLayer);

    var createSingleIframe = getSingle(function () {
       var iframe = document.createElement('iframe');
       document.body.appendChild(iframe);
       return iframe;
    });

    // document.getElementById('loginBtn').onclick = function () {
    //     var loginLayer = createSingleLoginLayer();
    //     loginLayer.style.display = 'block';
    // };


    document.getElementById('loginBtn').onclick = function () {
        var loginLayer = createSingleIframe();
        loginLayer.src = 'http://baidu.com';
    };
</script>
</body>
</html>
```


**************
### ** 推荐阅读 **

[怎么使用es6 的class 优雅地写出单例模式？](https://segmentfault.com/q/1010000007116553/a-1020000007117024)
[深入理解JavaScript系列（25）：设计模式之单例模式](http://www.cnblogs.com/TomXu/archive/2012/02/20/2352817.html)
[ES6语法实践，用ES6重写《JavaScript Patterns》中的设计模式](https://cnodejs.org/topic/5565b4a77d4c64752effb5dd)
[JavaScript设计模式：单例模式](http://www.zcfy.cc/article/javascript-design-patterns-the-singleton-918.html)
[JavaScript设计模式--单例模式](http://www.alloyteam.com/2012/10/common-javascript-design-patterns/)

