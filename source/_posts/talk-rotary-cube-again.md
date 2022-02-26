---
title: 再谈旋转的立方体
date: 2017-07-28 14:32:00
categories: HTML&&CSS
---
### ** 背景 **

之前写过一篇博文[旋转的立方体](http://www.sail.name/2017/02/16/rotary-cube/)

昨天有朋友说,[websocket-animation](https://github.com/iamsail/websocket-animation)项目中能把旋转原点设置在正方体中心就更好了

以下是旋转原点不在正方体中心

<iframe src="http://www.sail.name/CSS_Demo/rotary-cube.html" style="width:500px;height:500px;">
</iframe>

以下是旋转原点在正方体中心

<iframe src="http://www.sail.name/CSS_Demo/rotary-cube-1.html" style="width:500px;height:400px;">
</iframe>

当时说明天修改。

今天看代码的时候,一时却没有搞定。<span class="under0">一番研究过后,发现让立方体旋转起来有两个思路,不同的思路会导致在旋转原点上不同的效果。</span>

本文对两种实现方式做些记录。

*****************

以下是旋转原点不在立方体中心(记作A)的部分CSS代码

```CSS
  #face1  {
        }
  #face2 {
       -webkit-transform-origin:right;
       -webkit-transform: rotateY(-90deg);
   }
   #face3 {
       -webkit-transform-origin:left;
       -webkit-transform: rotateY(90deg);
   }
   #face4 {
       -webkit-transform-origin:top;
       -webkit-transform: rotateX(-90deg);
   }
   #face5 {
       -webkit-transform-origin:bottom;
       -webkit-transform: rotateX(90deg);
   }
   #face6 {
       -webkit-transform: translateZ(-200px);
   }
```
[demo](http://www.sail.name/CSS_Demo/rotary-cube.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/master/rotary-cube.html)


*******************

以下是旋转原点在立方体中心((记作B)的部分CSS代码

```CSS
   .inner1{
       background-color: rgba(111,222,222,0.5);
        transform: translateZ(100px);
    }
    .inner2{background-color: rgba(211,122,322,0.5);
        transform: translateZ(-100px);
    }
    .inner3{background-color: rgba(211,120, 22,0.5);
       transform: rotateY(90deg) translateZ(100px);
    }
    .inner4{background-color: rgba(311,320, 122,0.5);
        transform: rotateY(90deg) translateZ(-100px);
    }
    .inner5{background-color: rgba(322,1, 222,0.5);
        transform: rotateX(90deg) translateZ(-100px);
    }
    .inner6 {
        background-color: rgba(211, 000, 000, 0.5);
        transform: rotateX(90deg) translateZ(100px);
    }
```
[demo](http://www.sail.name/CSS_Demo/rotary-cube.html)
[demo源码](https://github.com/iamsail/CSS_Demo/blob/master/rotary-cube.html)

****************

A与B的不同在于,<span class="under0">** A的具体实现的时候借助了`transform-origin`,改变了其中四个面的变形原点,此时A有了多个原点,且原点不再位于每个面的中心,即主对角线与次对角线的交点; **</span>

** 而B的实现完全依赖`transform`中的`rotate`和`translate`来改变立方体的每一个面在空间中的位置,六个面的变形原点都处于该面主对角线与次对角线的交点。**

** <span class="under0">对一个立方体来说,六个面,两个相对的面的旋转中心叠加位于整个立方体的中心,所以旋转原点在立方体中心。</span>**

****************

我的[websocket-animation](https://github.com/iamsail/websocket-animation)中立方体的旋转不在中心便是因为上述原因,因此只需要改下立方体的CSS实现代码即可。


