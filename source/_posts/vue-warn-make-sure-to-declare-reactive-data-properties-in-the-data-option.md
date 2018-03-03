---
title: Vue warn--Make sure to declare reactive data properties in the data option.
date: 2017-06-11 11:36:59
categories: Vue
---

### ** 本文记录开发Vue应用时的一个BUG **

错误大致如下
```
[Vue warn]: Property or method "xxxxxxxxx" is not defined on the instance but
referenced during render.
Make sure to declare reactive data properties in the data option.
```

*************************

### ** 重现BUG **

- #### ** 以下是我重现问题的demo **


![vue-warn-make-sure-to-declare-reactive-data-properties-in-the-data-option0.png](/img/Vue/vue-warn-make-sure-to-declare-reactive-data-properties-in-the-data-option0.png)


```
<div id="left" >
    <p id="text-left">{{ message }}</p>
</div>


//    var leftImage = new Vue ({
//        el:"#left"
//    });

    var leftText = new Vue({
        el:"#text-left",
        data:{
            message: '前端'
        }

    });
```

这种情况下页面是正常的,页面会显示前端两个字

********************

可如果我们取消掉注释,错误信息如下

![vue-warn-make-sure-to-declare-reactive-data-properties-in-the-data-option1.png](/img/Vue/vue-warn-make-sure-to-declare-reactive-data-properties-in-the-data-option1.png)

```
[Vue warn]: Property or method "message" is not defined on the instance but
referenced during render.
Make sure to declare reactive data properties in the data option.
```

![vue-warn-make-sure-to-declare-reactive-data-properties-in-the-data-option2.png](/img/Vue/vue-warn-make-sure-to-declare-reactive-data-properties-in-the-data-option2.png)


** 页面中没有了"前端"两字 **

******************

### ** 解决 **

<span class="under0">这里我直接给出解释</span>

去掉注释，有两个vue实例，p标签对应的实例是在div内部。这种情况message是挂载在p标签对应的实例的data属性里的。

根据报错信息的意思是，Property or method "message" is not defined on the instance but referenced during render。

message没有被定义，页面渲染的时候却存在。

<span class="under2"> ** 文档里，data部分说，推荐在创建实例之前，就声明所有的根级响应式属性。**</span>

所以data属性应该写在最外层的实例里面。如下

```
<div id="left" >
    <p id="text-left">{{ message }}</p>
</div>

var leftImage = new Vue ({
    el:"#left",
    data:{
        message: '前端'
    }
});

var leftText = new Vue({
    el:"#text-left"
});
```
