---
title: 灵犀联云算法实习生笔试
date: 2018-06-24 21:04:30
tags: 笔试
password: 0Algorithm6,
---
### ** Preface **

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
























