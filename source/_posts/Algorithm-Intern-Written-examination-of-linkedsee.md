---
title: tow
date: 2018-06-24 21:04:30
tags: 笔试
password: 0Algorithm6,
---

### ** Preface **
灵犀联云算法实习生笔试

昨天中午收到了[灵犀联云](https://www.linkedsee.com/)hr的电话,聊了快十分钟。hr很专业也很nice.

还是蛮激动的,毕竟投了3天算法的简历,总算有一家有反馈的了。

有意思的是这家公司的创始团队全是从百度运维那边出来的,这家公司业务就是做智能运维的,今年还拿到了百度的投资。

电话结束过后,hr给我发了笔试邮件,今天上午做了。本文记录下。为了防止泄题,所以我加密了。

其实还是蛮想去的,不过我太菜了,应该是凉了。

*********************

### ** 第一题　**

> 返回第二大的元素,不可以调用sort

本题快排就可以解决

*********************

### ** 第二题　**

> 判断两颗二叉树是否相等(结构和值)

```regexp

```
*********************

### ** 第三题　**

> 非负整数，数字加和到只有一位数，打印值

```regexp

```
这题我是递归解决的,后面补下代码

*********************

### ** 第四题　**
> 两个人，石头，每次只能拿一到三块，我先拿，最后一个有石头拿的人为赢？两个人足够聪明，设计算法，根据石头数量，是否能赢

```regexp

```
*********************
### ** 第五题　**

>股票，每天只能交易一次，k天，有一个数组，股票每天的价格，交易前必须卖完？求最大利润

```regexp

```

*********************

### ** 秋招前端面试更新　**

关于算法的面经我都更新到了[图鸭信息科技算法实习生面试](http://www.sail.name/2018/06/26/algorithm-intern-interview-of-tucodec/),那前端就更新在这篇博客吧,所有的面经等我最终工作搞定后再解封。

这里我多说一句吧,算是对我自己的提醒,在最终工作敲定前,都不要松懈

********************

### ** 我看的面经 **

[腾讯前端一面凉经](https://www.nowcoder.com/discuss/91201?type=2&order=0&pos=9&page=1)
[昨天投今天面，令人窒息的腾讯前端一面(更新了) ](https://www.nowcoder.com/discuss/88698?type=2&order=0&pos=15&page=2)
[百度智能云前端面经 ](https://www.nowcoder.com/discuss/91112?type=2&order=0&pos=19&page=1)
[奇虎360 前端实习面经 ](https://www.nowcoder.com/discuss/91338?type=2&order=0&pos=67&page=1)
[阿里前端一面凉凉 ](https://www.nowcoder.com/discuss/91197?type=2&order=0&pos=86&page=1)
[更新了的腾讯IEG前端一面+二面 ](https://www.nowcoder.com/discuss/89155?type=2&order=0&pos=102&page=2)
[【有赞2019秋招前端内推面经】一面顺利通过 ](https://www.nowcoder.com/discuss/90535?type=2&order=0&pos=119&page=1)
[更新了的腾讯IEG前端一面+二面 ](https://www.nowcoder.com/discuss/89155?type=2&order=0&pos=102&page=2)
[腾讯前端一面 ](https://www.nowcoder.com/discuss/90243?type=2&order=0&pos=171&page=1)
[猿辅导前端面筋 ](https://www.nowcoder.com/discuss/93354?type=2&order=0&pos=52&page=1)
[前端的校招总结，结束秋招](https://www.nowcoder.com/discuss/51738?type=2&order=0&pos=108&page=1)
[有赞前端一面 ](https://www.nowcoder.com/discuss/93642?type=2&order=0&pos=130&page=1)
[有赞前端js面经一面 ](https://www.nowcoder.com/discuss/93681?type=2&order=0&pos=131&page=1)
[猿辅导前端一面 ](https://www.nowcoder.com/discuss/95432?type=0&order=0&pos=44&page=1)

********************
### ** 我从面经总结的问题 **
>let const区别 
[let 和 const 命令](http://es6.ruanyifeng.com/#docs/let)

>箭头函数和普通函数 
[箭头函数](http://es6.ruanyifeng.com/#docs/function#%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0)

>箭头函数可以当做构造函数吗
不可以

>箭头函数有没有prototype和constructor 
没有
[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

>JS中的this了解吗，this指向是执行时定义还是什么时候定义的，箭头函数的this指向呢 
[JavaScript 的 this 指向问题深度解析](https://segmentfault.com/a/1190000008400124)
[JS中this指向规则（简单易懂）](https://blog.csdn.net/runOnWay/article/details/78567900)
与我们常见的很多语言不同，JavaScript 函数中的 this 指向并不是在函数定义的时候确定的，而是在调用的时候确定的。换句话说，函数的调用方式决定了 this 指向。
JavaScript 中，普通的函数调用方式有三种：直接调用、方法调用和 new 调用。除此之外，还有一些特殊的调用方式，比如通过 bind() 将函数绑定到对象之后再进行调用、通过 call()、apply() 进行调用等。而 es6 引入了箭头函数之后，箭头函数调用时，其 this 指向又有所不同。下面就来分析这些情况下的 this 指向
箭头函数不会创建自己的this,它只会从自己的作用域链的上一层继承this

>cors和jsonp
[跨域请求之 JSONP 和 CORS](https://isudox.com/2016/09/24/cross-site-jsonp-and-cors/) 
[cors跨域（以及和jsonp的区别）](https://blog.csdn.net/qq_33562825/article/details/60780480)


>TCP UDP区别  为什么tcp是可靠传输 
[TCP和UDP的最完整的区别](https://blog.csdn.net/Li_Ning_/article/details/52117463)
[TCP和UDP之间的区别](http://blog.51cto.com/feinibuke/340272)
[面试题：TCP协议与UDP协议的区别](https://blog.csdn.net/qq_18425655/article/details/51955674)

>http头里有什么  http协议 http状态码
[前端阶段性总结之「理解HTTP协议」](https://godbasin.github.io/2017/05/20/front-end-notes-7-init-http/)
[关于 HTTP 协议，一篇就够了](https://juejin.im/entry/57ff5c5b0bd1d00058e5b2aa)
[《图解HTTP》读书笔记](https://sunshinevvv.coding.me/blog/2017/01/26/%E5%9B%BE%E8%A7%A3HTTP-%E8%AF%BB%E4%B9%A6%E7%AC%94%E8%AE%B0/)

>为什么dns要快，要用udp
[DNS使用的是TCP协议还是UDP协议](http://benbenxiongyuan.iteye.com/blog/1088085)
[DNS分别在什么情况下使用UDP和TCP](https://www.cnblogs.com/549294286/p/5172435.html)

>http https区别 https具体解决了哪些问题？举个栗子？ 
[详细解析 HTTP 与 HTTPS 的区别](https://juejin.im/entry/58d7635e5c497d0057fae036)
[http 和 https 有何区别？如何灵活使用？](https://www.zhihu.com/question/19577317)

>GET和POST请求的区别
[浅谈HTTP中Get与Post的区别](https://www.cnblogs.com/hyddd/archive/2009/03/31/1426026.html)
[get和post区别？](https://www.zhihu.com/question/28586791)
[HTTP协议中GET和POST方法的区别](https://sunshinevvv.coding.me/blog/2017/02/09/HttpGETv.s.POST/)
[HTTP幂等性及GET、POST、PUT、DELETE的区别](https://blog.csdn.net/zjkC050818/article/details/78799386)
[DNS正向解析分为递归和迭代。 通常是用递归，还是迭代呢？](https://www.zhihu.com/question/53882349)

>三次握手,四次挥手
[从输入url到页面展示到底发生了什么](https://mp.weixin.qq.com/s/7eY3XIhLXeCMqBYIQh6WwA)


[雅虎网站页面性能优化的34条黄金守则](http://www.cnblogs.com/li0803/archive/2009/09/20/1570581.html)
[reflow（回流）和repaint（重绘）及其优化](https://blog.csdn.net/ClaireKe/article/details/51375622)
[前端精选文摘：BFC 神奇背后的原理](http://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html)


>如何判断js数据类型 
[如何正确判断js数据类型](https://segmentfault.com/q/1010000000464600)
[javascript判断数据类型](https://segmentfault.com/a/1190000005174193)
Object.prototype.toString()
[判断JS数据类型的四种方法](https://www.cnblogs.com/onepixel/p/5126046.html)

>vue相比jQ?
vue v-dom
vue 双向数据绑定

>[vuex](https://vuex.vuejs.org/zh/)
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化
state，驱动应用的数据源；
view，以声明方式将 state 映射到视图；
actions，响应在 view 上的用户输入导致的状态变化。


>对vuex和[vue-router](https://router.vuejs.org/zh/)了解吗？那么请说一下vuex的store分为哪几部分？分别代表什么意思
vue的生命周期
[生命周期图示](https://cn.vuejs.org/v2/guide/instance.html#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE%E7%A4%BA)
[Vue2.0 探索之路——生命周期和钩子函数的一些理解](https://segmentfault.com/a/1190000008010666)
虚拟dom具体怎么对比的，为什么它性能好
怎么创建动态路由？
[深入 Vue2.x 的虚拟 DOM diff 原理](https://cloud.tencent.com/developer/article/1006029)
[解析vue2.0的diff算法](https://github.com/aooy/blog/issues/2)
[Vue原理解析之Virtual Dom](https://segmentfault.com/a/1190000008291645)
[剖析Vue实现原理 - 如何实现双向绑定mvvm](https://github.com/DMQ/mvvm)
[VirtualDOM与diff(Vue实现)](https://juejin.im/post/59bfbd736fb9a00a52065ec7)
[如何理解虚拟DOM?](https://www.zhihu.com/question/29504639)
[深度剖析：如何实现一个 Virtual DOM 算法](https://github.com/livoras/blog/issues/13)
[界面之下：还原真实的MV*模式 ](https://github.com/livoras/blog/issues/11)
[Vue2.0 源码阅读：模板渲染](http://zhouweicsu.github.io/blog/2017/04/21/vue-2-0-template/)
[Edit distance](https://en.wikipedia.org/wiki/Edit_distance)
[最短编辑距离算法（字符串比较）](https://blog.csdn.net/fouy_yun/article/details/46423753)
[最小编辑距离问题：递归与动态规划 ](https://github.com/youngwind/blog/issues/106)
[算法题解：最小编辑距离（动态规划算法）](https://segmentfault.com/a/1190000012769863)


>怎么判断一个对象为空对象呢，回答了JSON方法，还有吗 
[js如何判断一个对象{}是否为空对象，没有任何属性](https://blog.csdn.net/testcs_dn/article/details/40431835)
[js 判断一个 object 对象是否为空](https://blog.csdn.net/FungLeo/article/details/78113661)
1.最常见的思路，for...in... 遍历属性，为真则为“非空数组”；否则为“空数组”
2.通过 JSON 自带的 stringify() 方法来判断:
3.Object.keys() ES5 引入了Object.keys方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。

>用过cookie吗，怎么修改cookie呢，除了JS方法还有什么方法呢 
cookie都有哪些参数呢，cookie的本质是什么，如果让你封装一个cookie方法你怎么实现
[聊一聊 cookie](https://segmentfault.com/a/1190000004556040)
[https://segmentfault.com/a/1190000004556040](https://segmentfault.com/a/1190000004743454)
[如何修改cookie？](https://segmentfault.com/q/1010000009225824)
[xhr.withCredentials与 CORS 什么关系](https://segmentfault.com/a/1190000004322487#articleHeader13)
[php设置cookie的三种方法比较](https://newsn.net/say/php-cookie.html)

>禁止了浏览器cookie，session 还可以用吗
[禁止了浏览器 cookie，session 还可以用吗？](https://www.zhihu.com/question/35307626)
[如果cookie禁用了，session还能用吗，为什么](https://segmentfault.com/q/1010000004194930)

>cookie和session区别
[COOKIE和SESSION有什么区别？](https://www.zhihu.com/question/19786827)
[Cookie 与 Session 的区别](https://juejin.im/entry/5766c29d6be3ff006a31b84e)

>知道POST方法吗，POST方法如何设置传输的数据的格式 
[理解HTTP之Content-Type](http://homeway.me/2015/07/19/understand-http-about-content-type/)
[四种常见的 POST 提交数据方式](https://imququ.com/post/four-ways-to-post-data-in-http.html)
[HTTP请求GET/POST与参数小结](https://alanli7991.github.io/2016/10/26/HTTP%E8%AF%B7%E6%B1%82GETPOST%E4%B8%8E%E5%8F%82%E6%95%B0%E5%B0%8F%E7%BB%93/)
[关于post与ajax post的数据类型](https://www.jianshu.com/p/39eb83f22285)
application/x-www-form-urlencoded
multipart/form-data
application/json
text/xml
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded'); // 或
xhr.setRequestHeader('Content-Type', 'application/json');


>前端向后端传输数据的方法有哪些，ajax?还有呢，fetch？还有呢，JSONP？还有吗，表单传输？ 
[前端向后台服务器端发送请求并且传送数据的方式](https://blog.csdn.net/liufunan/article/details/50715053)
[前端 ，后端 关于数据交互的问题?](https://www.zhihu.com/question/26532621)

>详细说一下表单是怎么传输数据的 
[发送表单数据](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)

>CSS实现一个旋转的动画如何实现，animation和transition有什么区别 
[CSS animation 与 CSS transition 有何区别？](https://www.zhihu.com/question/19749045)
[CSS3 Transition 和Animation区别及比较](https://blog.csdn.net/cddcj/article/details/53582334)
[打字机动画](http://www.sail.name/2017/08/03/typing-animation/)
[transform失效了?](http://www.sail.name/2017/05/06/why-the-transform-cannot-work/)
[旋转的立方体](http://www.sail.name/2017/02/16/rotary-cube/)
[再谈旋转的立方体](http://www.sail.name/2017/07/28/talk-rotary-cube-again/)


>js 浅拷贝，深拷贝
[JavaScript中的浅拷贝和深拷贝](https://segmentfault.com/a/1190000008637489)
[javascript中的深拷贝和浅拷贝？](https://www.zhihu.com/question/23031215)


>事件代理
[JavaScript 事件委托详解](https://zhuanlan.zhihu.com/p/26536815?refer=qiutc)

如何实现图片的懒加载呢，如何才能监听到图片进入屏幕，利用了哪些属性

>回调地狱知道吗，怎么解决呢 
[【翻译】关于回调地狱](https://segmentfault.com/a/1190000009644973)
[回调地狱Callback Hell](https://www.jianshu.com/p/d31d2ecb4162)

>git merge 和git merge --no--ff有什么区别 
[git merge 跟 git merge -no-ff](https://blog.csdn.net/pzhtpf/article/details/52151320)


异步的解决方案有哪些呢 

>Promise怎么执行一个串行的请求，并行呢？ 
怎么自己实现一个promise （懵逼二连）
[大白话讲解Promise（一）](https://www.cnblogs.com/lvdabao/p/es6-promise-1.html)

>有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。
Promise也有一些缺点。首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。
其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。
第三，当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。



下面是一个用Promise对象实现的 Ajax 操作的例子。
```javascript
const getJSON = function(url) {
  const promise = new Promise(function(resolve, reject){
    const handler = function() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
    const client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

  });

  return promise;
};

getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
```

Ajax 是典型的异步操作，通过 Generator 函数部署 Ajax 操作，可以用同步的方式表达。

```javascript
function* main() {
  var result = yield request("http://some.url");
  var resp = JSON.parse(result);
    console.log(resp.value);
}

function request(url) {
  makeAjaxCall(url, function(response){
    it.next(response);
  });
}

var it = main();
it.next();
```

async/await怎么实现上述请求呢，generator呢 
generator的自动化执行怎么实现的呢，co实现generator自执行的条件 


>模块化 amd cmd mudule
[理解CommonJS、AMD、CMD三种规范](https://zhuanlan.zhihu.com/p/26625636)
[JS - CommonJS、ES2015、AMD、CMD模块规范对比与介绍（附样例）](http://www.hangge.com/blog/cache/detail_1686.html)

>prototype 属性和__proto__属性
[js中__proto__和prototype的区别和关系](https://www.zhihu.com/question/34183746)
[从__proto__和prototype来深入理解JS对象和原型链](https://github.com/creeperyang/blog/issues/9)
1.对象有属性__proto__,指向该对象的构造函数的原型对象。
2.方法除了有属性__proto__,还有属性prototype，prototype指向该方法的原型对象。

>大数加法 
[C++ 大数加法](https://blog.csdn.net/OrthocenterChocolate/article/details/36664901)

>浏览器最小显示的字体大小 如果想要显示更小怎么办  
[chrome浏览器最小字体大小限制的解决方案](https://blog.csdn.net/shidaping/article/details/52635595)
[谷歌浏览器默认最小字体的解决方法以及各浏览器对字体大小的支持](https://blog.csdn.net/CCG_T/article/details/77018446)


>进程和线程的区别
[腾讯面试题04.进程和线程的区别？](https://blog.csdn.net/mxsgoden/article/details/8821936)
[进程和线程的区别](https://www.cnblogs.com/lmule/archive/2010/08/18/1802774.html)

>各种排序算法的时间复杂度 
[常用排序算法稳定性、时间复杂度分析（转，有改动）](https://www.cnblogs.com/nannanITeye/archive/2013/04/11/3013737.html)
[各种排序算法比较(2):时间复杂度,空间复杂度](https://blog.csdn.net/weiwenhp/article/details/8622728)
[常用几种排序算法的时间复杂度和空间复杂度](https://blog.csdn.net/yhd0916/article/details/48207167)


堆和栈，为什么有的放堆有的放栈 
mvc是什么，mvvm是什么，react是哪种 

字符串匹配算法(kmp?)


********************

### ** 老虎证券　**

#### ** 一面　**

老虎证券是8月6号下午面的,从1点56面到接近3点,几乎一个小时吧。3点10收到了hr的电话,说面试官对我特别满意。接下来就是终面了,终面必须现场面,我去北京或者他们安排人过来。希望能够拿下第一个offer。

>1.自我介绍

>盒子模型　　具体怎么设置的　查下

`content-box`
默认值，标准盒子模型。 width 与 height 只包括内容的宽和高， 不包括边框（border），内边距（padding），外边距（margin）。注意: 内边距, 边框 & 外边距 都在这个盒子的外部。 比如. 如果 .box {width: 350px}; 而且 {border: 10px solid black;} 那么在浏览器中的渲染的实际宽度将是370px;
尺寸计算公式：width = 内容的宽度，height = 内容的高度。宽度和高度都不包含内容的边框（border）和内边距（padding）。

`border-box`
width 和 height 属性包括内容，内边距和边框，但不包括外边距。这是当文档处于 Quirks模式 时Internet Explorer使用的盒模型。注意，填充和边框将在盒子内 , 例如, .box {width: 350px; border: 10px solid black;} 导致在浏览器中呈现的宽度为350px的盒子。内容框不能为负，并且被分配到0，使得不可能使用border-box使元素消失

>flex

[Flex基础](http://www.sail.name/2017/07/09/the-base-of-flex/)
[flex垂直居中](http://www.sail.name/2017/07/22/vertical-center-by-flex/)

>position　　sticky

[position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)

>闭包

>js GC机制

>cookie localstorage sessionstorage
[cookie、 sessionStorage 、localStorage之间的区别和使用](http://www.cnblogs.com/caiyezi/p/5619506.html)

>cookie安全问题,加密篡改啥的
待更新

>对数据可视化的了解

>2.反转字符串　　具体了解下有哪些方法

```javascript
function reverse_string(str) {
    let temp = [];
    for(let i = 0;i < str.length; i++) {
       temp.push(str[i]); 
    }
    
    let final_str = [];
    
     for(let i = temp.length;i >=0 ; i--) {
       final_str.push(temp.pop()); 
    }
    
    return string(final_str);
}
```

这里第一次写的时候我忘记了对返回值要做个处理string(),不然返回的是字符串


> 如何把数组转为字符串
  join方法

>3.数组哪些方法是会改变数组本身的
    
[js数组方法 改变原数组和不改变原数组的方法整理](https://blog.csdn.net/love07070707/article/details/79888566)
[js中那些方法不改变原来的数组对象](https://blog.csdn.net/liangklfang/article/details/49300417)
[细说JS数组](https://segmentfault.com/a/1190000008211717)

> 还问题了webpack
　我应该了解一下了,一些常用的loader,以及当初用到的一些性能优化的插件
    
    
>es6 常用的有哪些
    深入下异步和class部分

>4.vue的虚拟dom算法
    对vue的原理部分,和全家桶这两天要了解下
    待更新

>对职业的发展

>对code review怎么看
    
>实习项目有什么特别难忘的bug之类的吗

>有什么想问的


********************

### ** 今日头条(8.8 下午两点半视频面试) **

这次头条的面试是深圳那边hr在牛客网上看到我的简历,然后安排的。头条的内推我还没搞,因为头条这个持续时间比较长。面了五十多分钟,接近一个小时。

大概能想起来这些问题,应该遗漏了部分

自我介绍

然后开始做题了,有几道js的代码题吧,都需要自己写代码,算是对知识的综合检验,就不写出来了

> 3道js题，题目懒得写了，也难以复现

> setInterval　clearInterval
[window.setInterval](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setInterval)
[window.setTimeout](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout)

> web动画

> JS动画

> repaint,reflow

> 动画硬件加速,原理

> http-options
[HTTP的请求方法OPTIONS - CSDN博客](https://blog.csdn.net/leikezhu1981/article/details/7402272)
[关于 HTTP OPTIONS](https://www.kilerd.me/archives/47)

> css　实现4比3,不固定宽度高度实现　

> 如何判断js加载完成　动态创建scirpt标签,插入页面　onload
[怎样判断页面内容全部加载？](https://segmentfault.com/q/1010000003103762)
[怎样判断js脚本是否加载完，并在加载完后进行操作](https://blog.csdn.net/xiaobing_hope/article/details/78318471)

```javascript
function loadJsAsync(url){
    var body = document.getElementsByTagName('body')[0];
    var jsNode = document.createElement('script');

    jsNode.setAttribute('type', 'text/javascript');
    jsNode.setAttribute('src', url);
    body.appendChild(jsNode);

    if (jsNode.onload) {
        jsNode.onload = function() {
            // do something
        }
    } else {
        // ie6, ie7不支持onload的情况
        jsNode.onreadystatechange = function() {
            if(jsNode.readyState == 'loaded' || jsNode.readyState == 'complete') {
                // 异步js加载完毕
                // do something执行操作
            }
        }
    }
}
```

> post请求有哪些类型
application/x-www-form-urlencoded
multipart/form-data
application/json
text/xml
xhr.setRequestHeader(‘Content-Type’, ‘application/x-www-form-urlencoded’); // 或
xhr.setRequestHeader(‘Content-Type’, ‘application/json’);
....

> post 请求头 application/x-www-form-urlencoded multipart/form-data 请求头中参数有什么区别

> 一亿条数据,找出第1000条大的数据

> 双向绑定的实现，抛开框架,自己如何实现

> 跨域

> http1.0 http1.1 http2.0
[HTTP1.0、HTTP1.1 和 HTTP2.0 的区别](https://juejin.im/entry/5981c5df518825359a2b9476)
[HTTP/2.0 相比1.0有哪些重大改进？](https://www.zhihu.com/question/34074946)
[HTTP1.0 、HTTP 1.1 、HTTP 2.0的区别摘要](https://segmentfault.com/a/1190000008686770)

> 有什么想问的

******************************

### ** 有赞(8.13 下午 40分钟+60分钟视频面试) **

> 跨域
图像ping
jsonp可以post吗,为什么
[详解跨域请求的两种方式，支持post请求](http://www.01happy.com/two-ways-of-cross-domain-request/)
[jsonp为什么不支持post请求？](https://www.zhihu.com/question/28890257)
jsonp的callback可以写在全局还是可以写在模块里,写在模块里可以吗
除了script还有什么也可以吗　img

> a.bom b.com
a.com 向b.com请求　跨域前会先发其他请求吗,还是直接发送请求,然后被告诉不能跨域or?
预检请求（option）:在 CORS 中，可以使用 OPTIONS 方法发起一个预检请求(一般都是浏览检测到请求跨域时，会自动发起)，以检测实际请求是否可以被服务器所接受。预检请求报文中的 Access-Control-Request-Method 首部字段告知服务器实际请求所使用的 HTTP 方法；Access-Control-Request-Headers 首部字段告知服务器实际请求所携带的自定义首部字段。服务器基于从预检请求获得的信息来判断，是否接受接下来的实际请求。
[cors跨域之简单请求与预检请求（发送请求头带令牌token）](https://segmentfault.com/a/1190000009971254)
Cross-Origin Resource Sharing (CORS)
Access-Control-Allow-Methods 


> tcp协议和http协议主要是做什么
[彻底搞懂HTTP协议](http://www.akathink.com/2016/07/28/%E5%BD%BB%E5%BA%95%E6%90%9E%E6%87%82HTTP%E5%8D%8F%E8%AE%AE/)
[HTTP,HTTP协议的作用是什么?](http://www.elecfans.com/baike/tongxingjishu/chungshuwang/20100322201699.html)
js基础类型
array是类型吗
function是类型吗
如何判断类型
如何查找对象属性 for in   object.key   getownpropery
call ,apply,bind

>浏览器输入一个url
三次握手最后一次握手可以发数据吗
[三次握手的第三次握手发送ACK能携带数据吗？如何携带？怎样体现的呢](https://www.zhihu.com/question/66407996)


>linux　查找3000 端口 ps  -aux | grep
linux chmod 权限分配　
777
[chmod命令](http://man.linuxde.net/chmod)

>盒子模型
如何指定盒子模型 box-sizing
    box-sizing: content-box;
    box-sizing: border-box;
backgrpund会应用到哪些部分
[background---背景颜色和背景图片填充的范围](https://blog.csdn.net/qq_35809245/article/details/53638986?locationNum=5&fps=1)
填充 :content+padding+ border

>position




>这道题要看看有没有更高效的做法,两次for循环了,以及xxx有没有替代方案
[JS两个数组比较,删除重复值的巧妙方法(推荐)  ](https://www.teakki.com/p/57dfb1add3a7507f975e7038)
[JS中实现字符串和数组的相互转化](https://blog.csdn.net/erlian1992/article/details/50561452)



```javascript
/**
 * 从两个数组中找出重复的元素，连连看
 * 
 * @param {array} arr1 数组1
 * @param {array} arr2 数组2
 * @returns {array} 重复的数组
 * @example 
 * findCommon([ 1, 2, 1, 2], [1, 5, 2, 3])
 * // [1, 2]
 */

function findCommon(arr1, arr2, is) {
　　 let result = [];
    for (let i = 0; i < arr1.length; i++) {
        let is_go = true;
        for (let j = 0; j < arr2.length && is_go; j++) {
             if (arr1[i] === arr2[j] && arr1[i]  !== 'xxx') {
                //  console.log(arr1[i]);
                 is_go = false;
                 result.push(arr1[i]);
                 arr1[i] = 'xxx'; 
                 arr2[j] = 'xxx';
             }    
        }  
        // console.log(arr1, arr2);
    }
    // console.log(result);
    // let temp = new Set(result);
    // console.log(temp);

    result = Array.from(new Set(result));
    return result;
}

const res = findCommon([ { a: 1 }, 2, 'xxx', [2]], [{ a: 1 }, 5, 2, 3]);
// [1, 2]
console.log(res)
```


>[js 驼峰命名和下划线互换](https://blog.csdn.net/luzhongk/article/details/78918489)
[js驼峰命名和下划线转换](https://blog.csdn.net/zjw0742/article/details/78567291)
[String.prototype.replace()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)
[javaScript中String.replace()的第二个参数为函数时的用法介绍](https://blog.csdn.net/LinBilin_/article/details/57094602)

```javascript
// 下划线转换驼峰
function toHump(name) {
    return name.replace(/\_(\w)/g, function(all, letter){
        return letter.toUpperCase();
    });
}

// 驼峰转换下划线
function toLine(name) {
  return name.replace(/([A-Z])/g,"_$1").toLowerCase();
}
```

>[js 判断一个 object 对象是否为空](https://blog.csdn.net/FungLeo/article/details/78113661)
1.最常见的思路，for...in... 遍历属性，为真则为“非空数组”；否则为“空数组”
2.通过 JSON 自带的 stringify() 方法来判断:
3.ES6 新增的方法 Object.keys():
Object.keys() 方法会返回一个由一个给定对象的自身可枚举属性组成的数组。

*********************



```javascript
/**
 * 将一个对象的所有key从下划线改为驼峰
 * 
 * @param {object} value 待处理对象
 * @returns {object} 处理后的对象
 * @example 
 * mapKeysToCamelCase({ yz_key: { yz_a: { yz_b: 2 } } })
 * // { yzKey: 1 }
 */

 function isObjectNUll () {

 } 

 function mapKeysToCamelCase(value) {
     if (typeof value !== 'object') {
         throw "这不是一个对象"
     }

    //  if (isObjectNUll()) {
    //      return;
    //  }

        //  console.log(Object.keys(value));
     let keys =  Object.keys(value)
     keys.forEach((key_val)=> {
         let temp = key_val.split('_');
         let result = null;

         if (temp.length > 0) {
            temp.forEach((val, index) => {
                let temp_first;
                let temp_str;

                if (index === 0) {
                    temp_first = null;
                    temp_str = null;
                    result = val;
                }

                if(index > 0) {
                   temp_first = val[0].toUpperCase();
                   temp_str = `${temp_first}${val.substr(1)}`;
                   result += `${temp_str}`
                } 
            })
         } 
        console.log(result);
     })
 }

 let test = { yz_key: 1, xz_key: 2 };

 mapKeysToCamelCase (test);
```

*************************************

### ** 百度智能云事业部提前批前端面试 **

之前陈林给我内推了百度,不过我投的是机器学习,至今没收到面试邀请,投了大概十天了吧。

昨天去丁香园面试,去丁香园面试的路上,收到了百度大商业的hr,也是提前批,约了明天上午十一点面试。今天去物流园给丁香园寄报销车票的时候收到了智能云的面试,下午面了一面。

#### **  一面(8.16) **
一面面了70分钟,先是面试,然后写代码,又是`collabedit.com`。

面试问的问题太多了,大概记录下

> 自我介绍

> 然后问了我一些个人相关信息,就业意向,手上的offer之类的

> 然后聊了项目,先是聊得实习项目

> 有用过vue和echarts吗

> 然后开始聊了我的智能对话系统项目,面试官对这个项目很感兴趣啊,聊了很久

css部分

> 布局。页面有一个弹框,想要垂直居中怎么做

> 盒子模型

> BFC

> 响应式布局

> js数据类型,存储方式的不同

> 继承

> webpack特点,使用场景,原理
[Webpack 常用配置总结](https://toutiao.io/posts/fiq8wd/preview)
[webpack Loader的使用教程及常用的loader[入门篇]](https://github.com/lengziyu/learn-webpack/issues/2)
[webpack原理与实战](http://imweb.io/topic/59324940b9b65af940bf58ae)
[webpack 打包JS 的运行原理](https://zhuanlan.zhihu.com/p/32093510)
[细说 webpack 之流程篇](http://taobaofed.org/blog/2016/09/09/webpack-flow/)
[Webpack模块化原理简析](https://segmentfault.com/a/1190000010409465)

> 跨域,cors具体字段怎么设置



>前端安全csrf,xss
[XSS 和 CSRF 攻击的一些非常规防御方法](https://www.imooc.com/article/18069)
事实上现代浏览器为我们带来了一个全新的安全策略，叫作内容安全策略，Content Security Policy，简称CSP。CSP的思路跟转义不一样，它的着手点是，如果一段代码变成了程序，我们是否应该运行它。或者更准确一点说，它实际上是定义页面上哪一些内容是可被信任的，哪一些内容是不被信任的。
[Content-Security-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy__by_cnvoid)
[浅谈CSRF攻击方式](http://www.cnblogs.com/hyddd/archive/2009/04/09/1432744.html)
[CSRF 攻击的应对之道](https://www.ibm.com/developerworks/cn/web/1102_niugang_csrf/index.html)
[程序猿必读-防范CSRF跨站请求伪造](https://segmentfault.com/a/1190000008505616)
[XSS攻击及防御](https://blog.csdn.net/ghsau/article/details/17027893)
[web安全测试之XSS](http://www.cnblogs.com/TankXiao/archive/2012/03/21/2337194.html#urlencode)
XSS 漏洞修复
原则：　不相信客户输入的数据
注意:  攻击代码不一定在<script></script>中
将重要的cookie标记为http only,   这样的话Javascript 中的document.cookie语句就不能获取到cookie了.
只允许用户输入我们期望的数据。 例如：　年龄的textbox中，只允许用户输入数字。 而数字之外的字符都过滤掉。
对数据进行Html Encode 处理
过滤或移除特殊的Html标签， 例如:` <script>, <iframe> ,  &lt; for <, &gt; for >, &quot for`
过滤JavaScript 事件的标签


> 模块化,这里问了很多问题,也是我的漏洞
commonjs和cmd的区别
[Javascript模块化编程（二）：AMD规范](http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html)
[Javascript模块化编程（三）：require.js的用法](http://www.ruanyifeng.com/blog/2012/11/require_js.html)
[前端模块化：CommonJS,AMD,CMD,ES6](https://juejin.im/post/5aaa37c8f265da23945f365c)
[CommonJS规范](http://javascript.ruanyifeng.com/nodejs/module.html)
[Module 的语法](http://es6.ruanyifeng.com/#docs/module)
[Module 的加载实现](http://es6.ruanyifeng.com/#docs/module-loader)
CommonJS模块的加载机制是，输入的是被输出的值的拷贝。也就是说，一旦输出一个值，模块内部的变化就影响不到这个值。
CommonJS模块的特点如下。
所有代码都运行在模块作用域，不会污染全局作用域。
模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。
模块加载的顺序，按照其在代码中出现的顺序。

>ES6 模块与 CommonJS 模块的差异
 讨论 Node 加载 ES6 模块之前，必须了解 ES6 模块与 CommonJS 模块完全不同。
 它们有两个重大差异。
 CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
 CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
 第二个差异是因为 CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。


> https的原理 
[https原理：证书传递、验证和数据加密、解密过程解析](https://blog.csdn.net/clh604/article/details/22179907)
[HTTPS的工作原理](https://www.cnblogs.com/ttltry-air/archive/2012/08/20/2647898.html)
[白话解释 对称加密算法 VS 非对称加密算法](https://segmentfault.com/a/1190000004461428)
[白话解释 电子签名，电子证书，根证书，HTTPS，PKI 到底是什么](https://segmentfault.com/a/1190000012466003)
[白话解释 OSI模型，TLS/SSL 及 HTTPS](https://segmentfault.com/a/1190000004467714)
[HTTP是一个无状态的协议。这句话里的无状态是什么意思？](https://www.zhihu.com/question/23202402)
[主题:请问https是有状态协议还是无状态协议啊](http://m.newsmth.net/article/NetPRG/34850)



> 算法题,一个数组,有重复的元素,找出重复次数最多的元素,以及下表

```javascript
function find_max_ele(arr) {
    if (!Object.isArray(arr) && arr.length === 0) {
        return
    }
    
    let tempObj = {};
    let indexArr = [];
    let max = 0;   
    arr.forEach((val, index)=> {
        if (!tempObj[val]) {
            tempObj[val] = 1;
        } else {
            tempObj[val]++;
        }
    })
    
    for (ele in tempObj) {
        if(max < tempObj[ele]) {
            max = tempObj[ele];
        }
    }
    
    for(let i = 0; i < arr.length; i++) {
        if(arr[i] === max) {
            indexArr.push(i);
        }
    } 
    return max,indexArr;
}


function find_max_ele(arr) {
   if (!Object.isArray(arr) && arr.length === 0) {
        return
   }
   
   let tempArr = [];
   tempArr.fill(0);
   for (let i = 0; i < arr.length; i++) {
       tempArr[arr[i]]++;
   }
   
   for () {}
}

```

#### ** 二面(8.16) **

##### **　这是面经看的整理的　**

[算法系列—— 输出所有的笛卡尔积组合](https://blog.csdn.net/ylyg050518/article/details/78787432)
[百度面试的一道题-笛卡尔积？](https://www.zhihu.com/question/28867645)
[每天一道算法题](https://hiblacker.github.io/stydy-note/day-day-up.html)
[c++求若干个集合的笛卡尔积](https://blog.csdn.net/pangjiuzala/article/details/52982521)

写一个方法，求任意长度数组的笛卡尔积。例如

`cartesian([[1,2],['a','b']]) = [[1,'a'],[1,'b'],[2,'a'],[2,'b']]`

```javascript
function cartesion(...arys) {
    if (arys.length == 0) return []
    if (arys.length == 1) return arys
    return arys.reduce((prev, item) => {
        let t = []
        for (let i of prev) {
            for (let j of item) {
                t.push(Array.isArray(i) ? [...i, j] : [i, j])
            }
        }
        return t
    })
}
console.log(cartesion([1, 2, 3], ['a', 'b'], ['x', 'y']))
```

##### **　正式二面内容　**


自我介绍
聊项目，聊了好久好久，聊我遇到的难点
学校的项目,也聊了很久
问题的话
主要有浏览器缓存
cookie session localstorage

>然后就是经典问题,输入一个url 23333333333,大概就是这么多吧
这里服务端返回资源后,是先解析dom树(html),html中有link,script标签,再去请求新的资源

然后邮件发了一道算法题,半个小时做完
[一天内时针和分针重叠的次数](https://blog.csdn.net/liurenyou/article/details/78445009)
[钟表的时针和分针一天之内会重合多少次](https://www.nowcoder.com/questionTerminal/9c857e6ba7a7409daea914e837094d60)
[一天时间内，时针与分针会重合几次？](https://blog.csdn.net/Zidane_2014/article/details/45081531)
[代码中简单实现四舍五入（加上0.5取整）适用于所有语言](https://blog.csdn.net/longshenlmj/article/details/17020911)
[C语言，用0.5进行四舍五入](https://zhidao.baidu.com/question/1180293093053491299.html)

```c++
#include <iostream>
using namespace std;

// 系统ubuntu16
// 开发工具Clion

int main() {
    int one_catch_time_by_minute = 30;

    for(int hour = 0; hour < 11; hour++)
    {
        // 时针的速度 360度 / (12 * 60)分 = 0.5度/分
        // 分针的速度 360度/ 60分 = 6度/分
        // 且分针跑得比时针块
        int minute = (hour * one_catch_time_by_minute) / (6-0.5) + 0.5;
        cout<< hour << ":" << minute <<endl;
        cout<< hour + 12 << ":" << minute <<endl;
    }

    // 程序打印结果为
    // 0:0
    // 12:0
    // 1:5
    // 13:5
    // 2:11
    // 14:11
    // 3:16
    // 15:16
    // 4:22
    // 16:22
    // 5:27
    // 17:27
    // 6:33
    // 18:33
    // 7:38
    // 19:38
    // 8:44
    // 20:44
    // 9:49
    // 21:49
    // 10:55
    // 22:55
    return 0;
}
```


*************************************
### ** 百度大商业提前批前端面试 **

下周一上午一面,还面试途中网易广州给我打电话了,没接到gg,希望还能给打过来

#### ** 一面 **

>清楚浮动bfc  position absolute?
[css清除浮动float的七种常用方法总结和兼容性处理](https://blog.csdn.net/promiseCao/article/details/52771856)

>三栏布局
calc
flex
[CSS_Demo](https://github.com/iamsail/CSS_Demo)
[双飞翼布局](https://www.sail.name/CSS_Demo/flying-wing-layout.html)
[圣杯布局](https://www.sail.name/CSS_Demo/grail-layout.html)

>0.1+0.2 0.29999999 0.30000001 底层原理　js 和 c++ 会出现　　java和php会出现吗 会
IEEE 754 Floating-point　　　　　　　　　　　　　
[从0.1+0.2=0.30000000000000004再看JS中的Number类型](https://juejin.im/post/5a6fce10f265da3e261c3c71)
[JS魔法堂：彻底理解0.1 + 0.2 === 0.30000000000000004的背后](https://www.cnblogs.com/fsjohnhuang/p/5115672.html)
[0.30000000000000004.com](http://0.30000000000000004.com/)

>tf-idf　项目相关

>原型链的理解

>高阶函数

>函数节流

>websocket的一些参数
>websocket传数据,在控制台请求里面看到的是二进制还是什么？
>ws和wss的区别
>ssl层出了问题,去哪一层修改

>树的掌握 这里出了一道题,文件夹,怎么查找节点　　节点命名如何设计　修改节点会有哪些冲突

>有一篇文章,如何找出出现次数最多的词语

>快速排序
[【啊哈！算法】算法3：最常用的排序——快速排序](http://bbs.codeaha.com/thread-4419-1-1.html)

>flex

>计算机网络的七层模型，五层模型　这里gg
[计算机网络七层模型和五层模型](https://blog.csdn.net/wx19950101/article/details/77120473)
[计算机网络五层（七层）协议](https://blog.csdn.net/qq_26927285/article/details/54426657)
[SSL协议到底工作在OSI模型中的那一层？](https://blog.csdn.net/better2326/article/details/48371241)
OSI七层模型
1 应用层  2 表示层  3 会话层  4 传输层（其中之一：TCP） 5 网络层（其中之一：IP） 6 数据链路层 7 物理层
五层模型
1 应用层 （应用层+表示层+会话层）2 传输层 3 网络层 4 数据链路层 5 物理层

> OSI七个层次的功能：
  物理层
  为数据链路层提供物理连接，在其上串行传送比特流，即所传送数据的单位是比特。此外，该层中还具有确定连接设备的电气特性和物理特性等功能。 
  数据链路层
  负责在网络节点间的线路上通过检测、流量控制和重发等手段，无差错地传送以帧为单位的数据。为做到这一点，在每一帧中必须同时带有同步、地址、差错控制及流量控制等控制信息。 
  网络层
  为了将数据分组从源（源端系统）送到目的地（目标端系统），网络层的任务就是选择合适的路由和交换节点，使源的传输层传下来的分组信息能够正确无误地按照地址找到目的地，并交付给相应的传输层，即完成网络的寻址功能。 
  传输层
  传输层是高低层之间衔接的接口层。数据传输的单位是报文，当报文较长时将它分割成若干分组,然后交给网络层进行传输。传输层是计算机网络协议分层中的最关键一层，该层以上各层将不再管理信息传输问题。 
  会话层
  该层对传输的报文提供同步管理服务。在两个不同系统的互相通信的应用进程之间建立、组织和协调交互。例如，确定是双工还是半双工工作。 
  表示层
  该层的主要任务是把所传送的数据的抽象语法变换为传送语法，即把不同计算机内部的不同表示形式转换成网络通信中的标准表示形式。此外，对传送的数据加密（或解密）、正文压缩（或还原）也是表示层的任务。 
  应用层
  该层直接面向用户，是OSI中的最高层。它的主要任务是为用户提供应用的接口，即提供不同计算机间的文件传送、访问与管理，电子邮件的内容处理，不同计算机通过网络交互访问的虚拟终端功能等。
   

>echarts有改过底层源码吗

>es6

>let 和　const的区别

>function和箭头函数

>promise有多个请求  all race

>git

>webpack用过哪些插件和loader　　我都记不得插件的名字,看来要多记几个了233333333

>还有一些问题,记不清了

*************************************
### ** IBM一面 **

IBM一面,42分钟　那边好像有三个还是四个面试官　主要还是结合简历上的内容来问,还有一个英语面试,大概有五分钟的样子,说我英语还不错 233333333

自我介绍
用到了哪些前端技术

> 响应式布局,媒体查询
媒体查询断点怎么打的
[CSS媒体查询](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Media_queries)
[响应式小demo(主要是媒体查询)](https://www.sail.name/CSS_Demo/smallDemo.html)
[快捷提示：别忘记Viewport Meta标签](https://webdesign.tutsplus.com/zh-hans/articles/quick-tip-dont-forget-the-viewport-meta-tag--webdesign-5972)
[CSS || @media媒体查询](https://segmentfault.com/a/1190000008745305)

主要是流式布局还是栅格布局
响应式布局用在了你的哪些项目中
实习项目
介绍下什么是流量波动分析
在工作室，做项目都担任了哪些角色，做了哪些工作
项目管理怎么做的
需求变动
websocket　channel怎么建立的
websocket项目怎么做判断的
学了这么多技术,求职意向
如果非要在前端和机器学习选一个呢

> docker　虚拟机 有哪些区别
[docker容器与虚拟机有什么区别？](https://www.zhihu.com/question/48174633)
[Docker容器与虚拟机区别](https://www.cnblogs.com/pangguoping/articles/5515286.html)

> 有写过shell吗

> linux你常用的命令

> 如何设置hostname

> mysql数据引擎
[mysql 数据库引擎](https://www.cnblogs.com/0201zcr/p/5296843.html)

```
mysql> show engines;
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
```

还问了些问题，忘了
面试官说看了我的博客和github，所以都是问的些相关的内容把











