---
title: 图片的响应式处理
date: 2017-08-29 00:12:00
categories: HTML&&CSS
tags: 响应式(设计)
---

** 在这个暑假,有若干次需要对图片进行响应式处理,本文记录下我总结的方法,仅供参考。**

***************

这里我直接将图片作为整个页面的背景图

```css
html,body{
    margin: 0;
    padding: 0;
    position: relative;
    background: url("./background.jpg")no-repeat;
    width: 100%;
    height: 100%;
    max-width: 100%;
    background-position-x:50%;
}

@media screen and (min-width: 1000px){
    html,body{
        background-size: 100%;
        background-position-x:left;
        width: 100vw;
        height: 100vh;
        overflow: hidden;
    }
}
```
