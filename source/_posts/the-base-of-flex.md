---
title: Flex基础
date: 2017-07-09 15:38:29
categories: HTML&&CSS
---

本文是对flex基础知识的一些记录,参考的是阮一峰[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)

除了传统的 `display  + position + float`,flex现在也更多被大家用在项目中

先看一下兼容性

![the-base-of-flex-0](/img/htmlcss/the-base-of-flex-0.png)

算是挺不错了的,如果受众群体都是学生的话,可以大胆使用了

******************************

任何一个容器都可以指定为` Flex `布局,行内元素也可以使用` Flex `布局。设为` Flex `布局以后，子元素的`float、clear`和`vertical-align`属性将失效。

** 设置Flex的元素,是Flex容器,子元素称为Flex项目 **

<span class="under0">容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。</span>

主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；
交叉轴的开始位置叫做cross start，结束位置叫做cross end。
![the-base-of-flex-1](/img/htmlcss/the-base-of-flex-1.png)

项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。
******************************

### ** 容器属性 **

```
flex-direction
flex-wrap
flex-flow
justify-content
align-items
align-content

```

**************************

#### ** flex-direction **

取值
```
row | row-reverse | column | column-reverse

row
flex容器的主轴被定义为与文本方向相同。 主轴起点和主轴终点与内容方向相同。

row-reverse
表现和row相同，但是置换了主轴起点和主轴终点

column
flex容器的主轴和块轴相同。主轴起点与主轴终点和书写模式的前后点相同

column-reverse
表现和column相同，但是置换了主轴起点和主轴终点

```

[demo](http://www.sail.name/CSS_Demo/flex/demo_flex_direction.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/gh-pages/flex/demo_flex_direction.html)

*************

#### ** flex-wrap **
取值

```
nowrap | wrap | wrap-reverse

nowrap
flex 的元素被摆放到到一行，这可能导致溢出 flex 容器。
cross-start  会根据 flex-direction 的值 相当于 start 或 before。

wrap
flex 元素 被打断到多个行中。
cross-start 会根据 flex-direction 的值选择等于start 或before。
cross-end 为确定的 cross-start 的另一端。

wrap-reverse
和 wrap 的行为一样，但是 cross-start 和 cross-end 互换。
```

[demo](http://www.sail.name/CSS_Demo/flex/demo_flex_wrap.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/gh-pages/flex/demo_flex_wrap.html)

*******************

#### ** flex-flow **
取值

```
## CSS flex-flow 属性是 flex-direction 和 flex-wrap 的简写。

Formal syntax: <'flex-direction'> || <'flex-wrap'>
```
[demo](http://www.sail.name/CSS_Demo/flex/demo_flex_flow.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/gh-pages/flex/demo_flex_flow.html)

********************

#### ** justify-content **
取值

```
flex-start | flex-end | center | space-between | space-around

flex-start
从行首开始排列。每行第一个弹性元素与行首对齐，同时所有后续的弹性元素与前一个对齐。

flex-end
从行尾开始排列。每行最后一个弹性元素与行尾对齐，其他元素将与后一个对齐。

center
伸缩元素向每行中点排列。每行第一个元素到行首的距离将与每行最后一个元素到行尾的距离相同。

space-between
在每行上均匀分配弹性元素。相邻元素间距离相同。每行第一个元素与行首对齐，每行最后一个元素与行尾对齐。

space-around
在每行上均匀分配弹性元素。相邻元素间距离相同。
每行第一个元素到行首的距离和每行最后一个元素到行尾的距离将会是相邻元素之间距离的一半。

```

[demo](http://www.sail.name/CSS_Demo/flex/demo_justify_content.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/gh-pages/flex/demo_justify_content.html)

********************
#### ** align-items **
取值

```
flex-start | flex-end | center | baseline | stretch

flex-start
元素向侧轴起点对齐。

flex-end
元素向侧轴终点对齐。

center
元素在侧轴居中。如果元素在侧轴上的高度高于其容器，那么在两个方向上溢出距离相同。

baseline
项目的第一行文字的基线对齐。

stretch
弹性元素被在侧轴方向被拉伸到与容器相同的高度或宽度。
```

[demo](http://www.sail.name/CSS_Demo/flex/demo_align_items.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/gh-pages/flex/demo_align_items.html)

*******************
#### ** align-content **
取值
```
flex-start | flex-end | center | space-between | space-around | stretch

flex-start
所有行从垂直轴起点开始填充。第一行的垂直轴起点边和容器的垂直轴起点边对齐。接下来的每一行紧跟前一行。

flex-end
所有弹性元素从垂直轴末尾开始填充。最后一个弹性元素的垂直轴终点和容器的垂直轴终点对齐。
同时所有后续元素与前一个对齐。

center
所有行朝向容器的中心填充。每行互相紧挨，相对于容器居中对齐。
容器的垂直轴起点边和第一行的距离相等于容器的垂直轴终点边和最后一行的距离。

space-between
所有行在容器中平均分布。相邻两行间距相等。
容器的垂直轴起点边和终点边分别与第一行和最后一行的边对齐。

space-around
所有行在容器中平均分布，相邻两行间距相等。
容器的垂直轴起点边和终点边分别与第一行和最后一行的距离是相邻两行间距的一半。

stretch
拉伸所有行来填满剩余空间。剩余空间平均的分配给每一行
```


[demo](http://www.sail.name/CSS_Demo/flex/demo_align_content.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/gh-pages/flex/demo_align_content.html)

********************

### ** 项目属性 **
```
order
flex-grow
flex-shrink
flex-basis
flex
align-self
```
**************
#### ** order **
取值
```
<integer>
```
[demo](http://www.sail.name/CSS_Demo/flex/demo_item_property_order.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/master/flex/demo_item_property_order.html)

**************
#### ** flex-grow **
取值
```
<integer>,负值无效

默认为0，即如果存在剩余空间，也不放大。
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。
如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
```
[demo](http://www.sail.name/CSS_Demo/flex/demo_item_property_flex_grow.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/master/flex/demo_item_property_flex_grow.html)

**************
#### ** flex-shrink **
取值
```
<integer>,负值无效

定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。
如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
```
[demo](http://www.sail.name/CSS_Demo/flex/demo_item_property_flex_shrink.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/master/flex/demo_item_property_flex_shrink.html)

**************
#### ** flex-basis **
取值
```
<length> | auto; /* default auto */

定义了在分配多余空间之前，项目占据的主轴空间（main size）。
浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。
```
[demo](http://www.sail.name/CSS_Demo/flex/demo_item_property_flex_basis.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/master/flex/demo_item_property_flex_basis.html)

**************
#### ** flex **
取值
```
none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
```
[demo](http://www.sail.name/CSS_Demo/flex/demo_item_property_flex.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/master/flex/demo_item_property_flex.html)
*************
#### ** align-self **
取值
```
auto | flex-start | flex-end | center | baseline | stretch

auto
设置为父元素的 align-items 值，如果该元素没有父元素的话，就设置为 stretch。

flex-start
flex 元素会对齐到 cross-axis 的首端。

flex-end
flex 元素会对齐到 cross-axis 的尾端。

center
flex 元素会对齐到 cross-axis 的中间，
如果该元素的 cross-size 的尺寸大于 flex 容器，将在两个方向均等溢出。

baseline
所有的 flex 元素会沿着基线对齐，
The item with the largest distance between its cross-start margin edge and
its baseline is flushed with the cross-start edge of the line。

stretch
flex 元素将会基于容器的宽和高，按照自身 margin box 的 cross-size 拉伸。
```
*************
### ** 参考 **

- [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)




