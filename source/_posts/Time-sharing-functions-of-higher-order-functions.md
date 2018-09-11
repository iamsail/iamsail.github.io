---
title: 高阶函数之分时函数
date: 2018-09-04 15:25:00
categories: 设计模式
---

### ** 高阶函数 **

高阶函数是指至少满足下列条件之一的函数:

1.函数可以作为参数被传递
2.函数可以作为返回值输入

******************************
### ** 分时函数 **

应用场景:WebQQ的好友列表,列表中通常有成百上千个好友,如果一个好友用一个节点来表示,当我们在页面中渲染这个列表的时候,可能要一次性往页面中创建成百上千个节点。

在短时间内往页面大量添加DOM节点会让浏览器卡顿甚至卡死,代码如下

```javascript
    var ary = [];
    for (var i = 1; i <= 1000; i++) {
        ary.push(i);

    }

    var renderFriendList = function (data) {
        for (var i = 0, l = data.length; i < l; i++) {
            var div = document.createElement('div');
            div.innerHTML = i;
            document.body.appendChild(div);
        }  
    };

    renderFriendList(ary)
```

分时函数`timeChunk`,让创建节点的工作分批进行

```javascript
    var timeChunk = function (ary, fn, count) {
        var obj,
            t;

        var len = ary.length;

        var start = function () {
            for(var i = 0; i < Math.min(count || 1, ary.length); i++) {
                var obj = ary.shift();
                fn(obj);
            }
        };

        return function () {
            t = setInterval(function () {
                if (ary.length === 0) {
                    return clearInterval(t);
                }
                start();
            }, 200);
        };
    }

    var ary = [];
    for (var i = 1; i <= 1000; i++) {
        ary.push(i);

    }

    var renderFriendList = timeChunk(ary, function (n) {
        var div = document.createElement('div');
        div.innerHTML = n;
        document.body.appendChild(div);
    }, 8);

    renderFriendList();
```

******************************

### ** 参考 **
《JavaScript设计模式与开发实践》
