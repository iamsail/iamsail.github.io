---
title: 牛顿迭代法解方程
date: 2018-06-16 12:41:00
categories: [算法]
---

### ** Preface **

前两天帮高中室友解一个方程,他课设中需要解的一个高次方程,使用的是牛顿迭代法,做下记录

********************

牛顿法的具体细节本文就赘述了,可以参考文末的链接。

![1.png](/img/算法/solve-equation-by-Newton-iterative-method/1.png)

*******************

**<span class="under0"> 一句话总结下,就是通过选择点,做切线,不断迭代下去,直到收敛。 </span>**

### ** 代码　**

```regexp
# -*- coding= utf-8 -*-

def f(x):
    # f的方程
    return 6900 * x ** 3 - 1767780 * x ** 2 + 250788032 * x - 120441587900

def f_first_order(x):
    # f的一阶导数
    return 6900 * 3 * x ** 2 - 1767780 * 2 * x + 250788032

def get_root(x0, max_iter=50, tol = 1e-8):
    # 将初始值浮点化
    p0 = x0 * 1.0
    for i in range(max_iter):
        # f的一阶导数不能为0，最普遍的说法是不能非正定
        p = p0 - f(p0)/ f_first_order(p0)

        # 如果小于精度值则退出迭代
        if abs(p - p0) < tol:
            return u'经过%s次的迭代，我们估计的参数值是%s' % (i, p)
        p0 = p

    print(u'已达到最大迭代次数， 但是仍然无法收敛')


# for x in range(-10000, 10000, 100):
#    print(get_root(x))
```


********************

### ** 参考 **

[如何通俗易懂地讲解牛顿迭代法求开方？](https://www.zhihu.com/question/20690553)
[python如何实现迭代法解方程?](https://www.zhihu.com/question/32280915)
[十行代码实现牛顿方法](http://python.jobbole.com/85295/)

