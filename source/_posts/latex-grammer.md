---
title: Latex语法
date: 2020-01-26 16:37:01
tags: [LATEX]
---

### ** Preface **

本文是对Latex语法的部分记录。因为我在平时写blog的时候,偶尔还是会需要写一些公式的，为了避免下次又去网上查找，直接记录在本文。

关于Hexo中如何使用Latex,之前已经写了一篇博客做介绍,[在hexo使用mathjax](http://www.sail.name/2018/05/31/use-mathjax-in-hexo/)。
***********************

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

### ** 语法 **

LaTeX 能够自动处理公式中的大多数字符之间的空格，但是有时候需要自己手动进行控制。

#### ** 公式中的空格 **

````
紧贴 $a\!b$
没有空格 $ab$
小空格 a\,b
中等空格 a\;b
大空格 a\ b
quad空格 $a\quad b$
两个quad空格 $a\qquad b$
````

#### ** 上标和下标 **
上标命令是 ^{角标}，下标命令是 _{角标}。当角标是单个字符时可以不用花括号（在 LaTeX 中，花括号是用于分组，即花括号内部文本为一组）。
```
$$x_1$$
$$x_1^2$$
$$x^2_1$$
$$x_{22}^{(n)}$$
$${}^*\!x^*$$    %（“\!” 表示其前后字符之间无间隙）

# 下面是示范例子
$x_1 \quad  x_1^2  \quad  x^2_1 \quad  x_{22}^{(n)}$
$x_1 \qquad  x_1^2  \qquad  x^2_1 \qquad  x_{22}^{(n)}$
$x_1 \  x_1^2  \  x^2_1 \  x_{22}^{(n)}$
$x_1 x_1^2 x^2_1 x_{22}^{(n)}$
```
$x_1 \quad  x_1^2  \quad  x^2_1 \quad  x_{22}^{(n)}$
$x_1 \qquad  x_1^2  \qquad  x^2_1 \qquad  x_{22}^{(n)}$
$x_1 \  x_1^2  \  x^2_1 \  x_{22}^{(n)}$
$x_1 x_1^2 x^2_1 x_{22}^{(n)}$

***********************

#### ** 数学模式和文本模式 **

LATEX可以排版公式与文字，故分为：数学模式和文本模式。如果你想要在公式中排版普通的文本（直立字体和普通字距），那么你必须要把这些文本放在\textrm{...} 命令中。
```
$x_1 \quad \textrm{哈哈哈哈} \quad  x_{22}^{(n)}$
```
$x_1 \quad \textrm{哈哈哈哈} \quad  x_{22}^{(n)}$

***********************

#### ** 分式 **

输入较短的分式时，最简单的方法是使用斜线，譬如输入 (x+y)/2，可得到(x+y)/2 。
要输入带有水平分数线的公式，可用命令：`\frac{分子}{分母}`。
```
$\frac{x+y}{2}$
$\frac{1}{1+\frac{1}{2}}$
```
$\frac{x+y}{2}$
$\frac{1}{1+\frac{1}{2}}$

***********************
#### ** 根式 **

排版根式的命令是：开平方：\sqrt{表达式}；开 n 次方：\sqrt[n]{表达式}

```
$\sqrt{2}<\sqrt[3]{3}$
$\sqrt{1+\sqrt[p]{1+a^2}}$
$\sqrt{1+\sqrt[^p\!]{1+a^2}}$
```
$\sqrt{2}<\sqrt[3]{3}$
$\sqrt{1+\sqrt[p]{1+a^2}}$
$\sqrt{1+\sqrt[^p\!]{1+a^2}}$

***********************
#### ** 求和与积分 **

排版求和符号与积分符号的命令分别为 \sum 和 \int，它们通常都有上下限，在排版上就是上标和下标。

```
$\sum_{k=1}^{n}\frac{1}{k}$
$\sum_{k=1}^n\frac{1}{k}$
$\int_a^b f(x)dx$
$\int_a^b f(x)dx$
微分符直体：$\int_a^b f(x)\mathrm{d}x$
```

$\sum_{k=1}^{n}\frac{1}{k}$
$\sum_{k=1}^n\frac{1}{k}$
$\int_a^b f(x)dx$
$\int_a^b f(x)dx$
$\int_a^b f(x)\mathrm{d}x$

***********************
#### ** 公式中的定界符 **
```
$($  $x_1$  $)$ 
$[$  $x_1$  $]$ 
$\|$ $x_1$   $\|$
$$\left(\sum_{k=\frac{1}{2}}^{N^2}\frac{1}{k}\right)$$

# 花括号
$\lbrace a*b \rbrace$

# 在上述这些定界符之前冠以 \left（修饰左定界符）或 \right（修饰右定界符），
# 可以得到自适应缩放的定界符，它们会根据定界符所包围的公式大小自适应缩放。
$$\left(\sum_{k=\frac{1}{2}}^{N^2}\frac{1}{k}\right)$$
```

$($  $x_1$  $)$ 
$[$  $x_1$  $]$ 
$\|$ $x_1$   $\|$
$$\left(\sum_{k=\frac{1}{2}}^{N^2}\frac{1}{k}\right)$$
$\lbrace a*b \rbrace$

***********************
#### ** 字体 **

- 使用\mathbb或\Bbb显示黑板粗体字，此字体经常用来表示代表实数、整数、有理数、复数的大写字母。
`$\mathbb{CHNQRZ}$`
$\mathbb{CHNQRZ}$ 
- 使用\mathbf显示黑体字
`$\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$`
$\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$
- 使用\mathtt显示打印机字体
`$\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$，$\mathtt{abcdefghijklmnopqrstuvwxyz}$`
$\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$，$\mathtt{abcdefghijklmnopqrstuvwxyz}$
- 使用\mathrm显示罗马字体
`$\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$，$\mathrm{abcdefghijklmnopqrstuvwxyz}$`
$\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$，$\mathrm{abcdefghijklmnopqrstuvwxyz}$
- 使用\mathscr显示手写体, 无小写
`$\mathscr{ABCDEFGHIJKLMNOPQRSTUVWXYZ}, $\mathscr{abcdefghijklmnopqrstuvwxyz}$`
$\mathscr{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$, $\mathscr{abcdefghijklmnopqrstuvwxyz}$
- 使用\mathfrak显示Fraktur字母（一种德国字体）
`$\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$, $\mathfrak{abcdefghijklmnopqrstuvwxyz}$`
$\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$, $\mathfrak{abcdefghijklmnopqrstuvwxyz}$

***********************

### ** 参考链接 **

[LATEX数学公式基本语法](https://www.cnblogs.com/houkai/p/3399646.html)
[常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)
[Demo LaTeX](http://simtalk.cn/2015/12/21/Demo-LaTeX/)
