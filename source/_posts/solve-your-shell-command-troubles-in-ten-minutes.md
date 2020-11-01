---
title: 十分钟解决你的shell命令烦恼
date: 2020-09-19 15:13:00
categories: Linux
tags: Shell
---

### ** Preface **

Shell命令众多并且参数复杂。使用的时候常常需要去查询。本文将提供两个工具，帮助大家更高效的掌握Shell命令。

******************

### ** [tldr](https://github.com/tldr-pages/tldr) **

以往我们查询Shell命令的时候，除了使用搜索引擎，一般都是使用`man command`。比如我们如果要查询`find`命令的使用，那么就会使用`man find`。使用`man`命令我们可以查到命令的使用用途以及相关参数。但是！！！这个命令提供的东西实在是太全太多了，看起来头比较大。

![1.png](/img/linux/solve-your-shell-command-troubles-in-ten-minutes/1.png)


这里我要安利一个工具[tldr](https://github.com/tldr-pages/tldr)

倘若你是一位钱端开发工程师，可以使用如下命令进行安装。如果是其他语言用户，也可以使用对应的包管理器进行安装。

```
npm install -g tldr
```

使用十分简单`tldr command`。比如执行`tldr find`

![2.png](/img/linux/solve-your-shell-command-troubles-in-ten-minutes/2.png)

**<span class="under0"> 如上图所示，`tldr`这个工具会直接把Shell命令以具体命令例子的方式给出来。</span>**十分方便,简直把`man`命令按在地上摩擦。

************************

### ** Linux命令大全 **

如果你觉得上面的`tldr`工具还是过于复杂，看不懂。这里推荐一个中文网站[linuxde](http://man.linuxde.net/)

![3.png](/img/linux/solve-your-shell-command-troubles-in-ten-minutes/3.png)

输入你要查询的命令,比如`find`,会给出该命令十分详细的参数解释，以及大量的示例。

![4.png](/img/linux/solve-your-shell-command-troubles-in-ten-minutes/4.png)

![5.png](/img/linux/solve-your-shell-command-troubles-in-ten-minutes/5.png)

******************
### ** 最后 **

本文一共介绍了三个Shell命令相关的工具,分别是`man`, `tldr`, Linux命令大全。推荐使用`tldr`。






