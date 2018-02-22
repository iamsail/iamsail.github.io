---
title: deviceorientation
date: 2017-07-08 15:38:29
categories: HTML&&CSS
---

Web中有两个关于设备检测的API,一个是`DeviceMotionEvent`,它在加速度发生改变时触发;另一个是`DeviceOrientationEvent`,它在加速度传感器检测到设备在方向上变化时触发。

具体讲解之前,先要了解坐标系

### ** 坐标系 **

坐标系是一种描述物体位置的系统，它包含三个轴(X,Y,Z)，三个轴共同描述了物体相对于参照物的位置信息。当我们使用`orientation`和`motion`事件时会接触到两种坐标系统。

#### ** 地球坐标系 **

地球坐标系是相对于地心的，也就是说，它的轴是基于重力方向和磁场北方向。我们使用大写的X,Y,Z来描述地球坐标系的轴。

X轴沿着地平面，垂直于Y轴，向东为正，向西为负。
Y轴沿着地平面，向北(北极，不是磁场北)为正，向南为负。
Z轴垂直于地平面，想象成一条线连接着设备跟地心。背对地心的方向为正，指向地心的方向为负。


#### ** 设备坐标系 **

设备坐标系是相对于设备中心的。我们使用小写的x,y,z来描述它的轴。

![deviceorientation-0.png](/img/htmlcss/deviceorientation-0.png)

x轴沿着屏幕表面，向右为正，向左为负。
y轴沿着屏幕表面，向上为正，向下为负。
z轴垂直屏幕表面或键盘，远离屏幕的方向为正


********************************
### ** API **


`DeviceOrientationEvent`有以下五个属性

`alpha` 围绕z轴旋转时(左右旋转),y轴的度数差;是一个介于0到360之间的浮点数

`beta`  围绕x轴旋转时(前后旋转),z轴的度数差;是一个介于-180到180之间的浮点数

`gamma` 围绕y轴旋转时(扭转设备),x轴的度数差;是一个介于-90到90之间的浮点数

`absolute` 布尔值,表示设备是否返回一个绝对值

`compassCalibrated` 布尔值,表示设备的指南针是否校准过

*******************************

### ** demo **

#### ** <span class="under0">demo-1</span> **

<iframe src="http://www.sail.name/CSS_Demo/HtmlApiPractice/deviceorientation-one.html" style="width:260px;height:140px;">
</iframe>

#### ** <span class="under0">demo-2</span> **

<iframe src="http://www.sail.name/CSS_Demo/HtmlApiPractice/deviceorientation-tow.html" style="width:260px;height:280px;">
</iframe>

********************************

### ** 源码 **

- [demo-1](https://github.com/iamsail/CSS_Demo/blob/gh-pages/HtmlApiPractice/deviceorientation-one.html)
- [demo-2](https://github.com/iamsail/CSS_Demo/blob/gh-pages/HtmlApiPractice/deviceorientation-tow.html)

*******************************

### ** 参考 **
- [Orientation 和 motion 数据解释](https://developer.mozilla.org/zh-CN/docs/Web/Guide/Events/Orientation_and_motion_data_explained)
********************************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>

