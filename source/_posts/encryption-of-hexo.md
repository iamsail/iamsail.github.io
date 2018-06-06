---
title: hexo加密
date: 2018-06-05 21:37:17
categories: chrome-bugs
tags: hexo&&博客记录
---

### ** Preface **

本文是对hexo对文章加密以及这个过程中踩的一些坑(包括一些浏览器本身的坑)的记录

****************
### ** hexo-blog-encrypt **

加密是使用的插件[hexo-blog-encrypt](https://github.com/MikeCoder/hexo-blog-encrypt/blob/master/ReadMe.zh.md)

#### ** 安装 **

在 hexo 根目录的 `package.json` 中添加 `"hexo-blog-encrypt": "1.1.*"` 依赖。
然后执行 `npm install` 命令。
该插件会自动安装

<span class="under0"> ** 这里一定要注意的是不要直接`npm install hexo-blog-encrypt`,这样文章是会加密失败的,具体原因不知。 **</span>

******************

#### ** 快速开始 **

首先在 `_config.yml` 中启用该插件:
```
# Security
##
encrypt:
    enable: true
```
然后在你的文章的头部添加上对应的字段，如 `password`, `abstract`, `message`

```
---
title: hello world
date: 2016-03-30 21:18:02
tags:
    - fdsafsdaf
password: Mike
abstract: Welcome to my blog, enter password to read.
message: Welcome to my blog, enter password to read.
---
```

`password`: 是该博客加密使用的密码
`abstract`: 是该博客的摘要，会显示在博客的列表页
`message`: 这个是博客查看时，密码输入框上面的描述性文字

然后使用 `hexo clean && hexo g && hexo s`,来查看效果。


当然你也可以像我这样写入`package.json`中


```javascript
"scripts": {
    "start": "hexo g && hexo s",
    "build": "hexo g && hexo d"
  },
```

执行`hexo clean && npm start`即可

****************

### ** 自定义加密模板　**

做完前面的工作,就已经对文章加密成功了。不过默认的模板比较丑,官方提供了自定义模板的方法如下:

<span class="under0"> ** 如果你对默认的主题不满意，或者希望修改默认的提示和摘要内容，你可以添加如下配置在 `_config.yml` 中。**</span>
```
# Security
##
encrypt:
    enable: true
    default_abstract: the content has been encrypted, enter the password to read.</br>
    default_message: Please enter the password to read.
    default_template:
                    <script src="//cdn.bootcss.com/jquery/1.11.3/jquery.min.js"></script>
                    <div id="security">
                        <div class="input-container">
                            <input type="password" class="form-control" id="pass" placeholder=" {{message}} " />
                            <label for="pass"> {{message}} </label>
                            <div class="bottom-line"></div>
                        </div>
                    </div>
                    <div id="encrypt-blog" style="display:none">
                        {{content}}
                    </div>
```

以看见，和上面的配置文件对比来看，多了 `default_template` 和 `default_abstract` 和 `default_message` 配置项。

>`default_abstract` : 这个是指在文章列表页，我们看到的加密文章描述。当然这是对所有加密文章生效的。
`default_message` : 这个在文章详情页的密码输入框上方的描述性文字。
`default_template` : 这个是指在文章详情页，我们看到的输入密码阅读的模板，同理，这个也是针对所有文章的。
最后的 `content` 显示 div 的 id 必须 是 `'encrypt-blog'`，同时为了好看，也希望进行隐藏。
同时，必须要有一个 input 输入框，id 必须是"pass"，用来供用户输入密码。
输入密码之后，务必要有一个触发器，用来调用 `'decryptAES'` 函数。样例中以 `button` 来触发。

****************

这里我给出我自己修改的模板和样式,喜欢的同学可以拿去直接用

![1.png](/img/chrome-bugs/encryption-of-hexo/1.png)


[实际效果见我这篇demo](http://www.sail.name/2018/06/05/atest/)

** html **
```regexp
# Security
##
encrypt:
    enable: true
    default_abstract: 我的秘密花园
    default_message: 姿势,什么姿势?
    default_template:
                    <div id="security">
                        <div class="orz-container">
                            <input style="display:none">
                            <input type="password" class="get-key" id="pass" autocomplete="new-password"  placeholder="解锁新知识" />
				<div class="input-group-orz"> <button type="button" class="final-key" onclick="decryptAES()">O.O</button> </div>
                            <div class="bottom-line"></div>
                        </div>
                    </div>
                    <div id="encrypt-blog" style="display:none">
                        {{content}}
                    </div>
```

** css **
```css
/*============文章加密样式=============*/
.orz-container {
}

.orz-container input[type="password"] {
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 50%;
  width: 150px;
  height: 150px;
  padding: 0 0;
  border:none;
  font-size: 18px;
  text-indent: 4px;
  color: deepskyblue;
  border:2px salmon solid;
}


input:-webkit-autofill, input:-webkit-autofill:focus {
  z-index: 4;
  -webkit-box-shadow:0 0 0 100px white inset; /* Change the color to your own background color */
}


.orz-container .final-key {
  position: relative;
  margin: 0 auto;
  display: block;
  background: #FFFFFF;
  border: 3px solid skyblue;
  width: 100px;
  font-size: 16px;
  font-weight: 600;
  border-radius: 50%;
  height: 100px;
}

.orz-container .final-key:hover, .final-key:focus {
  background: yellow;
}
/*============文章加密样式=============*/
```
****************

### ** 意外的bug **

这次写这个加密样式的时候,遭遇了一个chrome存在了八年的问题,官方链接戳这儿

[Auto-filled input text box yellow background highlight cannot be turned off!](https://bugs.chromium.org/p/chromium/issues/detail?id=46543)

就是`input`自动填充的背景颜色是黄色,不能关上。那个颜色的确很....

折腾了很久,最终找到了一个hack的解决办法

```css
input:-webkit-autofill, input:-webkit-autofill:focus {
  z-index: 4;  /*  这句可以不要　*/
  -webkit-box-shadow:0 0 0 100px white inset; /* Change the color to your own background color */
}
```
****************

后来我又找到了一个办法,既然是自动填充会出现这个黄色,那让input不要自动填充不就好了吗

这里我列出解决方法,具体可以看本文的参考链接

```
# 一、使用隐藏input来接受浏览器自动填充，这样不会影响用户体验，也可以兼容所有浏览器
<input style="display:none">
or
<input type="password" style={{position: 'absolute', top: '-999px'}}/>

# 二、
<input type="password" class="get-key" id="pass" autocomplete="new-password"  placeholder="解锁新知识" />
```
****************
### ** 参考 **
[hexo-blog-encrypt](https://github.com/MikeCoder/hexo-blog-encrypt/blob/master/ReadMe.zh.md)
[禁止浏览器自动填充到表单](https://segmentfault.com/q/1010000006090445?_ea=1009491)
[不能忍受的屎黄: chrome表单自动填充](https://www.jianshu.com/p/368eb18f04cf)
[Auto-filled input text box yellow background highlight cannot be turned off!](https://bugs.chromium.org/p/chromium/issues/detail?id=46543)
[The ultimate list of hacks for Chrome’s forced yellow background on autocompleted inputs](http://webagility.com/posts/the-ultimate-list-of-hacks-for-chromes-forced-yellow-background-on-autocompleted-inputs)