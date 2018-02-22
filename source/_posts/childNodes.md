---
title: childNodes
date: 2017-08-17 17:44:00
categories: Javascript
---

### ** 前言 **

今天有同学向我问了在[killCube](https://github.com/iamsail/killCube/)中遇到的BUG。

最终的原因是有关`Node.childNodes`的使用不当造成的。

本文做些记录。

### ** 重现BUG **

```HTML
<main id="main">
<div id="con">
    <!--   <div class="row">
        <div class="cell"></div>
        <div class="cell black"></div>
        <div class="cell"></div>
        <div class="cell"></div>
    </div>
    <div class="row">
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell black"></div>
        <div class="cell"></div>
    </div>
    <div class="row">
        <div class="cell black"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
    </div>
    <div class="row">
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell"></div>
        <div class="cell black"></div>
    </div>                                       -->
</div>
</main>

```

```javascript
function move( ) {
    var con=$('con');
    var top=parseInt(window.getComputedStyle(con,null)['top']);  
    if(speed+top>0)
    {top=0;}
    else {
        top+=speed;
    }
    con.style.top=top+"px";
    if (top==0)
    {
        creatrow();
        con.style.top='-100px';
        delrow();
    } else if(top==(-100 + speed )){
        var rows=con.childNodes;
        if((rows.length==5)&&(rows[rows.length-1].pass!==1)) {
            fail();
        }
    }
}

```

在以上代码中,move()函数中其中一部分逻辑是指 ** 当 `<div id="con">`的子节点长度为5时,且另一个逻辑`rows[rows.length-1].pass!==1`为真时,调用`fail()`函数,游戏结束。**

可这位同学以上的代码,却不能让游戏正常结束。

问题就出现在那段注释上,会导致`con.childNodes.length`在游戏的一开始就40+,远远超过了5,所以游戏不会结束。

**********

### ** 具体分析 **

** 分有注释和没有注释的两种情况进行讨论 **

#### ** 没有注释 **

```HTML
 <div id="con"></div>
```

```javascript
function $(id) {
        return document.getElementById(id)
    }
var con =$("con");
var rows=con.childNodes;
console.log(rows.length);
console.log(rows);
```
![0.png](/img/JavaScript/childNodes/0.png)

以上结果很容易理解,con节点并没有子节点

现在将HTML结构进行一些改变

```HTML
 <div id="con"> </div>
### 或者 
 <div id="con">
</div>
```
![1.png](/img/JavaScript/childNodes/1.png)

这样就有了一个子节点了。
<span class="under0">** 因为childNode将(空格,tab,换行等也计算了进去) **</span>

![2.png](/img/JavaScript/childNodes/2.png)
当然具体到空格还是回车换行等具体节点,它们的`data`属性还是不同,这里不做介绍。

#### ** 引入注释 **

```HTML
 <div id="con">
  <!--   <div></div> -->
</div>
```
![3.png](/img/JavaScript/childNodes/3.png)

<span class="under0">** 这种情况下,con节点有了三个子节点,除了两处的换行,注释也成为了一个节点 **</span>

************

#### ** 问题总结 **

回到最初的问题我们可以得出结论

<span class="under0"> ** 这位同学在HTML引入了空白以及换行符,导致子节点的个数远远增加,而不是预期的0,导致不能满足游戏结束的条件。而[killCube](https://github.com/iamsail/killCube/)中,子节点是通过脚本动态写入的,没有空格回车注释等,故不存在上述问题。**</span>

<span class="under0"> ** 有的时候,bug往往是因为HTML、CSS没写好造成的,导致需要写更多JS去维护。**</span>

### ** childNodes与children ** 

`Node.childNodes`返回包含<span class="under0"> ** 指定节点的子节点的集合 **</span>，该集合为即时更新的集合`（live collection）`。

`ParentNode.children`是一个只读属性，返回 一个<span class="under2"> ** `Node`的`子elements `的`活 HTMLCollection` **</span>。

`ParentNode.children`只返回** 元素 **的集合,因此使用`ParentNode.children`可以避免之前的问题出现

有关[nodeType](http://www.w3school.com.cn/jsref/prop_node_nodetype.asp)可以看看这儿。

### ** 封装 **

`ParentNode.children`只适用于`nodeType`为1的节点。

我稍微封装了一下,可以根据自己的需求使用

```javascript
    let  getXNodes = (parentNode) => {
            let arrayNodes = Array.from(parentNode.childNodes),
                filterResult = arrayNodes.filter((item,index,array) => {
            return (item.nodeName !== "#text")
        });
    };
```



### ** 参考 **

[js子节点children和childnodes的用法](http://www.cnblogs.com/carazk/p/6802307.html)

***********

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>


