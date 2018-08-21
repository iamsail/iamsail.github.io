---
title: Observer(观察者)模式
date: 2017-08-12 16:29:00
categories: 设计模式
---

### ** 定义 **

一个或多个观察者对目标的状态感兴趣,它们通过将自己依附在目标对象上以便注册感兴趣的内容。目标状态发生改变并且观察者可能对这些改变感兴趣,就会发送一个通知消息,调用每个观察者的更新方法。

当观察者不再对目标状态感兴趣时,它们可以简单地将自己从中分离。

`Subject(目标)`
维护一系列的观察者,方便添加或删除观察者

`Observer(观察者)`
为那些在状态发生改变时需获得通知的对象提供一个更新接口

`ConcreteSubject(具体目标)`
状态发生改变时,向`Observer`发出通知,储存`ConcreteObserver`的状态

`ConcreteObserver(具体观察者)`
存储一个指向`ConcreteSubject`的引用,实现`Observer`的更新接口,以使自身状态与目标的状态保持一致

*************

### ** 实现 ** 

<span class="under0">以下是ES5和ES6的各自实现</span>

#### ** ES5 **
 
模拟一个目标可能拥有的一系列依赖Observer 
 
```javascript
function ObserverList () {
  this.observerList = [];
}

ObserverList.prototype.Add = function (obj) {
    console.log("666");
    return this.observerList.push(obj);
};

ObserverList.prototype.Empty = function () {
  this.observerList = [];
}

ObserverList.prototype.Count = function () {
  return this.observerList.length;
}

ObserverList.prototype.Get = function () {
  if(index > -1 && index < this.observerList.length){
    return this.observerList[index];
  }
}

ObserverList.prototype.Insert = function (obj, index) {
  var pointer = -1;

  if(index === 0){
    this.observerList.unshift(obj);
    pointer = index;
  } else if (index === this.observerList.length){
    this.observerList.push(obj);
    pointer = index;
  }
  return pointer;
}

ObserverList.prototype.IndexOf = function (obj, startIndex) {
  var i = startIndex, pointer = -1;

  while(i < this.observerList.length){
    if(this.observerList[i] === obj){
      pointer = i;
    }
    i++;
  }
  return pointer;
}

ObserverList.prototype.RemoveIndexAt = function (index) {
  if(index === 0){
    this.observerList.shift();
  } else if(index === this.observerList.length - 1){
    this.observerList.pop();
  }
}

function extend (obj, extension) {
  for(var key in obj){
    extension[key] = obj[key];
  }
}
```

模拟目标(Subject)和在观察者列表上添加、删除或通知观察者的能力

```javascript
function Subject () {
  this.observers = new ObserverList();
}

Subject.prototype.AddObserver = function (observer) {
    this.observers.Add(observer);
}

Subject.prototype.RemoveObserver = function (observer){
    this.observers.RemoveIndexAt(this.observers.IndexOf(observer,0));
}

Subject.prototype.Notify = function (context) {
    console.log("1111111111111111");

    var observerCount = this.observers.Count;
    for (var i = 0; i < observerCount; i++){
      this.observers.Get(I).Update(context);
    }
}

```
创建新的Observer

```javascript
function Observer() {
    this.Update = function () {
    }
}
```

<span class="under0">实例</span>

```HTML
<button id="addNewObserver">Add New Observer checkbox</button>
<input id="mainCheckbox" type="checkbox"/>
<div id="observersContainer"></div>
```


```javascript
    var controlCheckbox = document.getElementById("mainCheckbox"),
        addBtn = document.getElementById("addNewObserver"),
        container = document.getElementById("observersContainer");

    extend(new Subject(), controlCheckbox);

    controlCheckbox["onclick"] = new Function("controlCheckbox.Notify(controlCheckbox.checked)");

    addBtn["onclick"] = AddNewObserver;

    function AddNewObserver() {
        var check = document.createElement("input");
        check.type = "checkbox";

        extend(new Observer(), check);

        check.Update = function (value) {
            this.checked = value;
        };

        controlCheckbox.AddObserver(check);

        container.appendChild(check);
    }

```

#### ** ES6 **

```javascript
const person = observable({
  name: '张三',
  age: 20
});

function print() {
  console.log(`${person.name}, ${person.age}`)
}

observe(print);
person.name = '李四';
```
上面代码中，数据对象`person`是观察目标，函数`print`是观察者。一旦数据对象发生变化，`print`就会自动执行


下面，使用 `Proxy` 写一个观察者模式的最简单实现，即实现`observable`和`observe`这两个函数。思路是`observable`函数返回一个原始对象的 `Proxy` 代理，拦截赋值操作，触发充当观察者的各个函数。

```javascript
const queuedObservers = new Set();

const observe = fn => queuedObservers.add(fn);
const observable = obj => new Proxy(obj, {set});

function set(target, key, value, receiver) {
  const result = Reflect.set(target, key, value, receiver);
  queuedObservers.forEach(observer => observer());
  return result;
}
```

上面代码中，先定义了一个`Set`集合，所有观察者函数都放进这个集合。然后，`observable`函数返回原始对象的代理，拦截赋值操作。拦截函数`set`之中，会自动执行所有观察者。

****************

### ** 以下是18年8月21更新 **

#### ** 观察者模式实践 **

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>观察者模式</title>
</head>
<body>
<h1>观察者模式</h1>
<script>
    var salesOffices = {};
    salesOffices.clientList = []; //　缓存

    salesOffices.listen = function (key, fn) {
        if (!this.clientList[key]) {
            this.clientList[key] = [];
        }

        this.clientList[key].push(fn); //增加订阅者
    };

    salesOffices.trigger = function () {
        var key = Array.prototype.shift.call(arguments),
            fns = this.clientList[key];

        if (!fns || fns.length === 0) {
            return false;
        }

        for (var i = 0, fn; fn = fns[i++];) {
            fn.apply(this, arguments);
        }
    };

    // 小明订阅88平方米房子的消息
    salesOffices.listen('squareMeter88', function (price) {
        console.log('价格= ' + price);
    });

    // 小红订阅110平方米房子的消息
    salesOffices.listen('squareMeter110', function (price) {
        console.log('价格= ' + price);
    });

    salesOffices.trigger('squareMeter88', 88);
    salesOffices.trigger('squareMeter110', 110);
</script>
</body>
</html>
```
*****************

** 把发布--订阅功能提取出来,放在一个独立的对象 **

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>观察者模式</title>
</head>
<body>
<h1>观察者模式</h1>
<script>
    var event = {
        clientList: [],
        listen: function (key, fn) {
            if (!this.clientList[key]) {
                this.clientList[key] = [];
            }

            this.clientList[key].push(fn); //增加订阅者
        },
        trigger: function () {
            var key = Array.prototype.shift.call(arguments),
                fns = this.clientList[key];

            if (!fns || fns.length === 0) {
                return false;
            }

            for (var i = 0, fn; fn = fns[i++];) {
                fn.apply(this, arguments);
            }
        }
    };

    var installEvent = function (obj) {
      for (var i in event) {
          obj[i] = event[i];
      }
    };

    var salesOffices = {};
    installEvent(salesOffices); //　缓存

    // 小明订阅88平方米房子的消息
    salesOffices.listen('squareMeter88', function (price) {
        console.log('价格= ' + price);
    });

    // 小红订阅110平方米房子的消息
    salesOffices.listen('squareMeter110', function (price) {
        console.log('价格= ' + price);
    });

    salesOffices.trigger('squareMeter88', 88);
    salesOffices.trigger('squareMeter110', 110);
</script>
</body>
</html>
```



****************

### ** 参考 **

JavaScript设计模式
ECMAScript 6 入门

