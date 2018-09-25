---
title: 策略模式
date: 2018-09-11 18:40:00
categories: 设计模式
---

### ** Preface **

策略模式指的是定义一系列的算法,把它们一个个封装起来。将不变的部分和变化的部分隔开是每个设计模式的主题,策略模式也不例外,策略模式的目的就是将算法的使用与算法的实现分离开来。

一个基于策略模式的程序至少由两部分组成。第一个部分是一组策略类,策略类封装了具体的算法,并负责具体的计算过程。第二个部分是环境类Context,Context接受客户的请求,随后把请求委托给某一个策略类。要做到这点,说明Context中要维持对某个策略对象的引用

****************
### ** 策略模式实现 **
```javascript
var strategies = {
    "S": function (salary) {
        return salary * 4;
    },
    "A": function (salary) {
        return salary * 3;
    },
    "B": function (salary) {
        return salary * 2;
    }
}
var calculateBonus = function (level, salary) {
    return strategies[level](salary);
};
console.log(calculateBonus('S', 2000));
console.log(calculateBonus('A', 1000));
```
*****************
### ** 使用策略模式实现缓动动画 **

```javascript
var tween = {
    // 这4个参数的含义分别是动画已消耗的时间,小球原始位置,小球目标位置,动画持续的总时间
    // 返回的值则是动画元素应该处在的当前位置
    linear: function (t, b, c, d) {
        return c*t/d + b;
    },
    easeIn: function (t, b, c, d) {
        return c * (t /= d) * t + b;
    },
    strongEaseIn: function (t, b, c, d) {
        return c * (t /= d) * t * t * t * t + b;
    },
    strongEaseOut: function (t, b, c, d) {
        return c * ((t = t / d - 1) * t * t * t * t + 1) + b;
    },
    sineaseIn: function (t, b, c, d) {
        return c * (t /= d) * t * t + b;
    },
    sineaseOut: function (t, b, c, d) {
        return c * ((t = t / d - 1) * t * t + 1) + b;
    },
}

var Animate = function (dom) {
    this.dom = dom;     // 进行运动的dom结点
    this.startTime = 0; // 动画开始的时间
    this.startPos = 0;  // dom的初始位置
    this.endPos = 0;    // dom的目标位置
    this.propertyName = null; // dom节点需要被改变的css属性名
    this.easing = null;       // 缓动算法
    this.duration = null;     // 动画持续时间
}

Animate.prototype.start = function (propertyName, endPos, duration, easing) {
    this.startTime = +new Date; // 动画启动时间
    this.startPos = this.dom.getBoundingClientRect()[propertyName]; // dom结点初始位置
    this.propertyName = propertyName; // dom节点需要被改变的CSS属性名
    this.endPos = endPos; // dom节点目标位置
    this.duration = duration; // 动画持续事件
    this.easing = tween[easing]; // 缓动算法
    var self = this;
    var timeId = setInterval(function () {  // 启动定时器,开始执行动画
        if (self.step() === false) {        // 如果动画已结束,则清楚定时器
            clearInterval(timeId);
        }
    }, 19)
}


Animate.prototype.step = function () {
    var t = +new Date; // 取得当前时间
    // 如果当前时间大于动画开始时间加上动画持续时间之和,说明动画已经结束了,此时要修正小球位置
    if (t >= this.startTime + this.duration) {
        this.update(this.endPos);
        return false;
    }
    // pos为小球当前位置
    var pos = this.easing(t - this.startTime, this.startPos, this.endPos - this.startPos, this.duration);
    this.update(pos); // 更新小球的CSS属性
};


Animate.prototype.update = function (pos) {
    this.dom.style[this.propertyName] = pos + 'px';
}
var div = document.getElementById('div');
var animate = new Animate(div);
// animate.start('top', 1500, 500, 'strongEaseIn');
animate.start('top', 1500, 500, 'linear');
```

****************
### ** 参考 **
《JavaScript设计模式与开发实践》