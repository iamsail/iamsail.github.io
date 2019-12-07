---
title: react合成事件
date: 2019-12-07 12:01:45
categories: react
---

### ** Preface **
最近在代码中遇到了react合成事件的相关问题，本文做下记录。
******************

### ** 合成事件(SyntheticEvent) **

在react中,事件处理程序将传递 `SyntheticEvent` 的实例，这是一个跨浏览器原生事件包装器。 它具有与浏览器原生事件相同的接口，包括 `stopPropagation()` 和 `preventDefault()` ，除了事件在所有浏览器中他们工作方式都相同。

如果您发现由于某种原因需要底层浏览器事件，只需使用 `nativeEvent` 属性来获取它。 每个 `SyntheticEvent`对象都具有以下属性：

| 类型 | 属性 |
|---|---|
|boolean |bubbles    |        
|boolean |cancelable   |
|DOMEventTarget| currentTarget |
|boolean| defaultPrevented  |
|number| eventPhase  |
|boolean |isTrusted  |
|DOMEvent |nativeEvent  |
|void| preventDefault()  |
|boolean |isDefaultPrevented() |
|void |stopPropagation()  |
|boolean |isPropagationStopped() |
|DOMEventTarget |target |
|number |timeStamp |
|string |type |
******************

### ** 异步事件 **

`SyntheticEvent `对象是通过合并得到的。这意味着在事件回调被调用后，`SyntheticEvent `对象将被重用并且所有属性都将被取消。 这是出于性能原因。 因此，您无法以异步方式访问该事件。
<span class="under0">**如果要以异步方式访问事件属性，应该对事件调用 event.persist() ，这将从池中删除合成事件，并允许用户代码保留对事件的引用。**</span>

```javascript
clickHandle = (e) => {
    # 这一行必须不可少
    e.persist();
    console.log(e);
    console.log(e.type);
    # 这里是异步的
    setTimeout(() => {
      console.log(e);
      console.log(e.type);
    }, 100);

    # 这里也是异步的
    this.setState({event:event})
  }
```
*****************

### ** 合成事件机制 **

![syntheticEvent.png](/img/react/react-syntheticEvent/syntheticEvent.png)

`react`的所有事件都挂载在`document`中。当真实`dom`触发后冒泡到`document`后才会对`react`事件进行处理，所以原生的事件会先执行，然后执行`react`合成事件，最后执行真正在`document`上挂载的事件。


`react`事件机制分为三个部分:

<span class="under0">**事件注册部分，**</span>所有的事件都会注册到`document`上，拥有统一的调函数`dispatchEvent`来执行事件分发。`React`使用对象池来管理合成事件对象的创建和销毁，这样减少了垃圾的生成和新对象内存的分配，大大提高了性能。也就是说不同的事件，可能会共享一个合成事件对象。

触发`document`注册原生事件的回调`dispatchEvent`,获取到触发这个事件最深一级的元素,遍历这个元素的所有父元素，依次对每一级元素进行处理。构造合成事件。将每一级的合成事件存储在`eventQueue`事件队列中。遍历`eventQueue`。通过`isPropagationStopped`判断当前事件是否执行了阻止冒泡方法。如果阻止了冒泡，停止遍历，否则通过`executeDispatch`执行合成事件。释放处理完成的事件。

<span class="under0">**事件分发部分，**</span>首先生成合成事件，注意同一种事件类型只能生成一个合成事件`Event`，如`onclick`这个类型的事件，`dom`上所有带有通过`jsx`绑定的`onClick`的回调函数都会按顺序（冒泡或者捕获）会放到`Event._dispatchListeners` 这个数组里，后面依次执行它。也就是说，`React`以队列的方式，从触发事件的组件向父组件回溯，调用它们在JSX中声明的`callback`，`React`自身实现了一套事件冒泡机制。

<span class="under0">**事件存储部分，**</span>合成事件以对象池的方式实现创建和销毁，大大提高了性能。

******************
### ** 参考链接 **

- [合成事件(SyntheticEvent)](http://cn.voidcc.com/question/p-mvzpkdzm-t.html)
- [React.js onClick事件返回所有空值](http://cn.voidcc.com/question/p-mvzpkdzm-t.html)
- [揭秘React形成合成事件的过程](https://segmentfault.com/a/1190000013363525)
- [react合成事件](http://cycle263.github.io/blogs/framework/React/implement/event.html)
- [React 合成事件（SyntheticEvent）](http://www.ptbird.cn/react-syntheticEvent.html)