---
title: Constructor(构造器)模式
date: 2017-07-29 10:00:00
categories: 设计模式
---
### ** 前言 **

之前零星的学了点设计模式,趁着假期,开始看《JavaScript 设计模式》系统的学习下,并写写博文做记录。

***************

### ** 分类 **

在《JavaScript 设计模式》一书中,讲了以下这三种类别的设计模式

#### ** 创建型设计模式 **

创建型设计模式专注于处理对象创建机制,以适合给定情况的方式来创建对象。

属于这个类别的模式包括:Constructor(构造器)、Factory(工厂)、Abstract(抽象)、Prototype(原型)、Singleton(单例)和Builder(生成器)。

#### ** 结构型设计模式 **

结构型模式与对象组合有关,通常可以用于找出在不同对象之间建立关系的简单方法。

属于这个类别的模式包括:Decorator(装饰者)、Facade(外观)、Flyweight(享元)、Adapter(适配器)和Proxy(代理)

#### ** 行为设计模式 **

行为设计模式专注于改善或简化系统中不同对象之间的通信

行为模式包括:Iterator(迭代器模式)、Mediator(中介者)、Observer(观察者)和Visitor(访问者)

**************
### ** Constructor(构造器) 模式 **

#### ** 基本Constructor(构造器) **

```JavaScript
function Car(model, year, miles) {
    this.model = model;
    this.year = year;
    this.miles = miles;

    this.toString = function()  {
        return this.model + " has done " + this.miles + " miles";
    };
}

let sail = new Car("sail",2017,6666);
let Sail = new Car("Sail",2017,9999);

console.log(sail.toString());
console.log(Sail.toString());

```
该版本存在一定的问题,它使得继承变得困难。另外,这种实现方式,toString()这样的函数是为每个使用Car构造器创建的新对象而分别重新定义的。

***************
#### ** 带原型的Constructor(构造器) **

```JavaScript
function Car(model, year, miles) {
    this.model = model;
    this.year = year;
    this.miles = miles;

}

Car.prototype.toString = function () {
    return this.model + " has done " + this.miles + " miles";
};

var sail = new Car("sail",2017,6666);
var Sail = new Car("Sail",2017,9999);

console.log(sail.toString());
console.log(Sail.toString());
```

通过这种方式,可以创建的多个Car对象,并访问相同的原型。

****************

<span class="under0">我用ES6重写了以上两段代码,却出现了一些问题。代码依次如下</span>

#### ** 基本Constructor(构造器) **
```JavaScript
function Car(model, year, miles) {
    this.model = model;
    this.year = year;
    this.miles = miles;

    this.toString = () => {
        return this.model + " has done " + this.miles + " miles";
    };
}

let sail = new Car("sail",2017,6666);
let Sail = new Car("Sail",2017,9999);

console.log(sail.toString());
console.log(Sail.toString());
```
#### ** 运行结果 **

```
sail has done 6666 miles
Sail has done 9999 miles
```
************

#### ** 带原型的Constructor(构造器) **

```JavaScript
function Car(model, year, miles) {
    this.model = model;
    this.year = year;
    this.miles = miles;
}

Car.prototype.toString = () => {
    return this.model + " has done " + this.miles + " miles";
};

let sail = new Car("sail",2017,6666);
let Sail = new Car("Sail",2017,9999);

console.log(sail.toString());
console.log(Sail.toString());

```
#### ** 运行结果 **

```
undefined has done undefined miles
undefined has done undefined miles
```

<span class="under0">前一段代码能够正常运行,而后一段代码 `this.model` 、`this.miles` 皆是 `undefined`</span>

这里就涉及到有关箭头函数的使用问题了。在我的博文[JS类数组转数组](http://www.sail.name/2017/05/15/Array-like-to-Array-in-JavaScript/)曾提到过。


#### ** 箭头函数有几个使用注意点 **

（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。

************

在基本Constructor(记作A)中的那段代码能够正常运行是因为

```javascript
function Car(model, year, miles) {
    this.model = model;
    this.year = year;
    this.miles = miles;
    this.toString = () => {
        return this.model + " has done " + this.miles + " miles";
    };
}
```

`toString`方法中的this是父级作用域的this,即函数Car的this.

<span class="under0"> ** 箭头函数本身是没有this,arguments的 ** </span> 

而在带原型的Constructor(记作B)中的这段代码undefined是因为

```javascript
function Car(model, year, miles) {
    this.model = model;
    this.year = year;
    this.miles = miles;
}

Car.prototype.toString = () => {
    return this.model + " has done " + this.miles + " miles";
};
```
<span class="under0">** 箭头函数中的this不是指向Car,而是指向了全局作用域。**</span>普通函数则没这个问题。

另一个容易犯的错误是使用箭头函数定义对象的方法
```javascript
let a = {
  foo: 1,
  bar: () => console.log(this.foo)
}

a.bar()  //undefined
```
以上代码中,箭头函数中的this并不是指向a这个对象。对象a并不能构成一个作用域,所以再往上到达全局作用域，this就指向全局作用域。如果我们使用普通函数的定义方法，输出结果就符合预期，这是因为a.bar()函数执行时作用域绑定到了a对象。

**************

### ** 参考 **

- 《JavaScript 设计模式》
- [少年，不要滥用箭头函数啊](https://cnodejs.org/topic/584a207a3ebad99b336b1ede)

****************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>


