---
title: matplotlib中文显示为方框(ubuntu) 
date: 2018-06-09 15:24:00
categories: Python
---

### ** Preface **

本文是对`matplotlib`画图时,中文显示为方框的解决的记录

***********************

### ** 解决 **



先下载字体[SimHei.ttf下载](https://github.com/StellarCN/scp_zh/blob/master/fonts/SimHei.ttf)

将字体放在对应的`ttf`目录下

比如我的是
`/home/sail/.local/lib/python3.5/site-packages/matplotlib/mpl-data/fonts/ttf`


目录可以通过以下代码进行查询

```python
import matplotlib
print (matplotlib.matplotlib_fname())
```

**********************

删除`~/.cache/matplotlib`的缓冲目录

**********************

![1.png](/img/python/chinese-display-cube-in-matplotlib-at-ubuntu/1.png)


修改`/home/sail/.local/lib/python3.5/site-packages/matplotlib/mpl-data/matplotlibrc文件`(这里应该是前面查询的目录下的`matplotlibrc文件`)，修改如下：

```
font.family         : sans-serif        

# 这里其实在最前面加上SimHei即可
font.sans-serif     : SimHei, Bitstream Vera Sans, Lucida Grande, Verdana, Geneva, Lucid, Arial, Helvetica, Avant Garde, sans-serif 
axes.unicode_minus，将True改为False，作用就是解决负号'-'显示为方块的问题   
```

然后重启即可。


***********************

上面要确认的就是配置文件一定要修改成功,我最初修改了一次,不知道为什么修改的`matplotlibrc`不见了。然后重新修改了下就可以了。


当然也可以在代码中修改配置,还是需要在代码中加入以下几行,才可以

```python
import matplotlib.pyplot as plt
font_name = 'SIMHEI' 
plt.rcParams['font.family'] = font_name #用来正常显示中文标签 
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号
```

最终效果:

![2.png](/img/python/chinese-display-cube-in-matplotlib-at-ubuntu/2.png)

***********************
### ** 参考　**
[SimHei.ttf下载](https://github.com/StellarCN/scp_zh/blob/master/fonts/SimHei.ttf)
[解决matplotlib不能显示中文的问题（Ubuntu）](https://blog.csdn.net/weixin_39599711/article/details/78813736)
[使用matplotlib警告Font family未找到](http://wenda.chinahadoop.cn/question/6828)
[Matplotlib的中文字体显示为方块的问题](https://blog.csdn.net/g11d111/article/details/77600114)
[python matplotlib 中文显示参数设置](https://segmentfault.com/a/1190000005144275)