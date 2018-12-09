---
title: 使用drawImage不显示图片
date: 2017-06-22 19:44:29
categories: HTML&&CSS
tags: Canvas
---

<code>CanvasRenderingContext2D.drawImage()</code>方法可以在Canvas上绘制图像。

### ** 语法 **

```
void ctx.drawImage(image, dx, dy);
void ctx.drawImage(image, dx, dy, dWidth, dHeight);
void ctx.drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);
```

### ** 参数 **

<code>image</code>

** 绘制到上下文的元素。允许任何的 canvas 图像源(CanvasImageSource)，例如：HTMLImageElement，HTMLVideoElement，或者 HTMLCanvasElement。**

<code>dx</code>

** 目标画布的左上角在目标canvas上 X 轴的位置。**
<code>dy</code>

** 目标画布的左上角在目标canvas上 Y 轴的位置。**

<code>dWidth</code>

** 在目标画布上绘制图像的宽度。 允许对绘制的图像进行缩放。 如果不说明， 在绘制时图片宽度不会缩放。**

<code>dHeight</code>

** 在目标画布上绘制图像的高度。 允许对绘制的图像进行缩放。 如果不说明， 在绘制时图片高度不会缩放。**
<code>sx</code>

** 需要绘制到目标上下文中的，源图像的矩形选择框的左上角 X 坐标。**

<code>sy</code>

** 需要绘制到目标上下文中的，源图像的矩形选择框的左上角 Y 坐标。**

<code>sWidth</code>

** 需要绘制到目标上下文中的，源图像的矩形选择框的宽度。如果不说明，整个矩形从坐标的sx和sy开始，到图像的右下角结束。**

<code>sHeight</code>

** 需要绘制到目标上下文中的，源图像的矩形选择框的高度。**

****************************

### ** 易错点 **

需要注意的是,调用drawImage时,若图片没有加载完,什么也不会发生。
<span class="under0">因此你应该用load时间来保证不会在加载完毕之前使用这个图片</span>

```
var img = new Image();   // 创建img元素
img.onload = function(){
  // 执行drawImage语句
}
img.src = 'myImage.png'; // 设置图片源地址
```

******************************



```
<body onload="draw();">
<canvas id="canvas" width="1000" height="1000"></canvas>
<script>
    function draw() {
        var ctx = document.getElementById('canvas').getContext('2d');
        var img = new Image();
        img.onload = function(){
            ctx.drawImage(img,0,0,500,500);
            ctx.beginPath();
            ctx.moveTo(30,96);
            ctx.lineTo(70,66);
            ctx.lineTo(103,76);
            ctx.lineTo(170,15);
            ctx.closePath();
            ctx.stroke();
        };
        img.src = './images/1.png';
    }
</script>
```
以上这段代码我在执行的时候，却没有加载出图片。

后来我将图片压缩了下,就可以正常工作了。

![drawImage-0.png](/img/canvas/drawImage-0.png)

