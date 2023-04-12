---
title: 滑动平均模型(tensorflow)
date: 2018-8-14 22:50:45
categories: 深度学习
tags: [TensorFlow, (MA)移动平均模型]
mathjax: true
---

在时间序列分析中，移动平均模型（简记为：MA模型）是一个常见的对单一变量时间序列进行建模的方法。

移动平均法是用一组最近的实际数据值来预测未来一期或几期内公司产品的需求量、公司产能等的一种常用方法。移动平均法适用于即期预测。当产品需求既不快速增长也不快速下降，且不存在季节性因素时，移动平均法能有效地消除预测中的随机波动，是非常有用的。移动平均法根据预测时使用的各元素的权重不同

** 移动平均法是一种简单平滑预测技术，它的基本思想是：根据时间序列资料、逐项推移，依次计算包含一定项数的序时平均值，以反映长期趋势的方法。因此，当时间序列的数值由于受周期变动和随机波动的影响，起伏较大，不易显示出事件的发展趋势时，使用移动平均法可以消除这些因素的影响，显示出事件的发展方向与趋势（即趋势线），然后依趋势线分析预测序列的长期趋势。**

******************

### ** 移动平均法的优缺点 **

使用移动平均法进行预测能平滑掉需求的突然波动对预测结果的影响。但移动平均法运用时也存在着如下问题：
1、加大移动平均法的期数（即加大n值）会使平滑波动效果更好，但会使预测值对数据实际变动更不敏感；
2、移动平均值并不能总是很好地反映出趋势。由于是平均值，预测值总是停留在过去的水平上而无法预计会导致将来更高或更低的波动；
3、移动平均法要由大量的过去数据的记录。

***************
### ** MA-IN-TF **

在tensorflow中提供了`tf.train.ExponentialMovingAverage`来实现滑动平均模型。在初始化`ExponentialMovingAverage`时,需要提供一个衰减率(decay)。这个衰减率将用于控制模型更新速度。`ExponentialMovingAverage`对每一个变量会维护一个影子变量(shadow variable),这个影子变量的初始值就是相应变量的初始值,而每次运行变量更新时,影子变量的值会更新为

$ shadow_variable = decay \times shadow_variable + (1 - decay) * variable$

其中`shadow_variable`为影子变量,variable为待更新的变量,decay为衰减率。从公式可以看出,decay决定了模型的更新速度,decay越大模型越稳定。在实际运用中,decay一般会设成非常接近1的数(比如0.999或0.9999)。为了使模型在训练前期可以更新得更快,`ExponentialMovingAverage`还提供了`num_updates`参数来动态设置decay的大小。如果在`ExponentialMovingAverage`初始化时提供了`num_updates`参数,那么每次使用的衰减率将是:

min{$decay, \frac{1 + num_updates}{10 + num_updates}$}


```python
import tensorflow as tf

# 定义一个变量用于计算滑动平均,初始值为0。
v1 = tf.Variable(0, dtype=tf.float32)
# step变量模拟神经网络中迭代的轮数, 可以用于动态控制衰减率
step = tf.Variable(0, trainable=False)

# 定义一个滑动平均的类(class),初始化时给定了衰减率(0.99)和控制衰减率的变量step
ema = tf.train.ExponentialMovingAverage(0.99, step)
# 定义一个更新变量的滑动平均操作。这里需要给定一个列表,每次执行这个操作时,这个列表中的变量都会被更新
maintain_averages_op = ema.apply([v1])


with tf.Session() as sess:
#     init_op = tf.initialize_all_variables()
    init_op = tf.global_variables_initializer()
    sess.run(init_op)
    
    # 通过ema.average(v1)获取滑动平均之后的变量取值。在初始化之后变量v1的值和v1的滑动平均都为0
    print(sess.run([v1, ema.average(v1)]))
    
    # 更新v1的值为5
    sess.run(tf.assign(v1, 5))
    #更新v1的滑动平均值。衰减率为min{0.99, (1+step)/(10+step) = 0.1} = 0.1
    sess.run(maintain_averages_op)
    print(sess.run([v1, ema.average(v1)]))
    
    sess.run(tf.assign(step, 10000))
    sess.run(tf.assign(v1, 10))
    sess.run(maintain_averages_op)
    print(sess.run([v1, ema.average(v1)]))
    
    sess.run(maintain_averages_op)
    print(sess.run([v1, ema.average(v1)]))
    
    
==========================
[0.0, 0.0]
[5.0, 4.5]
[10.0, 4.555]
[10.0, 4.60945]    
```

****************
### ** 参考 **
[移动平均模型](https://zh.wikipedia.org/wiki/%E7%A7%BB%E5%8A%A8%E5%B9%B3%E5%9D%87%E6%A8%A1%E5%9E%8B)
[滑动平均法、滑动平均模型法（Moving average，MA）](https://blog.csdn.net/qq_39521554/article/details/79028012)
[时间序列](https://zh.wikipedia.org/wiki/%E6%99%82%E9%96%93%E5%BA%8F%E5%88%97)
[markdown编辑数学公式](https://blog.csdn.net/huanhuan_coder/article/details/79325071)