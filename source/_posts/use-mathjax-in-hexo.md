---
title: 在hexo使用mathjax
date: 2018-5-31 14:03:45
categories: hexo&&博客记录
---
### ** Preface **

本文是对在hexo下使用数学公式的方法记录,还是折腾了几十分钟,网上的有些文章有些太老了。

我使用的是[MathJax](https://github.com/mathjax/MathJax)。MathJax is an open-source JavaScript display engine for LaTeX, MathML, and AsciiMath notation that works in all modern browsers。

而[hexo-math](https://blog.csdn.net/emptyset110/article/details/50123231)是别人写好的一个自动部署`MathJax`的`hexo`插件。 

****************
### ** 使用 **

先安装`hexo-math`

```
npm install hexo-math --save
```

**************

接下来这里网上很多文章说要执行`hexo math install`,但是执行这个是没什么用的,hexo会提醒你没这个命令。

在`hexo-math`github已经给出了说明:

自从1.0.6版本过后,`hexo-math`使用了一种不同的方法注入`MathJax`到你的站点中,所以不需要再执行`hexo math install`,如果你之前执行过,执行`hexo math`即可

**************

接下来在你博客的配置文件`config.yml`加上如下的配置

`config.yml`

```regexp
math:
  engine: 'mathjax' # or 'katex'
  mathjax:
    src: custom_mathjax_source
    config:
      # MathJax config
  katex:
    css: custom_css_source
    js: custom_js_source # not used
    config:
      # KaTeX config
```


在博客主题配置文件`config.yml`开启`mathjax`
```
# Enable Mathjax
mathjax: true
```



****************

### ** 实践 **

<span class="under0">**在输入数学公式的时候，需要在数学公式的前后加入`$$`或`$`符号，将需要输入的公式加入到`$$`或`$`中间。**</span>

`$$`会使公式居中,`$`不会。

```regexp
$h(\theta) =$
$$h(\theta) =$$
$\alpha$
```
展示如下


$h(\theta) =$
$$h(\theta)=$$
$\alpha$

****************

### ** 存在的问题 **

到现在为止,还是存在一些问题的,

比如如下这一段

```regexp
$$
\begin{eqnarray}
\nabla\cdot\vec{E} &=& \frac{\rho}{\epsilon_0} \\
\nabla\cdot\vec{B} &=& 0 \\
\nabla\times\vec{E} &=& -\frac{\partial B}{\partial t} \\
\nabla\times\vec{B} &=& \mu_0\left(\vec{J}+\epsilon_0\frac{\partial E}{\partial t} \right)
\end{eqnarray}
$$
```
![1.png](/img/hexo&&博客记录/use-mathjax-in-hexo/1.png)

会出现一些问题，原因是`hexo`先用`marked.js`渲染，然后再交给`MathJax`渲染。在`marked.js`渲染的时候下划线`_`是被`escape`掉并且换成了`<em>`标签，即斜体字，另外`LaTeX`中的`\\`也会被转义成一个`\`，这样会导致`MathJax`渲染时不认为它是一个换行符了。

********************

### ** 修复问题(使Marked.js与MathJax共存) **


通过修改`marked.js`源码的方式来避开这些问题 
- 针对`marked.js`与`Mathjax`对于个别字符二次转义的问题，我们只要不让`marked.js`去转义`\\,\{,\}`在`MathJax`中有特殊用途的字符就行了。 
- 针对下划线的问题，取消`_`作为斜体转义，因为`marked.js`中`*`也是斜体的意思，所以取消掉`_`的转义并不影响我们使用`markdown`，只要我们习惯用`*`作为斜体字标记就行了。 
具体修改方式，用编辑器打开`marked.js`（在`./node_modules/marked/lib/`中）


Step 1:
```
  escape: /^\\([\\`*{}\[\]()# +\-.!_>])/,
```
替换成
```
  escape: /^\\([`*\[\]()# +\-.!_>])/,
```
这一步是在原基础上取消了对`\\,\{,\}`的转义(escape)

******************

Step 2:
```
  em: /^\b_((?:[^_]|__)+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```
替换成
```
  em:/^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```
*******************

重启hexo,可以看见前面那段被渲染成如下这样了


![2.png](/img/hexo&&博客记录/use-mathjax-in-hexo/2.png)

如果重启没有效果,执行下`hexo clean`

****************
### ** 参考 **

[hexo-math](https://github.com/hexojs/hexo-math#migration-note)
[搭建一个支持LaTEX的hexo博客](https://blog.csdn.net/emptyset110/article/details/50123231)
[Hexo下mathjax的转义问题](https://segmentfault.com/a/1190000007261752)
[如何在 hexo 中支持 Mathjax？](https://blog.csdn.net/u014630987/article/details/78670258)