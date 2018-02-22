---
title: 一行代码实现太极图(阴阳八卦)
date: 2016-12-09 12:23:45
categories: HTML&&CSS
---

### 用CSS实现太极图
之前有看别人用CSS实现太极图，写了老长的代码。
不过第一次见的时候，还是觉得挺好玩的。
CSS如下([效果预览](http://www.sail.name/CSS_Demo/%E9%98%B4%E9%98%B3%E5%85%AB%E5%8D%A6.html)):
		 #yin-yang {
            width: 96px;
            height: 48px;
            background: #eee;
            border-color: red;
            border-style: solid;
            border-width: 2px 2px 50px 2px;
            border-radius: 100%;
            position: relative;
        }
        #yin-yang:before {
            content: "";
            position: absolute;
            top: 50%;
            left: 0;
            background: #eee;
            border: 18px solid red;
            border-radius: 100%;
            width: 12px;
            height: 12px;
        }
        #yin-yang:after {
            content: "";
            position: absolute;
            top: 50%;
            left: 50%;
            background: red;
            border: 18px solid #eee;
            border-radius:100%;
            width: 12px;
            height: 12px;
        }

如果上面的代码，你看着还有问题，那需要补补CSS了

******

### 用HTML实现太极图
不过我发现用html实现这个太极图，只需要一行代码
代码如下([效果预览](http://www.sail.name/CSS_Demo/%E4%B8%80%E8%A1%8C%E5%85%AB%E5%8D%A6.html)):
			
			<span class="Sail">&#9775;</span>

******

** 这是什么原理呢？**
这个叫做[Unicode字符](https://unicode-table.com/en/)。
使用Unicode字符，需要在meta标签中将charset属性值设为utf-8
使用字符
- 一、工作量更加少
- 二、是响应的
- 三、不需要像使用其他icon那样引入文件，页面性能更高
- 四、Unicode字符，实现了一万多种不同的字符


** 很多工作别人已经帮我们做好了，只是我们不知道。**

<hr />
    <p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
    </p>